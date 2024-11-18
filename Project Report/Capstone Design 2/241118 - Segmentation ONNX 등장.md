드디어 Segmentation 학습을 마치고 ONNX로 나타났다.

Input Tensor은 (1, 3, 256, 256) 으로 batch_size, channel, width, height 이고
Output Tensor은 (1, 8, 256, 256) 으로 batch_size, classes, width, height 으로
각 좌표에 대한 classe가 정해진다. (0부터 7의 결과)

1 : sidewalk - 주황색 (255, 165, 0)
2 : braille_guid_blco