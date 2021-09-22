# Semantic Segmentation

## Fully Convolutional Networks(FCN)
- Fully Connected Layer에 1x1 Conv.filter를 사용하여 공간 정보를 유지함
- end-to-end 구조를 가지는 첫 semantic segmentattion

## Hyper-columns for object segmentation
- low level layer와 high level layer의 특징을 합쳐서 사용
- FNC과 달리 end-to-end 구조가 아님
- FC 부분의 hypercolumn은 모든 위치가 동일한 정보를 공유함을 의미

## U-Net
- FCN의 skip connection과 비슷하게 low level layer와 high level layer를 결합하는 방법을 제시
- Overlap-tile strategy를 사용
- 객체 경계를 잘 구분하도록 Weighted Loss를 제시

## DeepLab
- Conditional Random Fields (CRFs)를 후처리로 사용
- Dilated Convolution을 사용하여 더 넗은 Receptive filed를 고려(parameter 수는 늘어나지 않음)
- Atrous convolution과 Depthwise separable convolution를 결합하여 연산을 줄임