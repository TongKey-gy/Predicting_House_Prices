🏡 보스턴 주택 가격 예측 모델
K-겹 교차 검증(K-Fold Cross-Validation) 및 최적 Epoch 탐색을 통한 신경망 모델 최적화

📋 프로젝트 개요
Keras를 활용하여 보스턴 주택 가격 데이터셋을 분석하고 예측하는 회귀 모델을 구현합니다. 이 프로젝트는 K-겹 교차 검증을 통해 안정적인 성능을 확보하고, 과적합을 방지하기 위한 최적 훈련 Epoch를 찾는 데 중점을 둡니다.

🎯 주요 목표

✅ K-겹 교차 검증을 통한 모델의 일반화 성능 향상
✅ 과적합 발생 전 최적 Epoch 수 탐색
✅ 안정적이고 신뢰할 수 있는 주택 가격 예측 모델 구축


📊 데이터셋
Boston Housing Price Dataset

특성 개수: 13개 (범죄율, 방 개수, 접근성 등)
타겟: 주택 가격 (단위: $1,000)
문제 유형: 회귀(Regression)


🔧 모델 구조
Keras Sequential Model
입력층 (13개 특성)
    ↓
정규화(Normalization)
    ↓
Dense Layer (64 units, ReLU)
    ↓
Dense Layer (64 units, ReLU)
    ↓
출력층 (1 unit) - 주택 가격 예측
모델 설정

손실 함수: MSE (Mean Squared Error)
평가 지표: MAE (Mean Absolute Error)
옵티마이저: RMSprop


🚀 핵심 실습 과정
1️⃣ K-겹 교차 검증 (4-Fold Cross-Validation)
목적: 훈련/검증 데이터 분할에 따른 편향 제거 및 안정적인 성능 평가
설정:

총 Epoch: 500
Fold 개수: 4
각 Fold마다 모델을 새로 초기화하여 독립적으로 훈련

과정:
Fold #0: 데이터 분할 → 훈련 → 검증
Fold #1: 데이터 분할 → 훈련 → 검증
Fold #2: 데이터 분할 → 훈련 → 검증
Fold #3: 데이터 분할 → 훈련 → 검증
2️⃣ 최적 Epoch 결정 (과적합 방지)
방법:

각 Epoch마다 모든 Fold의 검증 MAE 기록
평균 MAE 계산 → average_mae_history 생성
초반 노이즈 제거 (첫 10개 데이터 포인트 제외)
지수 이동 평균(EMA)으로 평활화
평활화된 그래프에서 최저점 찾기 → 최적 Epoch 결정

시각화:

검증 MAE 변화 그래프
평활화된 MAE 곡선
최적 Epoch 지점 표시

3️⃣ 최종 모델 훈련 및 평가
과정:

최적 Epoch 수 적용
전체 훈련 데이터로 최종 모델 학습
테스트 데이터셋으로 최종 성능 검증


📈 예상 결과

검증 MAE: 약 2.5~3.0 (천 달러 단위)
테스트 MAE: 최적 Epoch 적용 시 과적합 최소화
최적 Epoch: 평활화 그래프 분석을 통해 자동 결정


🛠️ 사용 기술

Python 3.x
TensorFlow / Keras
NumPy
Matplotlib (시각화)


💡 핵심 학습 포인트

K-겹 교차 검증의 중요성과 구현 방법
과적합 탐지 및 최적 학습 시점 결정
데이터 정규화가 신경망 학습에 미치는 영향
평활화 기법을 통한 노이즈 제거 및 경향성 파악

Test MAE: 약 [최종 결과 값 입력] ($1,000)
