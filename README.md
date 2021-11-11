# RugPull_Prediction_AI
러그풀 예측 AI모델 개발

# 1. 라벨링
 - Total Data Input : __Uniswap에 Pool이 생성된 토큰__ 
 + 전체 데이터에 대해서 유동성 풀을 기준으로, 러그풀이 발생했는지 아닌지에 대한 __True/False 라벨링__ 을 수행


# 2. Feature 도출
- 라벨링된 True/False 데이터에 대해서 학습시 사용할 Feature를 구한다. 이때, 각각의 Feature들은 __주어진 TimeStamp시점__ 까지의 Feature를 구한다.
- 주어진 TimeStamp란?
    1. 정상 : ~~토큰의 유동성 풀이 생성된 이후로 7일까지의 Feature~~
         -> 학습을 해본결과 Feature를 7일까지 하면, 스캠코인과의 Feature들의 경향성이 너무 심함. __1일__ 로 수정
    2. 스캠 : 러그풀 발생 직전까지의 Feature
- 특이사항 : 라벨링된 데이터들의 Feature를 구하는 과정에서, 오류가 나는 상황이 많다. 해당데이터들은 삭제시켜서 Dataset의 크기가 줄어듬

# 3. 학습

# 💀진행하면서 에러 사항
 11.08 
 - 정상 데이터들의 TimeStamp를 30일로 하면, 지금 뽑은 피처들이 스캠 데이터랑 편차가 너무 큼. 확실히 초기 토큰들은 스캠으로 분류될거 같긴한데... 너무 전부 스캠으로 분류 될거 같아서 바꿈
 - Feature를 뽑다보면 별에별 에러가 다 나옴. 현재 Labeling_v1.2가 최종이라고 했는데, Feature를 뽑으면서 에러 나는것들 그냥 삭제시키기로 함. 갯수 줄어들 듯 
 - Feature를 뽑고 보니, 각각의 Feature를 보면 상위 1~2%정도는 지우는게 학습에 좋아보임.. 라벨링이 잘못된 경우도 있는거 같고 너무 튀는 애들이 좀 있음.


# 추후 진행 사항
- 현재 정상으로 라벨링한 데이터들이 __너무 정상__ 인 상황. 너무 정상인 애들과 너무 스캠인 애들이 라벨링 된걸로 학습을 시키니까 정확도가 100퍼가 나오지..
- 정상 라벨링 중, 너무 Official한 애들은 제외한다.(경향성이 너무 커지기 때문) -> TxCount를 기준으로 하던.. Token이 생성된 날짜가 20.05이전이면 그것도 삭제. 특성이 다름
 
