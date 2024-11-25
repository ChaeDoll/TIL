Segmentation이 왜 학습이 잘 안될까! 
학습이 잘 되었다면 스마트폰에서 작동해야한다. 그럴려면 엄청 경량화되어야한다.
논문 링크 - https://arxiv.org/pdf/1902.04502

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

class DepthwiseSeparableConv(nn.Module):
    def __init__(self, in_channels, out_channels, stride=1):
        super(DepthwiseSeparableConv, self).__init__()
        self.depthwise = nn.Conv2d(in_channels, in_channels, kernel_size=3, stride=stride, padding=1, groups=in_channels, bias=False)
        self.pointwise = nn.Conv2d(in_channels, out_channels, kernel_size=1, bias=False)
        self.bn = nn.BatchNorm2d(out_channels)
        self.relu = nn.ReLU()
def forward(self, x):
        x = self.depthwise(x)
        x = self.pointwise(x)
        x = self.bn(x)
        return self.relu(x)
        
class LearningToDownsample(nn.Module):
    def __init__(self):
        super(LearningToDownsample, self).__init__()
        self.conv = nn.Conv2d(3, 32, kernel_size=3, stride=2, padding=1, bias=False)
        self.dsconv1 = DepthwiseSeparableConv(32, 48, stride=2)
        self.dsconv2 = DepthwiseSeparableConv(48, 64, stride=2)
    def forward(self, x):
        x = self.conv(x)
        x = self.dsconv1(x)
        x = self.dsconv2(x)
        return x

class GlobalFeatureExtractor(nn.Module):
    def __init__(self):
        super(GlobalFeatureExtractor, self).__init__()
        self.bottleneck1 = DepthwiseSeparableConv(64, 96, stride=2)
        self.bottleneck2 = DepthwiseSeparableConv(96, 128, stride=2)
        self.ppm = nn.AdaptiveAvgPool2d((1, 1))  # Pyramid Pooling Module
    def forward(self, x):
        x = self.bottleneck1(x)
        x = self.bottleneck2(x)
        x = self.ppm(x)
        return x
        
class FeatureFusionModule(nn.Module):
    def __init__(self):
        super(FeatureFusionModule, self).__init__()
        self.conv1 = nn.Conv2d(192, 128, kernel_size=1, bias=False)
        self.bn = nn.BatchNorm2d(128)
        self.relu = nn.ReLU()
    def forward(self, high_res, low_res):
        x = torch.cat((high_res, low_res), dim=1)
        x = self.conv1(x)
        x = self.bn(x)
        return self.relu(x)
  
class Classifier(nn.Module):
    def __init__(self, num_classes):
        super(Classifier, self).__init__()
        self.dsconv1 = DepthwiseSeparableConv(128, 128)
        self.dsconv2 = DepthwiseSeparableConv(128, 128)
        self.conv = nn.Conv2d(128, num_classes, kernel_size=1, bias=False)
    def forward(self, x):
        x = self.dsconv1(x)
        x = self.dsconv2(x)
        x = self.conv(x)
        return F.interpolate(x, scale_factor=8, mode='bilinear', align_corners=False)

class FastSCNN(nn.Module):
    def __init__(self, num_classes):
        super(FastSCNN, self).__init__()
        self.learning_to_downsample = LearningToDownsample()
        self.global_feature_extractor = GlobalFeatureExtractor()
        self.feature_fusion = FeatureFusionModule()
        self.classifier = Classifier(num_classes)
    def forward(self, x):
        high_res = self.learning_to_downsample(x)
        low_res = self.global_feature_extractor(high_res)
        fused = self.feature_fusion(high_res, low_res)
        return self.classifier(fused)
# 모델 생성
if __name__ == "__main__":
    model = FastSCNN(num_classes=19)
    input_tensor = torch.randn(1, 3, 1024, 1024)
    output = model(input_tensor)
    print("Output shape:", output.shape)
```

커스텀 데이터셋을 가져와서 학습한다. 일단 한뭉치만 가져올까?

직접 Pytorch 사용해서 모델 만들고, 데이터셋 넣어서 학습하고, 경량화해서 사용할란다.
1024x1024로 입력하면 다운샘플링되며 128x128로 변환되는데, Classifier 이후 다시 업샘플링해서 1024x1024로 전달된다. 하지만 우리는 그냥 다운샘플링된 값을 그대로 활용한다. 
`return F.interpolate(x, scale_factor=8, mode='bilinear', align_corners=False)`
였던 코드를 `return x` 로 간단하게 변경하였다.

