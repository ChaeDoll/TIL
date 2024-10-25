그렇게 추출이 안되더니...
혹시나해서 onnx 라이브러리 다 uninstall하고
ipynb가 아닌 py에서 실행보았다.

잘....export 되네..? onnx가 뽑혔다!ㅋㅋㅋㅋ

근데 유니티에 import시켜도 제대로 작동이 되지 않는다.
모델을 변환할 필요가 있어보인다.

yolo11n  모델은 onnx 변환부터 문제가 많았는데, 변환을 해도 적용이 안된다고한다. (Split이라는 계층때문에)
따라서 yolov8n 모델로 다시 onnx 파일을 구하였다. 근데 마찬가지로 onnx import에서 split 계층의 문제가 발생하였다.

### Barracuda => Sentis
Unity Barracuda라는 라이브러리가 상대적으로 예전 라이브러리인듯 하다.
최근에는 Unity Sentis라는 AI 라이브러리가 존재하고, 여기서 이 문제를 해결해보고자 하였다.

com.unity.sentis 라는 name으로 Package를 다운로드한다. Barracuda는 지웠다.
![[Pasted image 20241025192713.png]]
모델이 잘 import 되는것을 확인할 수 있다!

이제 코드를 작성해서 모델을 가져오고, 입력 이미지를 3(rgb)x640x640 형태로 변경한다.
이후 Worker에서 모델을 생성하고, worker.Schedule(입력데이터)를 통해 입력 Tensor를 넣어 실행한다. Execute와 같은것이다.

결과 Tensor은 worker.P

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.Sentis;

public class ObjectDetectManager : MonoBehaviour
{
    [SerializeField] private ModelAsset objectDetectionModel;

    private Model runtimeModel;
    private Worker worker;
    public float[] results;

    void Start()
    {
        runtimeModel = ModelLoader.Load(objectDetectionModel);

        Texture2D inputTexture = Resources.Load<Texture2D>("inputImage");
        Texture2D resizedTexture = ResizeTexture(inputTexture, 640, 640);
        TensorShape shape = new TensorShape(1, 3, 640, 640);
        Tensor<float> inputTensor = TextureToTensor(resizedTexture, shape);

        // Worker 생성 및 모델 실행
        worker = new Worker(runtimeModel, BackendType.CPU);
        worker.Schedule(inputTensor);

        // 결과 텐서 추출 및 결과 배열에 저장
        Tensor outputTensor = worker.PeekOutput();
        print(outputTensor);

        inputTensor.Dispose();
        outputTensor.Dispose();
    }

    Texture2D ResizeTexture(Texture2D sourceTexture, int width, int height)
    {
        RenderTexture rt = RenderTexture.GetTemporary(width, height);
        Graphics.Blit(sourceTexture, rt);
        RenderTexture.active = rt;

        Texture2D resizedTexture = new Texture2D(width, height);
        resizedTexture.ReadPixels(new Rect(0, 0, width, height), 0, 0);
        resizedTexture.Apply();

        RenderTexture.active = null;
        RenderTexture.ReleaseTemporary(rt);

        return resizedTexture;
    }
    private Tensor<float> TextureToTensor(Texture2D texture, TensorShape shape)
    {
        var pixels = texture.GetPixels();
        var data = new float[pixels.Length * 3];
        for (int i = 0; i < pixels.Length; i++)
        {
            data[i * 3 + 0] = pixels[i].r;
            data[i * 3 + 1] = pixels[i].g;
            data[i * 3 + 2] = pixels[i].b;
        }
        return new Tensor<float>(shape, data);
    }

    private void OnDisable()
    {
        worker.Dispose();
    }
}

```