# 2021 데이터 크리에이터 캠프
<p align="center"> ⏳ 2021.10.02 | 2021.10.16 | 이화여자대학교 잠자리 ⌛ </p>
<p align="center"><a href="http://creator.kbig.kr/"><img src="https://user-images.githubusercontent.com/63901494/137845544-dc611955-00f9-4f2e-8dc2-6dde2e62206c.png"></a></p>

## Program
* 예선/본선 각각 대회 **당일 공지된 과제를 3시간 이내에 해결하는 해커톤 방식**으로 진행되었습니다.
* Kaggle 리더보드를 통해 최종 모델을 평가하였습니다. 

## Preliminary Round
서울시에서 2015년 부터 시행한 무인 공공자전거 대여 서비스 "따릉이"는 해가 지날수록 이용하는 시민이 늘어나는 추세입니다. 하지만 2020년 9월 서울환경연합에서 진행한 '[자전거 이용에 관한 설문조사](http://ecoseoul.or.kr/archives/41430)'에 따르면 조사 대상 2,700명 중 27%의 응답자들이 따릉이 이용 시 가장 불편한 점으로 대여시 따릉이가 부족한 점을 지적하였다고 합니다. 이를 해소하기 위해 2019년 06월 부터 2020년 12월 까지의 날씨와 따릉이 이용량 정보를 활용하여 각 날짜에 해당하는 대여량 예측을 진행하였습니다. 

<!--
### Model
* LinearRegressor
* XGBoostRegressor
* LightGBMRegressor
  
### Optimization
* LightGBM
* Hyperparameter tuning - using optuna framework
  ```
  'colsample_bytree': 0.4,
  'learning_rate': 0.08,
  'max_depth': 5,
  'min_child_samples': 114,
  'num_leaves': 204,
  'reg_alpha': 0.0010251805749509925,
  'reg_lambda': 0.2671750951630589,
  'subsample': 1.0
  ```
* 10-Fold cross validation

### Result
R2 Score: 0.81940<br>
<img src="https://user-images.githubusercontent.com/63901494/139278440-acda6362-3f85-4991-9540-bc4c905c6021.png" width="300" height="300">
-->

## Final Round
주어진 뉴스 데이터의 내용/제목들로부터 특징들을 추출 후, 이를 기반으로 뉴스를 주제별로 분류하였습니다.

<!--
### Data
[AI-Hub 문서요약 텍스트](https://aihub.or.kr/aidata/8054)

### Model
* LSTM
* GRU
* KoBERT

# Optimization
* Dropout 추가
* Weight Decay 적용

### Result

## Reference 
* [SKTBrain/Kobert](https://github.com/SKTBrain/KoBERT)
-->


## Members
<table>
  <tr>
    <td align="center"><a href="https://github.com/Taehee-K"><img src="https://user-images.githubusercontent.com/63901494/129619988-1a959834-313c-443c-84c2-4fc2db8ef8f6.jpg" width="100" height="100"><br /><sub><b>김태희</b></sub></td>
    <td align="center"><a href="https://github.com/SK-jeong"><img src="https://user-images.githubusercontent.com/63901494/129582209-1d1d194e-cf3e-48d6-b097-35a7b855a683.jpg" width="100" height="100"><br /><sub><b>정성경</b></sub></td>
    <td align="center"><a href="https://github.com/jyjy318"><img src="https://user-images.githubusercontent.com/63901494/139084437-17d8f084-ee9c-4d20-b52a-e71f57a48991.png" width="100" height="100"><br /><sub><b>문지예</b></sub></td>
    <td align="center"><a href="https://github.com/YuKyeong97"><img src="https://user-images.githubusercontent.com/63901494/139084338-c1ff0768-8258-49d0-9628-66943e958814.png" width="100" height="100"><br /><sub><b>한유경</b></sub></td>
  </tr>
</table>

<!--
## Structure
-->