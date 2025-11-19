🏡 보스턴 주택 가격 예측 모델
K-겹 교차 검증(K-Fold Cross-Validation) 및 최적 Epoch 탐색

이 저장소에는 Keras를 사용하여 보스턴 주택 가격 데이터를 분석하고 예측하는 신경망 모델의 훈련 및 평가 과정이 담겨 있습니다.
본 실습의 주요 목표는:

K-겹 교차 검증(K-Fold Cross-Validation) 을 활용하여 안정적인 성능을 확보하고

**과적합(Overfitting)**이 발생하기 전의 최적 훈련 Epoch 수를 찾아내는 것입니다.

🔑 1. 데이터 및 모델 개요
📌 데이터셋

Boston Housing Price Dataset

총 13가지 특성(feature) 기반으로 주택 가격(단위: $1,000)을 예측하는 회귀(Regression) 문제입니다.

📌 모델 구조 (Keras Sequential Model)

입력 데이터 정규화(Normalization)

2개의 Dense 은닉층 (각 64 units, 활성화 함수: ReLU)

출력층: 1 unit (주택 가격 예측)

📌 사용한 평가 지표

Loss: MSE (Mean Squared Error)

Metrics: MAE (Mean Absolute Error)

📈 2. 핵심 실습 내용 및 결과
A. ✔ K-겹 교차 검증 (4-Fold Cross-Validation)

목적: 훈련/검증 데이터 분할에 따른 편향을 줄이고 안정적인 일반화 성능을 평가

설정:

num_epochs = 500

k = 4개의 폴드 생성

fold #0 ~ fold #3까지 순차적으로 훈련 및 평가

각 fold별로 모델을 새로 정의하여 훈련시킴

B. ✔ 최적 Epoch 결정 (과적합 방지)

각 epoch마다 계산된 검증 MAE를 기록하여 average_mae_history를 생성

초반 MAE는 노이즈가 커서 제외하고, 이후 값에 대해 지수 이동 평균(EMA) 평활화를 적용

평활화된 MAE 그래프의 최저점을 찾아 최적 Epoch 수 결정

C. ✔ 최종 모델 훈련 및 테스트 평가

최적 epoch 수로 전체 훈련 데이터를 사용해 최종 모델 재학습

이후 테스트 데이터셋으로 최종 성능을 검증

📌 최종 모델 성능 (예시):

Test MAE: 약 [최종 결과 값 입력] ($1,000)

💾 3. 모델 저장 및 불러오기
✔ 모델 저장 형식

Keras 공식 권장 포맷인 .keras 확장자로 저장했습니다.

model.save(f'boston_price_predictor_20251118_fold_{i}.keras')

✔ 모델 로드 방법
from keras.models import load_model

model = load_model('boston_price_predictor_20251118_fold_0.keras')


가중치(weights)와 네트워크 구조까지 그대로 복원됩니다.
