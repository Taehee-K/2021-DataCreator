# 2021 데이터 크리에이터 캠프
<p align="center"> ⏳ 2021.10.02 | 2021.10.16 | 이화여자대학교 잠자리 ⌛ </p>
<p align="center"><a href="http://creator.kbig.kr/"><img src="https://user-images.githubusercontent.com/63901494/137845544-dc611955-00f9-4f2e-8dc2-6dde2e62206c.png"></a></p>

## Program
* 예선/본선 각각 대회 **당일 공지된 과제를 3시간 이내에 해결하는 해커톤 방식**으로 진행되었습니다.
* Kaggle 리더보드를 통해 최종 모델을 평가하였습니다. 

## Preliminary Round
서울시에서 2015년 부터 시행한 무인 공공자전거 대여 서비스 "따릉이"는 해가 지날수록 이용하는 시민이 늘어나는 추세입니다. 하지만 2020년 9월 서울환경연합에서 진행한 '[자전거 이용에 관한 설문조사](http://ecoseoul.or.kr/archives/41430)'에 따르면 조사 대상 2,700명 중 27%의 응답자들이 따릉이 이용 시 가장 불편한 점으로 대여시 따릉이가 부족한 점을 지적하였다고 합니다. 이를 해소하기 위해 2019년 06월 부터 2020년 12월 까지의 날씨와 따릉이 이용량 정보를 활용하여 각 날짜에 해당하는 대여량 예측을 진행하였습니다. 

### Data
* 결측치 확인<br>
  <img src="https://user-images.githubusercontent.com/63901494/140647241-21a2df94-1ec9-40c3-9528-64daecb74a99.png" width="500">
  * `Temperature`와 `Windspeed`, `Dewpoint`에 소량의 결측치 존재
  * `Rainfall`과 `Snow`에 대량의 결측치 존재
* 날짜별 EDA<br>
  * 연도별, 월별 분석<br>
    <img src="https://user-images.githubusercontent.com/63901494/140647546-3b1a1bea-62d3-4d3f-901d-a4151c67547a.png" width="600">
    * 19년도보다는 20년도에 대여량이 높다
    * 상대적으로 따뜻한 4월~10월 까지의 대여량이 높다
  * 요일별 분석 <br>
    <img src="https://user-images.githubusercontent.com/63901494/140647739-0430c856-7582-43a5-918a-59207ca1876e.png" width="600">
    * 주중/주말 여부에 따라 대여량 추이가 다르다
    * 주중(0~4)에는 출퇴근 시간대의 대여량이 높다
    * 주말(5~5)에는 낮-오후 시간대의 대여량이 높다

## Preprocessing
* 결측치 처리
  * `Temperature`, `Windspeed`, `Dewpoint` 데이터의 경우 nearest interpolation 기법을 사용
  * `Rainfall`, `Snow`의 경우 0으로 결측치 대체
* 연도, 월, 요일 정보를 담은 `Year`, `Month`, `Weekday` 변수 생성
* Standard Scaling 진행

### Model
* LinearRegressor
* XGBoostRegressor
* LightGBMRegressor

Baseline 모델의 R2Score 및 연산 비용을 고려해 LightGBM을 최종 모델로 선택하였습니다.
  
### Optimization
* LightGBM Hyperparameter Tuning (Optuna 프레임워크 사용)
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
* 10-Fold Cross Validation

### Result
|  | Linear | LightGBM | XGBoost | LightGBM Optimized |
| :-: | :-: | :-: | :-: | :-: |
| R2Score | 0.39522 | 0.67232 | 0.69045 | **0.81940** |
| Plot | <img src="https://user-images.githubusercontent.com/63901494/139447416-f6e21634-2449-499f-94f7-cefc62a334a5.png" width="130"> | <img src="https://user-images.githubusercontent.com/63901494/139447698-e906644a-b67a-4969-86ff-d67c72e8d3ff.png" width="130"> | <img src="https://user-images.githubusercontent.com/63901494/139447625-807211f7-ff03-4774-ab7a-79e6dbe311c7.png" width="130"> | <img src="https://user-images.githubusercontent.com/63901494/139278440-acda6362-3f85-4991-9540-bc4c905c6021.png" width="130"> |

>예선 대회 Kaggle 리더보드 1위

## Final Round
주어진 뉴스 데이터의 내용/제목들로부터 특징들을 추출 후, 이를 기반으로 뉴스를 주제별로 분류하였습니다.
<!--
### Data
* 총 6개 카테고리별 각각 4500 개의 뉴스들로 데이터의 균등한 분포 확인
* [AI-Hub 문서요약 텍스트](https://aihub.or.kr/aidata/8054)를 참조하여 각 클래스 별 카테고리 추정<br>0: 문화, 1: IT/과학, 2: 경제, 3: 사회, 4: 스포츠, 5: 정치
  | Title | Abstract |
  | :-: | :-: |
  | <img src="https://user-images.githubusercontent.com/63901494/139452999-1c083dfd-9af4-49cb-b261-c45ad3799c6a.png" width="300"> | <img src="https://user-images.githubusercontent.com/63901494/139453328-d1f43b35-9607-4959-9378-3137a76b0a1d.png" width="300"> |

### Preprocessing
* Komoran 형태소 분석기를 활용해 텍스트 데이터의 형태소 분석 및 품사 태깅
* 의미 파악에 불필요하다고 판단한 조사, 선어말어미, 연결어미, 전성어미, 접미사 등의 불용어 제거
* TF-IDF 알고리즘으로 텍스트 벡터화

### Model
* LSTM
* GRU
* KoBERT

### Optimization
* Finetune KoBERT
* Dropout 추가
* Weight Decay 적용

### Result
<table>
<tr><td align="center">제목 데이터</td><td align="center">요약 데이터</td></tr>
<tr><td>

|  | LSTM | GRU | KoBERT |
| :-: | :-: | :-: | :-: |
| F1-Score |  |  | **0.64** |
| Accuracy |  |  | **0.65** |

</td><td>

|  | LSTM | GRU | 
| :-: | :-: | :-: |
| F1-Score |  |  |
| Accuracy |  |  |

</td></tr>
</table>

>본선 대회 Kaggle 리더보드 1위

## Reference 
* [SKTBrain/Kobert](https://github.com/SKTBrain/KoBERT)
-->
## Members
<table>
  <tr>
    <td align="center"><a href="https://github.com/Taehee-K"><img src="https://user-images.githubusercontent.com/63901494/139446853-32606da5-5534-4e9d-a6fd-6b610c61bbde.jpg" width="100" height="100"><br /><sub><b>김태희</b></sub></td>
    <td align="center"><a href="https://github.com/SK-jeong"><img src="https://user-images.githubusercontent.com/63901494/129582209-1d1d194e-cf3e-48d6-b097-35a7b855a683.jpg" width="100" height="100"><br /><sub><b>정성경</b></sub></td>
    <td align="center"><a href="https://github.com/jyjy318"><img src="https://user-images.githubusercontent.com/63901494/139084437-17d8f084-ee9c-4d20-b52a-e71f57a48991.png" width="100" height="100"><br /><sub><b>문지예</b></sub></td>
    <td align="center"><a href="https://github.com/YuKyeong97"><img src="https://user-images.githubusercontent.com/63901494/139084338-c1ff0768-8258-49d0-9628-66943e958814.png" width="100" height="100"><br /><sub><b>한유경</b></sub></td>
  </tr>
</table>

<!--
## Structure
-->