# Classification

## 1. AlexNet
- Image Net 우승으로, ML의 패러다임 변화를 이끔
- LeNet와 비슷하지만 더 깊은 구조를 가짐(ReLU, Dropout 등을 사용)
- 11x11 convolution filter를 사용

## 2. VGGNet
- 3x3 크기의 Filter만 사용해, Parameter의 수를 감소시킴
- 3x3 Conv filters block과 2x2 max pooling으로 구성
- 3x3 Conv filters block과 2x2 max pooling으로 구성

## 3. GoogLeNet
- Inception Block을 통해 다양한 크기의 FIlter를 사용
- Bottleneck 구조(1x1 Filter)를 통해 Parameter의 수를 감소
- Auxiliary Classifier(2개의 FC layer와 1개의 1x1 Conv layer)를 통해 Gradient Vanishing Problem을 해결

## 4. ResNet
- Residual Block을 사용하여 Degradation Problem을 해결 
- Skip Connection을 사용하여 더 복잡하고 다양한 문제를 학습
- He Initialization을 사용
- 모든 Residual Block에 3x3 Conv layer를 쌓았고 모든 Conv layer 이후 BN을 적용
- Block마다 Spatial Pooling을 적용하여 Down-Sampling

## 5. DenseNet
- Dense Block들에서 모든 Output의 각 layer가 channel 축을 기준으로 Concatenation
- 모든 layer의 feature를 concatenate 함으로서 재사용이 용이

## 6. SENet
- 네트워크의 어떤 곳이라도 붙일 수 있음
- Parameter 증가량에 비해 모델 성능 향상도가 매우 큼
- Squeeze : GAP(Global Average Pooling)을 사용하여 중요 정보 추출
- Excitation : 채널당 중요도를 고려하고 재보정(recalibration)(FC -> ReLU -> FC -> Sigmoid)

## 7. EfficientNet
- Width, Depth, High Resolution을 모두 고려한 Model

## 8. Deformable convolution
- Irregular Filter를 사용함으로서 더 Flexible한 영역의 특징을 추출
- Offset을 계산하는 Branch와 Offset의 정보를 받아 Convolution 연산을 수행하는 Branch로 나뉨