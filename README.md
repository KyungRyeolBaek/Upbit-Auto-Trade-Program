# Upbit-Auto-Trade-Program
업비트 자동 매매 프로그램.

AI 부트캠프 3기 백경렬의 다섯번째 프로젝트입니다.

CS1에서는 자동으로 코인을 사고 파는 프로그램을 만들었습니다.

매 분 마다 오를 것이라 예측한 코인 종목들을 구매를 하고 판매하는 프로그램입니다.

알고리즘 방식은

1. 매 분 오를 종목 예측
2. 오를 종목 구매
3. 1분 뒤 모든 종목 판매
4. 위를 반복

전체적인 수익은 마이너스 이지만 재미있었던 프로젝트 중 하나였습니다.

#

전체적인 작동 원리는
1. 1분 간격으로 시간, 시가, 종가, 거래량의 데이터를 받아왔습니다.
2. 시가를 통해 종가를 예측하여 증가 비율이 양수가 되는 모든 코인들을 구매 리스트에 넣었습니다.
  
  ( 2, 3 과정 사이의 소비되는 시간에 변동하는 코인들도 있어 오차가 발생 합니다. )
  
3. 바로 구매 리스트에 있는 코인들을 전부 매수 합니다.
4. 일분이 지나면 매수한 코인을 전부 팝니다.
5. 수익률을 계산합니다.

시가를 통해 종가를 예측하는 부분의 ML 모델 구조는 아래와 같습니다.
```Python
globals()['{}_model'.format(item)] = Sequential([
        BatchNormalization(),
        Dense(128, activation='relu'),
        Layer.Dropout(0.2),
        Dense(256, activation='relu'),
        Layer.Dropout(0.2),
        Dense(512, activation='relu'),
        Dense(1, activation='relu') # 분류할 방법에 따라 개수를 조정해야 합니다. 
    ])
```
예측하는 부분의 로직과 ML 모델 부분을 바꾼다면 수익이 나게 자동 매매 프로그램을 만들 수 있지 않을까 싶습니다.

분 단위의 예측은 수수료가 계속 빠져나가기에 수익이 크게 나지 않습니다..

이를 참고해서 수정하시면 좋을 듯 싶습니다 !

감사합니다.
