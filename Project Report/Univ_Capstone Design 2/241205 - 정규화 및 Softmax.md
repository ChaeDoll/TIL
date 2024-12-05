동주가 새로운 모델을 건네주었는데 자꾸 작동을 안한다.
문제가 돼서 Threshold까지 추가했는데도 작동을 안하더라.

동주도 문제를 파악하고 본인 파일과 비교해보았는데, 겉으로 보이는 문제는 없었다.

output값을 뽑아보니, 클래스 별 확률값이 나와야하는데 -3.5 ~ 4.7까지 정말 다양한 수가 나오길래 문제가 있는것을 알게되었다.

혹시나해서 Softmax 연산을 돌려보았지만 의미있는 결과를 얻지는 못했다. 한쪽으로 너무 편향되어 데이터가 나타나는 문제가 발생했다.

ipynb를 통해 파이썬 환경에서도 onnx를 실행시켜봐도 동일한 결과가 나타났다.

동주 컴퓨터의 python 모델을 제대로 확인해보았다.

입력 데이터에서 Nomalize 하여 입력하고, 출력할 때 Softmax로 출력하고 있었다.
그랬더니 ONNX 포맷을 사용해서도 제대로된 결과를 출력하는 것을 볼 수 있었다.
이제 Unity 환경에서 C#을 활용해서 정규화와 Softmax를 구현해주어야한다.

```csharp
private void NomalizeTensor(TensorFloat inputTensor, int height, int width)
{
	// ImageNet 평균 및 표준편차 값 (RGB 순서)
	float[] mean = { 0.485f, 0.456f, 0.406f };
	float[] std = { 0.229f, 0.224f, 0.225f };

	for (int y = 0; y < height; y++)
	{
		for (int x = 0; x < width; x++)
		{
			for (int c = 0; c < 3; c++) // RGB 채널
			{
				float value = inputTensor[0, y, x, c];
				value = (value / 255.0f - mean[c]) / std[c]; // 정규화
				inputTensor[0, y, x, c] = value; // 정규화 값 다시 저장
			}
		}
	}
}

private void ApplySoftmax(TensorFloat inputTensor, int numClasses, int height, int width)
{
	float[] logits = new float[numClasses];
	for (int y=0; y < height; y++)
	{
		for (int x=0; x < width; x++)
		{
			// 1. 각 픽셀의 Logits 값 가져오기
			for (int c=0; c < numClasses; c++)
			{
				int index = (c * height + y) * width + x;
				logits[c] = inputTensor[index];
			}

			// 2. Softmax 계산
			float[] probabilities = Softmax(logits);

			for (int c=0; c < numClasses ; c++)
			{
				int index = (c * height + y) * width + x;
				inputTensor[index] = probabilities[c];
			}
		}
	}
}

private float[] Softmax(float[] logits)
{
	float maxLogit = Mathf.Max(logits);
	float[] exps = new float[logits.Length];
	float sumExps = 0f;
	for (int i = 0; i < logits.Length; i++)
	{
		exps[i] = Mathf.Exp(logits[i] - maxLogit);
		sumExps += exps[i];
	}
	for (int i = 0; i < logits.Length; i++)
	{
		exps[i] /= sumExps;
	}
	return exps;
}
```

이처럼 1차원 배열로 입력되고 나오는 TensorFloat에 대해 입력 시 Normalize를 실행하고, 출력 시 Softmax를 실행하여 결과를 도출해내었다.

처음에 Nomalize가 잘 안되는 문제가 있었는데, (normalize만 통과하면 Texture 색상이 적용되지 않는 문제가 발생함) 입력되는 inputTensor가 batch, channel, height, width 인줄알았는데, batch, height, width, channel 인가보다.
