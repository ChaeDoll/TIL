나는 결과적으로 class는 무엇이고, box위치는 무엇이고 등.. 여러가지의 output을 내놓아야한다. yolo는 image-to-image 모델이 아니라, image-to-data이기에 이러한 변환에 어려움이 있었다. 

Worker.PeekOutput(index)으로 multiple outputs를 다룰 수 있다고 한다. 실제로 PeekOutput(1)처럼 index를 넣었는데, 출력 index가 1개라고 나타났다. 왜일까... 분명 여러가지 output을 얻어야하는데..
