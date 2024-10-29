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

값들이 규칙성이 있다. 분명... x