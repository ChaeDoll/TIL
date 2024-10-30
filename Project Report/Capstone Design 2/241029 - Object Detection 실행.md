나는 결과적으로 class는 무엇이고, box위치는 무엇이고 등.. 여러가지의 output을 내놓아야한다. yolo는 image-to-image 모델이 아니라, image-to-data이기에 이러한 변환에 어려움이 있었다. 

Worker.PeekOutput(index)으로 multiple outputs를 다룰 수 있다고 한다. 실제로 PeekOutput(1)처럼 index를 넣었는데, 출력 index가 1개라고 나타났다. 왜일까... 분명 여러가지 output을 얻어야하는데..

다양한 것들을 사용하고 얻은것은...
        var result = outputTensor.DownloadToArray();
        var json = result.Serialize().json;
    라는 메소드를 작성해보니, json 형태의 결과물을 얻을 수 있게 되었다.
유니티 Console에는 출력에 제한이 있기에 해당 데이터를 txt 메모장 파일로 저장시켰다.
![[Pasted image 20241029182459.png]]
컴이 죽었다...

현재 Output의 Tensor의 size가 Float(1, 84, 8400) 이다.
한개 사진에 대해 84개의 클래스로 분류되어 값이 8400개 있는 것을 판단하였다. (?) 맞나

값들이 규칙성이 있다. 분명... x쭈루룩, y쭈루룩, mask 쭈루룩..이렇게 되어있을 가능성이 크다.
규칙을 찾던 중, 확실한 탐색을 위해 파이썬에서 yolo11n.pt  모델을 실행해보고, 그 결과를 통해 어떻게 반환되는지 찾고자 하였다.

https://jseobyun.tistory.com/562
onnx 변환은 해주지만 NMS가 빠진상태로 변환하고 있는 상황이 딱 내 상황이었다.
원래는 bounding box 정보와 class 별 confidence를 나타내는 N x (4+C) 형태여야하는데 (4 + C) x 8400같은 이상한 Dimension 결과가 나온다.ㄴ

우선 Transpose해주었다. 그리고 결과를 출력하니, 
15.1, 3.81, 30.48, 7.73 그리고 80개의 0.000어쩌구...들이 나왔다. 이것은 4개의 xywh과 80개의 클래스에 대한 score라고 생각했다.

따라서 코드를 작성했다.
```
 var result = outputTensor.ReadbackAndClone();
        for (int i = 0; i < numDetections; i++)
        {
            int index = i * (4 + numClasses);
            float x = result[index];
            float y = result[index + 1];
            float w = result[index + 2];
            float h = result[index + 3];
            float maxScore = 0f;
            int classId = -1;
            // Max Class Score 계산
            for (int j = 0; j<numClasses; j++) 
            {
                float score = (result[index + 4 + j]);
                if (score > maxScore)
                {
                    maxScore = score;
                    classId = j;
                }
            }
            // Threshold 반영
            if (maxScore > threshold)
            {
                DetectionResult detection = new DetectionResult
                {
                    x = x,
                    y = y,
                    width = w,
                    height = h,
                    classId = classId,
                    confidence = maxScore
                };
                results.Add(detection);
            }
        }
        foreach (var item in results)
        {
            print("[" + item.x + ", " + item.y + ", " + item.width + ", " + item.height + ", " + item.classId + ", " + item.confidence + "]");
        }
```
시그모이드도 정의해놨고, 
```
 private float Sigmoid(float value)
    {
        return 1f / (1f + Mathf.Exp(-value));
    }

```
DetectionResult라는 Class도 만들어두었다.
```
public class DetectionResult
{
    public float x;
    public float y;
    public float width;
    public float height;
    public int classId;
    public float confidence;
}
```

Confidence? Score? 저 값이 너무 작아서일까 모르겠는데 너무 숫자가 작다. (0.00001보다 작은 수준) 그래서 출력값들을 정규화 해줘야할것같다.