드디어 Segmentation 학습을 마치고 ONNX로 나타났다.

Input Tensor은 (1, 3, 256, 256) 으로 batch_size, channel, width, height 이고
Output Tensor은 (1, 8, 256, 256) 으로 batch_size, classes, width, height 으로
각 좌표에 대한 classe가 정해진다. (0부터 7의 결과)

1 : sidewalk - 주황색 (255, 165, 0)
2 : braille_guid_blocks - 노란색 (255, 255, 0)
3 : roadway - 남색 (0, 0, 128)
4 : alley - 회색 (128, 128, 128)
5 : crosswalk - 하늘색 (135, 206, 235)
6 : bike_lane - 보라색 (128, 0, 128)
7 : caution_zone - 빨간색 (255, 0, 0)

이렇게 분류된다. 이 범위외의 숫자 (ex: 0)가 나오면 그냥 투명한색으로 지정하면 될 것 같다.

결과가...이상하다...ㅠㅠㅠ

그래도 표지판 띄우는건 가능하다.