# Object Detection
## R-CNN
- Selective Search를 사용하여 Region Proposal을 추출
- 추출된 Region은 Warp되어 CNN 연산을 수행
- Classifier는 SVM을 사용

## SPPNet
- Spatial Pyramid Pooling(SPP)를 사용하여 CNN을 한 번만 수행
- SPP를 사용함으로서 입력 이미지 크기에 상관없이 항상 동일한 크기의 결과를 얻음

## Fast R-CNN
- RoI Pooling을 사용하여 RoI를 CNN에 한 번만 수행
- Classification과 Bounding Box Regression을 하나의 모델에서 학습(End-to-End)

## Faster R-CNN
- Region Proposal Network(RPN)을 사용하여 RoI를 추출
- RPN에서 k개의 Anchor Box를 미리 정의하여 사용
- Non-Maximum Suppression(NMS)를 사용하여 Proposal 개수를 줄임