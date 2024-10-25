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

이제 코드를 작성해서 모델을 가져오고, 입력 이미지를 