# 인공지능 수업 과제


## <실험 설정>
- 데이터셋: FashionMNIST
- 학습 데이터셋: 60,000개의 이미지
- 테스트 데이터셋: 10,000개의 이미지
- 입력 이미지 크기: 28x28
- 클래스 수: 10 (FashionMNIST 클래스)
- 학습 에폭: 100
- 배치 크기: 64
- 최적화 알고리즘: 확률적 경사 하강법 (SGD)
- 학습률: 0.01
- 모멘텀: 0.9
- 가중치 감쇠: 0.0001
- 손실 함수: 교차 엔트로피 손실
- 초기화: He 초기화
- 디바이스: CUDA지원하는 GPU

## <모델 세부 정보>
1. ResNet-50 : 50개의 레이어로 구성되며 잔여 연결(residual connection)을 사용
    - 아키텍처: 합성곱 레이어 ➡️ 잔여 블록 ➡️ 전역 평균 풀링 ➡️ 완전 연결 레이어
    - 각 잔여 블록은 2개 또는 3개의 합성곱 레이어와 숏컷 연결(shortcut connection)을 포함
    - 활성화 함수: ReLU
    - 각 합성곱 레이어 후에 배치 정규화를 적용
2. ResNext-50 : ResNet50과 유사하지만 그룹 컨볼루션(group convolution)을 적용
    - 잔여 블록 내 각 합성곱 레이어를 그룹으로 나눔 
    - 그룹의 개수는 네트워크의 카디널리티(cardinality)를 결정
    - 활성화 함수, 배치 정규화 및 기타 세부 정보는 ResNet-50과 동일
  동일한 모델 세부 정보와 하이퍼파라미터 설정을 사용하여 ResNet-50과 ResNext-50의 성능을 비교함으로써 그룹 컨볼루션의 영향을 분석하고자 한다. ResNet50는 그룹 컨볼루션을 사용하지 않는 기준 모델로 작용하며, ResNext50은 그룹 컨볼루션 적용의 효과를 확인한다.

-----------------------------------------
## 1. Experimental setting and implementation details

| Learning rate | Epoch | Batch size | Model depth | Types of optimizer |
| --- | --- | --- | --- | --- |
| 0.01 | 100 | 64 | 50 | SGD |


## 2. Experimental result

| Model | FLOPs | #parameters | Accuracy(Top-1) | Accuracy(Top-5) |
| --- | --- | --- | --- | --- |
| ResNet | 4.04 G | 23.52M | 88.79% | 99.79% |
| ResNext | 4.18 G | 22.99M | 89.99% | 99.85% |
