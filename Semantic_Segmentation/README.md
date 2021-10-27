# Semantic Segmentation

### Fully Convolutional Networks(FCN)
- Fully Connected Layer에 1x1 Conv.filter를 사용하여 공간 정보를 유지함
- end-to-end 구조를 가지는 첫 semantic segmentation
- 문제점
    - 객체의 크기가 크거나 작은 경우 예측을 잘 하지 못함
    - Object의 디테일한 모습이 사라지는 문제 발생

## 1. Decoder 개선
### DeconvNet
- CNN은 VGG16을 사용
    - 13개의 층으로 이루어짐
    - ReLU와 Pooling이 Convolution 사이에서 이루어짐
    - 7x7 Convolution 및 1x1 Convolution을 활용
- Deconvolution Network는 Unpooling, Deconvolution, ReLU로 이루어짐
    - Unpooling은 디테일한 경계를 포착
    - Transposed Convolution은 전반적인 모습을 포착
- Unpooling
    - 일반적인 Pooling의 경우 노이즈를 제거하는 장점이 있지만 그 과정에서 정보가 손실
    - Unpooling을 통해서 Pooling시에 지워진 경계에 정보를 기록했다가 복원
    - 학습이 필요없기 때문에 빠름
- Deconvolution (Transposed Convolution)
    - Input Object의 모양으로 복원
    - 순차적인 층의 구조가 다양한 수준의 모양을 잡아냄(low level : 전반적인 모습, high level : 구체적인 모습)

### SegNet
- 자율 주행과 같은 분야에 있어서 class를 빠르고 정확하게 구분할 수 있게 고안
- DeconvNet과 같이 Encoder와 Decoder Network가 대칭으로 이루어짐
- DeconvNet의 Encoder 구조에서 중간의 1x1 Convolution을 제거
    - Weight Parameter 감소
    - 학습 및 추론 시간 감소
- DecovnNet의 Decoder에서 Deconvolution을 사용했다면 SegNet에서는 Convolution을 사용

## 2. Skip Connection 활용
### FC DenseNet
- Skip Connnection을 활용
- Dense Block을 사용

### U-Net
- FCN의 skip connection과 비슷하게 low level layer와 high level layer를 결합하는 방법을 제시
- Overlap-tile strategy를 사용
- 객체 경계를 잘 구분하도록 Weighted Loss를 제시

## 3. Receptive Field 확장
### DeepLab v1
- Conditional Random Fields (CRFs)를 후처리로 사용
- Dilated Convolution을 사용하여 더 넗은 Receptive filed를 고려(parameter 수는 늘어나지 않음)
- Atrous convolution과 Depthwise separable convolution를 결합하여 연산을 줄임

### DilatedNet
- 다양한 크기의 Dilated Convolution을 사용하여 다양한 Receptive Field를 고려

### DeepLab v2
- 성능 향상을 위해 더 깊은 ResNet-101 사용
- ASPP를 적용하여 다양한 크기의 Receptive Field를 고려

### PSPNet
- Mismatch되거나 Category 구분을 잘 못하는 문제를 해결하기위해 고안
- 1x1, 2x2, 3x3, 6x6 출력의 Average Pooling을 적용하여 주변 정보를 파악해서 객체를 예측

### DeepLab v3+
 - Encoder - Decoder 구조 : Encoder에서 Spatial Dimension의 축소로 인해 손실된 정보를 Decoder에서 점진적으로 복원
    - Encoder
        - 수정된 Xception을 Backbone으로 사용
        - Atrous Separable Convolution을 적용한 ASPP 사용
        - Backbone내 low-level feature와 ASPP 모듈 출력을 모두 Decoder에 전달
    - Decoder
        - ASPP 모듈의 출력을 Up-sampling하여 low-level feature와 결합
        - 결합된 정보는 Convolution 연산 및 Up-sampling되어 최종 결과 도출
        - 기존의 단순한 Up-sampling 연산을 개선시켜 Detail을 유지
    - Xception
        - Depthwise Separable Convolution(Depthwise Convolution + Point Wise Convolution)을 사용
        - Depthwise Convolution : 각 채널마다 다른 Filter를 사용하여 Convolution 연산 후 결합
        - Pointwise Convolution : 1x1 Convolution 연산