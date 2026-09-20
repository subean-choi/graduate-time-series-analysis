# 시계열 데이터 분석

---
📖 **Textbook - Introduction to Time Series Forecasting**
**💡 공지**
- 시험 1번
- 프로젝트 1번 (없을 수도 있음)
- PPT는 수업 끝나고 업뎃
---
### 📺 PDF & 실습 코드
> Fundamentals
- 1장. Python 환경
- 2장. What is Time Series Forecasting
- 3장. Time Series as Supervised Learning
> Data PreParation
- 4장. Load and Explore Time Series Data
- 5장. Basic Feature Engineering
- 6장.  Data Visualization
- 7장.  Resampling and Interpolation
- 8장. Power Transforms
- 9장.  Moving Average Smoothing
> Temporal Structure
- 10장. A Gentle Introduction to White Noise
- 11장. A Gentle Introduction to the Random Walk
- 12장. Decompose Time Series Data
- 13장. Use and Remove Trends
- 14장.  Use and Remove Seasonality

---

# 1장. Python 환경

---
### 1.1 Why Python?
> Python은 범용 인터프리터 언어로, R이나 MATLAB보다 배우기 쉽고 가독성이 높습니다.
- 장점
- 연구(R&D)와 실제 운영(Production) 모두에 사용할 수 있음
- 동적 언어로 빠른 프로토타이핑과 대형 응용 프로그램 개발에 유리함
- 머신러닝과 데이터 과학 분야에서 풍부한 라이브러리 지원 덕분에 널리 사용됨
- Python은 데이터 과학자들에게 인기가 높으며, StackOverflow 등에서 항상 상위권에 위치함
- R보다 더 많은 구인 수요가 있으며, 머신러닝 플랫폼으로 자리 잡음
### 1.2 Python Libraries for Time Series
> 시간 시계열 분석에 중요한 Python의 핵심 라이브러리는 Pandas, Statsmodels, scikit-learn입니다.<br>이들은 모두 SciPy 생태계(SciPy Stack) 위에서 작동합니다.
1. **Pandas**
데이터를 불러오고 처리하는 고성능 도구를 제공
- 주요 기능:
- `Series` 객체: 단일 시계열 표현
- 시간 인덱스(DateTime Index) 지원
- 시프트, 래그, 보간 등의 변환(transform)
- 업샘플링 / 다운샘플링 / 집계(resampling) 기능
- 시계열 데이터 분석의 기본 도구로 사용됨
2. **Statsmodels**
통계적 모델링 및 시계열 분석 도구 제공
- 주요 기능:
- 정상성 검정(Augmented Dickey-Fuller Test)
- 자기상관(ACF), 부분 자기상관(PACF) 분석
- AR, MA, ARMA, ARIMA 모델 제공
- 회귀, 추정, 통계 테스트 등 전통적 분석에 적합
3. ** scikit-learn**
머신러닝 알고리즘 및 데이터 전처리 도구 제공
- 주요 기능:
- 데이터 전처리 (스케일링, 결측치 보간)
- 회귀/분류/클러스터링 알고리즘 제공
- TimeSeriesSplit을 통한 시계열 교차 검증 지원

---

# 2장. What is Time Series Forecasting

---
### 2.1 Time Series
- 일반적인 머신러닝 데이터는 순서 없는 관측값들의 집합이지만,
**시계열 데이터(time series)** 는 **시간 순서에 따라 기록된 관측값들의 연속**임.
- 시간은 중요한 변수로, 각 관측값은 과거와 미래의 데이터와 **의존 관계(temporal dependency)** 를 가짐.
- 즉, 시계열은 “시간에 따른 변화”를 다루는 데이터 형태임.
### 2.2 Time Series Nomenclature (용어 정리)
- `t`: 현재 시점
- `t-1`, `t-2`: 과거 시점 (lag)
- `t+1`, `t+2`: 미래 시점 (forecast horizon)
- 시계열 분석에서는 이러한 시간 인덱스를 사용해 데이터를 설명하거나 예측함.
### 2.3 Describing vs. Predicting
- **Describing (분석)**: 시계열의 패턴, 추세, 계절성 등을 이해하는 것 (예: “왜 이런 변화가 생겼는가?”)
- **Predicting (예측)**: 과거 데이터를 기반으로 미래 값을 예측하는 것
- 시계열 분석은 ‘이유(why)’를 찾고, 시계열 예측은 ‘미래(what next)’를 맞히는 데 초점을 둠.
**2.3.1 Time Series Analysis**
- 시계열 분석은 데이터를 설명하는 **통계적 모델**을 만드는 과정
- 주로 데이터의 구조(추세, 계절성 등)를 이해하기 위해 사용됨
- 목표: 표본 데이터에 대한 **수학적 모델을 개발하여 원인 분석**
**2.3.2 Time Series Forecasting**
- 과거 데이터를 이용해 **미래 값을 예측하는 것**
- 분석과 달리, 미래 데이터가 주어지지 않으므로 과거 정보만으로 예측해야 함
- 모델의 성능은 미래 값을 얼마나 잘 맞추는지에 따라 평가됨 (정확도, 신뢰구간 등)
### 2.4 Components of Time Series (구성 요소)
시계열 데이터는 보통 다음 네 가지 요소로 구성됨:
1. **Level**: 기준선 수준 (데이터의 기본 값)
2. **Trend**: 장기적인 증가 또는 감소 경향
3. **Seasonality**: 주기적으로 반복되는 패턴 (예: 계절, 주, 일 단위)
4. **Noise**: 설명되지 않는 무작위 변동
→ 대부분의 시계열은 **Level + Noise**, 경우에 따라 **Trend**와 **Seasonality**를 포함함.
### 2.5 Concerns of Forecasting (예측 시 고려사항)
시계열 예측을 할 때 고려해야 할 주요 질문:
1. **데이터 양**: 충분히 확보 가능한가?
2. **예측 기간**: 단기, 중기, 장기 중 어느 범위를 예측할 것인가?
3. **업데이트 주기**: 예측을 실시간으로 갱신할 수 있는가?
4. **데이터 주기(Frequency)**: 데이터가 초 단위, 일 단위, 월 단위인가?
또한 시계열 데이터는 다음과 같은 전처리가 필요할 수 있음:
- **빈도 조정(Frequency adjustment)**
- **이상치 처리(Outlier handling)**
- **결측치 보간(Missing value interpolation)**
### 2.6 Examples of Time Series Forecasting
시계열 예측 문제의 예시:
- 주식 종가 예측
- 하루 판매량 예측
- 병원 출산율 예측
- 실업률 분기별 예측
- 서버 사용량 예측
- 기름값, 농작물 수확량, 기차 승객 수 등 예측
→ 거의 모든 산업 분야에서 시계열 예측이 활용됨.

---

# 3장. Time Series as Supervised Learning

---
### 시계열 예측과 지도학습의 관계
- **시계열 예측(Time Series Forecasting)** 은
데이터를 **지도학습(Supervised Learning)** 형태로 변환하여 다룰 수 있습니다.
- 이렇게 변환하면
→ **일반적인 머신러닝 알고리즘** (선형/비선형 회귀, 트리, 신경망 등)을
→ **시계열 데이터 예측 문제**에 그대로 적용할 수 있습니다
### 이 장(Chapter 3)의 핵심 학습 내용
1. **슬라이딩 윈도우(Sliding Window)** 개념 이해
- 시계열 데이터를 입력(X)과 출력(y) 형태로 재구성하는 방법
2. **단변량(Univariate)** 시계열
- 한 변수(예: 온도, 주가 등)의 시간 변화 예측
3. **다변량(Multivariate)** 시계열
- 여러 변수(예: 온도 + 습도 + 풍속 등)를 함께 고려한 예측
4. **다단계 예측(Multi-step Forecasting)**
- 한 번에 여러 미래 시점을 예측하는 방법 (예: 내일 + 모레의 값 동시에 예측)
### 3.1 Supervised Machine Learning
- 지도학습은 입력변수(X)와 출력변수(y)가 있는 데이터에서 `Y = f(X)` 형태의 관계를 학습하는 방식
- 새로운 입력값이 주어지면, 학습된 함수 `f`를 이용해 결과값 `y`를 예측
- 예시:


<table header-row="true">
<tr>
<td>X</td>
<td>y</td>
</tr>
<tr>
<td>5</td>
<td>0.9</td>
</tr>
<tr>
<td>4</td>
<td>0.8</td>
</tr>
<tr>
<td>5</td>
<td>1.0</td>
</tr>
</table>


- **Classification**: 출력이 범주형 (예: ‘병 있음/없음’)
- **Regression**: 출력이 실수형 (예: 온도, 가격 등)
 → 시계열 예측은 보통 **회귀(regression)** 문제로 분류


### 3.2 Sliding Window
- 시계열은 시간 순서가 있는 데이터이므로,
- 이전 시점의 값들로 다음 시점의 값을 예측하도록 데이터를 변환할 수 있습니다.
= 이 과정을 **슬라이딩 윈도우(Sliding Window)** 라고 부릅니다.


- 예를 들어 원본 시계열이 다음과 같다면:
<table header-row="true">
<tr>
<td>time</td>
<td>measure</td>
</tr>
<tr>
<td>1</td>
<td>100</td>
</tr>
<tr>
<td>2</td>
<td>110</td>
</tr>
<tr>
<td>3</td>
<td>108</td>
</tr>
<tr>
<td>4</td>
<td>115</td>
</tr>
<tr>
<td>5</td>
<td>120</td>
</tr>
</table>


→ 지도학습 데이터로 변환하면 다음과 같습니다:
<table header-row="true">
<tr>
<td>X</td>
<td>y</td>
</tr>
<tr>
<td>100</td>
<td>110</td>
</tr>
<tr>
<td>110</td>
<td>108</td>
</tr>
<tr>
<td>108</td>
<td>115</td>
</tr>
<tr>
<td>115</td>
<td>120</td>
</tr>
</table>


- 이전 시점(`t`)의 값이 입력(X)
- 다음 시점(`t+1`)의 값이 출력(y)
- 첫 번째 행은 이전 값이 없으므로 제거, 마지막 행은 미래값이 없으므로 제거
→ 이렇게 변환하면 시계열을 일반적인 회귀 데이터로 사용할 수 있게 됩니다.
### 3.3 Sliding Window with Multivariates
- **다변량 시계열(Multivariate Time Series)** 은 한 시점에 여러 변수가 있는 경우입니다.
- 예: 온도(Temperature), 습도(Humidity), 기압(Pressure)
- 예시:
<table header-row="true">

<tr>
<td>time</td>
<td>measure1</td>
<td>measure2</td>
</tr>
<tr>
<td>1</td>
<td>0.2</td>
<td>88</td>
</tr>
<tr>
<td>2</td>
<td>0.5</td>
<td>89</td>
</tr>
<tr>
<td>3</td>
<td>0.7</td>
<td>87</td>
</tr>
<tr>
<td>4</td>
<td>0.4</td>
<td>88</td>
</tr>
<tr>
<td>5</td>
<td>1.0</td>
<td>90</td>
</tr>
</table>
- 이 데이터를 지도학습 형태로 바꾸면:
<table header-row="true">

<tr>
<td>X1</td>
<td>X2</td>
<td>X3</td>
<td>y</td>
</tr>
<tr>
<td>?</td>
<td>?</td>
<td>0.2</td>
<td>88</td>
</tr>
<tr>
<td>0.2</td>
<td>88</td>
<td>0.5</td>
<td>89</td>
</tr>
<tr>
<td>0.5</td>
<td>89</td>
<td>0.7</td>
<td>87</td>
</tr>
<tr>
<td>0.7</td>
<td>87</td>
<td>0.4</td>
<td>88</td>
</tr>
</table>
→ 즉, 이전 시점의 `measure1`, `measure2` 값들을 이용해 다음 시점의 `measure2`를 예측
- 이 방식을 확장하면 여러 변수를 동시에 예측하는 **multi-output forecasting** 도 가능
- 예를 들어 `measure1`과 `measure2`를 동시에 예측할 수도 있습니다.
<table header-row="true">
<tr>
<td>X1</td>
<td>X2</td>
<td>y1</td>
<td>y2</td>
</tr>
<tr>
<td>0.2</td>
<td>88</td>
<td>0.5</td>
<td>89</td>
</tr>
<tr>
<td>0.5</td>
<td>89</td>
<td>0.7</td>
<td>87</td>
</tr>
<tr>
<td>0.7</td>
<td>87</td>
<td>0.4</td>
<td>88</td>
</tr>
</table>
→ 이는 **다변량 + 다출력(multivariate multi-output)** 예측 형태입니다.
### 3.4 Sliding Window with Multiple Steps
- **Multi-step forecasting**은 한 번에 여러 시점의 미래를 예측하는 것입니다.
- **One-step Forecast**: 다음 시점(t+1)만 예측
- **Multi-step Forecast**: 두 개 이상 미래 시점(t+1, t+2, …) 예측


- 예시 데이터:
<table header-row="true">
<tr>
<td>time</td>
<td>measure</td>
</tr>
<tr>
<td>1</td>
<td>100</td>
</tr>
<tr>
<td>2</td>
<td>110</td>
</tr>
<tr>
<td>3</td>
<td>108</td>
</tr>
<tr>
<td>4</td>
<td>115</td>
</tr>
<tr>
<td>5</td>
<td>120</td>
</tr>
</table>


→ 2-step 예측 형태로 변환하면:
<table header-row="true">

<tr>
<td>X1</td>
<td>y1</td>
<td>y2</td>
</tr>
<tr>
<td>100</td>
<td>110</td>
<td>108</td>
</tr>
<tr>
<td>110</td>
<td>108</td>
<td>115</td>
</tr>
<tr>
<td>108</td>
<td>115</td>
<td>120</td>
</tr>
</table>


- 즉, 현재값(X1)으로 다음 두 시점(y1, y2)을 동시에 예측하는 방식입니다.
- 이 경우 첫 번째 행과 마지막 행은 예측에 사용할 수 없으므로 제거합니다.
- 모델이 한 번에 여러 시점을 예측해야 하므로, 입력 정보의 양과 모델의 복잡성이 함께 늘어납니다.

---

# 4장. Load and Explore Time Series Data

---
### 학습 목표
- CSV 파일에서 시계열 데이터를 불러오기
- 날짜 인덱스를 활용해 탐색 및 조회
- 기본 통계량 계산 및 해석
### 4.1 Daily Female Births Dataset
- 사용 데이터: `daily-total-female-births.csv`
- 데이터 내용: 1959년 한 해 동안 캘리포니아에서 **하루마다 기록된 여성 출생 수**
- 데이터 구성:
- `Date`: 날짜 (1959-01-01 \~ 1959-12-31)
- `Births`: 여성 출생 수
- 데이터 크기: 총 365개 (1년치 일별 데이터)
- 데이터 형식: CSV
- 목적: Pandas의 시계열 처리 기능 실습
### 4.2 Load Time Series Data
**코드 예시**
```python
# load dataset using read_csv()
from pandas import read_csv

series = read_csv(
    'daily-total-female-births.csv',
    header=0,          # 첫 번째 행을 열 이름으로 사용
    index_col=0,       # 첫 번째 열을 인덱스로 지정
    parse_dates=True,  # 인덱스를 날짜(datetime)로 변환
    squeeze=True       # 단일 컬럼일 경우 Series로 반환
)

print(type(series))
print(series.head())
```
**출력 예시**
```bash
<class 'pandas.core.series.Series'>
Date
1959-01-01    35
1959-01-02    32
1959-01-03    30
1959-01-04    31
1959-01-05    44
Name: Births, dtype: int64
```
### 4.3 Exploring Time Series Data
**4.3.1 Peek at the Data**
> 목적: 불러온 데이터가 의도대로 로드됐는지 빠르게 확인<br>핵심: head(n), tail(n)으로 앞/뒤 일부 행만 미리 보기기<br>포인트: 날짜가 인덱스로 잡혔는지, 값의 dtype이 맞는지, 이상치가 눈에 띄는지 점검
- 코드 예시
```python
# summarize first few lines of a file
from pandas import read_csv
series = read_csv('daily-total-female-births.csv',
                  header=0, index_col=0, parse_dates=True, squeeze=True)
print(series.head(10))
```
- 출력 예시
```bash
Date
1959-01-01    35
1959-01-02    32
1959-01-03    30
1959-01-04    31
1959-01-05    44
1959-01-06    29
1959-01-07    45
1959-01-08    43
1959-01-09    38
1959-01-10    27
Name: Births, dtype: int64
```
**4.3.2 Number of Observations**
> 목적: 관측치 개수(데이터 길이)를 확인
핵심: Series.size 또는 len(Series) 사용
포인트: 기대한 길이(예: 365일)와 실제 길이가 다른지로 누락 여부를 빠르게 진단
- 코드 예시
```python
# summarize the dimensions of a time series
from pandas import read_csv
series = read_csv('daily-total-female-births.csv',
                  header=0, index_col=0, parse_dates=True, squeeze=True)
print(series.size)
```
- 출력 예시
```plain text
365
```
**4.3.3 Querying By Time**
> 목적: 시간 인덱스를 활용해 특정 기간의 데이터만 선택
핵심: 문자열 슬라이싱으로 조회(예: series['1959-01'], series['1959-01-10':'1959-01-20'])
포인트: 인덱스가 datetime이어야 합니다(parse_dates, index_col 설정). 월·연 단위 조회가 직관적
- 코드 예시
```python
# query a dataset using a date-time index
from pandas import read_csv
series = read_csv('daily-total-female-births.csv',
                  header=0, index_col=0, parse_dates=True, squeeze=True)
print(series['1959-01'])
```
- 출력 예시
```bash
Date
1959-01-01    35
1959-01-02    32
1959-01-03    30
1959-01-04    31
1959-01-05    44
1959-01-06    29
1959-01-07    45
1959-01-08    43
1959-01-09    38
1959-01-10    27
1959-01-11    38
1959-01-12    33
1959-01-13    55
1959-01-14    47
1959-01-15    45
1959-01-16    37
1959-01-17    50
1959-01-18    43
1959-01-19    41
1959-01-20    52
1959-01-21    34
1959-01-22    53
1959-01-23    39
1959-01-24    32
1959-01-25    37
1959-01-26    43
1959-01-27    39
1959-01-28    35
1959-01-29    44
1959-01-30    38
1959-01-31    24
Name: Births, dtype: int64
```
**4.3.4 Descriptive Statistics**
> 목적: 분포와 범위를 한 번에 파악
핵심: describe()로 count, mean, std, min, 25/50/75%, max를 출력
포인트: 평균·중앙값 차이로 비대칭 여부, min/max로 이상치 가능성, 표준편차로 변동성 규모를 가늠
- 코드 예시
```python
# calculate descriptive statistics
from pandas import read_csv
series = read_csv('daily-total-female-births.csv',
                  header=0, index_col=0, parse_dates=True, squeeze=True)
print(series.describe())
```
- 출력 예시
```bash
count    365.000000
mean      41.980822
std        7.348257
min       23.000000
25%       37.000000
50%       42.000000
75%       46.000000
max       73.000000
Name: Births, dtype: float64
```
### 4.4 Summary
- Pandas의 `read_csv()`로 시계열 데이터를 쉽게 불러올 수 있음
- `head()`로 데이터의 앞부분을 확인 가능
- `size`로 전체 관측치 개수 확인
- `series['YYYY-MM']` 형식으로 특정 기간 데이터 조회 가능
- `describe()`로 평균, 표준편차, 최소·최대값 등 기본 통계량 요약 가능
**핵심 학습 내용**
- 시계열 데이터를 Pandas Series로 불러오기
- 날짜 인덱스를 기반으로 탐색 및 쿼리 수행
- 통계 요약으로 데이터 분포 이해

---

# 5장. Basic Feature Engineering

---
### 5.1 Feature Engineering for Time Series
- **핵심 개념:**
- 시계열 데이터는 원래 입력과 출력이 명확히 구분되지 않음
- 따라서 머신러닝 모델이 예측할 수 있도록 데이터를 ‘입력–출력 쌍’ 형태로 다시 구성해야 함
- 변환 전 데이터
```bash
time 1, value 1
time 2, value 2
time 3, value 3
```
- 변환 후 데이터
```bash
input 1, output 1
input 2, output 2
input 3, output 3
```
- 목적: 과거 값(input)을 이용해 미래 값(output)을 예측할 수 있는 **지도학습용 데이터셋**으로 재구성
- 주요 피처 종류
- **Date-Time Features**: 날짜/시간 구성요소 (월, 일, 시 등)
- **Lag Features**: 과거 시점의 값
- **Window Features**: 일정 기간(윈도우)의 요약 통계량 (평균, 최소, 최대 등)
### 5.2 Goal of Feature Engineering
- **목표:** 입력(X)과 출력(y)의 관계를 강하고 단순하게 만들어, 모델이 학습하기 쉽게 하는 것
- **중요 포인트:**
- 시계열에는 명확한 입력·출력 개념이 없으므로 우리가 정의해야 함
- 복잡한 관계를 단순화하여 모델 성능을 높이고 해석을 용이하게 함
- 다양한 피처를 시도해보고 모델 성능으로 좋은 피처를 선택
### 5.3 Minimum Daily Temperatures Dataset
- **사용 데이터:** `daily-minimum-temperatures.csv`
- **내용:** 1981–1990년, 호주 멜버른(Melbourne)의 일별 최저 기온
- **구성:**
- Date: 날짜
- Temperature: 최저기온(℃)
- **용도:** 이후 예제에서 모든 피처 엔지니어링 실습용
### 5.4 Date Time Features
- 코드 예시
```python
# create date time features of a dataset
from pandas import read_csv
from pandas import DataFrame

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

dataframe = DataFrame()
dataframe['month'] = [series.index[i].month for i in range(len(series))]
dataframe['day'] = [series.index[i].day for i in range(len(series))]
dataframe['temperature'] = [series[i] for i in range(len(series))]

print(dataframe.head(5))
```
- 출력 예시
```bash
   month  day  temperature
0      1    1         20.7
1      1    2         17.9
2      1    3         18.8
3      1    4         14.6
4      1    5         15.8
```
- **설명:**
날짜 인덱스에서 월(month)과 일(day)을 추출하여 각각을 새로운 열로 추가
→ 모델이 ‘계절적 요인’(예: 여름, 겨울)을 학습할 수 있게 도움
### 5.5 Lag Features
- 코드 예시 (lag=1)
```python
# create a lag feature
from pandas import read_csv, DataFrame, concat

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)
temps = DataFrame(series.values)
dataframe = concat([temps.shift(1), temps], axis=1)
dataframe.columns = ['t', 't+1']
print(dataframe.head(5))
```
- 출력 예시
```bash
      t   t+1
0   NaN  20.7
1  20.7  17.9
2  17.9  18.8
3  18.8  14.6
4  14.6  15.8
```
- 설명:
이전 시점의 값을 현재 시점의 입력으로 추가
→ 예: `t`(하루 전)로 `t+1`(오늘)을 예측
- **확장 예시 (lag=3)**
```python
# include last 3 observed values
from pandas import read_csv, DataFrame, concat
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)
temps = DataFrame(series.values)
dataframe = concat([temps.shift(3), temps.shift(2), temps.shift(1), temps], axis=1)
dataframe.columns = ['t-2', 't-1', 't', 't+1']
print(dataframe.head(5))
```
- **출력 예시**
```bash
     t-2   t-1     t   t+1
0    NaN   NaN   NaN  20.7
1    NaN   NaN  20.7  17.9
2    NaN  20.7  17.9  18.8
3   20.7  17.9  18.8  14.6
4   17.9  18.8  14.6  15.8
```
### 5.6 Rolling Window Statistics
- 코드 예시
```python
# create a rolling mean feature
from pandas import read_csv, DataFrame, concat
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)
temps = DataFrame(series.values)
shifted = temps.shift(1)
window = shifted.rolling(window=2)
means = window.mean()
dataframe = concat([means, temps], axis=1)
dataframe.columns = ['mean(t-1,t)', 't+1']
print(dataframe.head(5))
```
- 출력 예시
```bash
   mean(t-1,t)   t+1
0          NaN  20.7
1          NaN  17.9
2        19.30  18.8
3        18.35  14.6
4        16.70  15.8
```
- 설명:
최근 두 시점의 평균을 계산하여 입력으로 사용 
→ 최근 w개 값의 요약 통계(평균 등)를 계산해 피처로 추가한다. 
→ 단순한 이동평균(rolling mean) 피처 생성
### 5.7 Expanding Window Statistics
- 코드 예시
```python
# create expanding window features
from pandas import read_csv, DataFrame, concat
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)
temps = DataFrame(series.values)
window = temps.expanding()
dataframe = concat([window.min(), window.mean(), window.max(), temps.shift(-1)], axis=1)
dataframe.columns = ['min', 'mean', 'max', 't+1']
print(dataframe.head(5))
```
- 출력 예시
```bash
    min      mean   max   t+1
0  20.7  20.700000  20.7  17.9
1  17.9  19.300000  20.7  18.8
2  17.9  19.133333  20.7  14.6
3  14.6  18.000000  20.7  15.8
4  14.6  17.560000  20.7  15.8
```
- 설명:
지금까지의 모든 과거 데이터를 누적하여 최소, 평균, 최대값을 계산
→ ‘점점 커지는 누적 윈도우’를 활용
### 5.8 Summary
- 시계열 데이터는 지도학습 형태로 변환되어야 함
- 피처 엔지니어링의 목적은 모델이 쉽게 학습할 수 있도록 입력과 출력의 관계를 단순화하는 것
- 세 가지 주요 피처 생성법
1. **Date-Time Features** — 월, 일, 요일 등 시간 구성요소
2. **Lag Features** — 과거 시점의 값을 입력으로 사용
3. **Window Features** — 일정 구간의 요약 통계(평균, 최소, 최대 등)
**핵심 학습 내용**
- 시계열 데이터를 지도학습용 데이터셋으로 변환
- 날짜·시간 기반, 지연 기반, 윈도우 기반 피처 생성
- Pandas의 `shift()`, `rolling()`, `expanding()` 함수 활용

---

# 6장.  Data Visualization

---
### 6.1 시계열 시각화 (Time Series Visualization)
> 시계열 데이터의 시간적 구조(추세, 주기, 계절성 등)를 파악하고 적절한 예측 모델을 선택하기 위해 시각화는 매우 중요한 역할
1. **라인 플롯 (Line Plots)**
2. 히스토그램 및 밀도 플롯 (Histograms and Density Plots)
3. 박스 및 위스커 플롯 (Box and Whisker Plots)
4. 히트맵 (Heat Maps)
5. 지연 플롯 또는 산점도 (Lag Plots or Scatter Plots)
6. 자기상관 플롯 (Autocorrelation Plots)
### 6.2 일일 최저 기온 데이터셋 (Minimum Daily Temperatures Dataset)
이 튜토리얼에서는 예제로 '일일 최저 기온 데이터셋'을 사용
- **내용**: 호주 멜버른의 10년간(1981-1990) 일일 최저 기온
- **파일명**: `daily-minimum-temperatures.csv`
### 6.3 라인 플롯 (Line Plot)
- 시계열 데이터를 시각화하는 가장 첫 번째이자 가장 대중적인 방법
- **X축에 시간**을, **Y축에 관측값**을 두어 데이터를 선으로 연결해 보여줌
- **Line Plot 예시**
```python
# create a line plot
from pandas import read_csv
from matplotlib import pyplot

# 'daily-minimum-temperatures.csv' 파일을 읽어옵니다.
# header=0: 첫 번째 줄을 헤더로 사용
# index_col=0: 첫 번째 열을 인덱스로 사용
# parse_dates=True: 인덱스 열을 날짜/시간 형식으로 변환
# squeeze=True: 데이터 열이 하나일 경우 Series 객체로 변환
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

# 데이터를 플롯(그래프)으로 만듭니다.
series.plot()

# 화면에 그래프를 보여줍니다.
pyplot.show()
```
[image omitted: temporary Notion asset]
- **Dot Plot **
- 기존의 라인 플롯은 모든 점을 선으로 연결했지만, 데이터 포인트가 많으면 선이 겹쳐 보입니다. 
- **점 플롯**은 선을 제거하고 각 데이터를 점으로만 표시하여 시각적 혼잡함을 줄여줍니다. 
- 전체적인 추세는 유지하면서 개별 데이터 포인트를 더 명확하게 볼 수 있습니다.
- **코드 설명**: `plot()` 함수에 `style='k.'` 옵션을 추가하면 검은색('k') 점('.') 스타일로 그래프가 그려집니다.
```python
# create a dot plot
from pandas import read_csv
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

# 'k.' 스타일을 적용하여 점 플롯 생성
series.plot(style='k.')
pyplot.show()
```
[image omitted: temporary Notion asset]
- **연도별 누적 라인 플롯 (Stacked Line Plots by Year)**
- 10년 치 데이터를 한 번에 보면 장기적인 계절성은 보이지만, 특정 연도의 패턴이나 다른 해와의 차이점을 비교하기는 어렵습니다. 
- 데이터를 **연도별로 그룹화**하여 각 해의 플롯을 위아래로 쌓아 그리면, 연도별 패턴을 한눈에 비교하고 이상치(예: 유난히 더웠던 해)를 쉽게 찾아낼 수 있습니다.
- **코드 설명**: 
- `series.groupby(Grouper(freq='A'))`는 일별 데이터를 연도('A': Annual) 기준으로 그룹화하는 핵심 부분입니다.
-  이렇게 나뉜 각 그룹(연도)을 `DataFrame`의 열로 저장한 뒤 `subplots=True` 옵션으로 각각의 플롯을 그립니다.
```python
# create stacked line plots
from pandas import read_csv
from pandas import DataFrame
from pandas import Grouper
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

groups = series.groupby(Grouper(freq='A'))
years = DataFrame()

for name, group in groups:
    years[name.year] = group.values

years.plot(subplots=True, legend=False)
pyplot.show()
```
[image omitted: temporary Notion asset]
### 6.4 히스토그램 및 밀도 플롯 (Histogram and Density Plots)
- 이 시각화 기법들은 시간의 흐름을 무시하고, **데이터 값 자체의 분포**에 집중합니다. 
- 즉, "어떤 온도 값이 얼마나 자주 나타나는가?"를 보여줍니다. 
- 데이터가 특정 분포(예: 정규 분포)를 따르는지 확인하는 데 매우 유용합니다.
1. **히스토그램 (Histogram)**
- **히스토그램**은 전체 온도 데이터를 몇 개의 구간(예: 0\~2도, 2\~4도...)으로 나눈 뒤, 각 구간에 몇 개의 데이터가 포함되는지를 막대그래프로 나타낸 것입니다. 
- 이 그래프를 통해 데이터가 어디에 집중되어 있는지, 분포가 대칭적인지 등을 직관적으로 파악할 수 있습니다.
```python
# create a histogram plot
from pandas import read_csv
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

series.hist()
pyplot.show()
```
[image omitted: temporary Notion asset]
- **해석**: 아래 히스토그램을 보면 최저 기온이 약 10\~12도 근처에서 가장 빈번하게 나타나며, 전체적으로 종 모양(bell curve)과 비슷한 가우시안 분포를 띄는 것을 알 수 있습니다.
1. **밀도 플롯 (Density Plot)**
- **밀도 플롯**은 히스토그램의 각진 막대를 부드러운 곡선으로 만들어 데이터의 분포를 더 매끄럽게 보여주는 방법입니다. 
- 히스토그램보다 분포의 형태를 더 명확하게 요약해주며, 비대칭성이나 봉우리의 뾰족한 정도를 파악하기 좋습니다.
```python
# create a density plot
from pandas import read_csv
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

series.plot(kind='kde')
pyplot.show()
```
[image omitted: temporary Notion asset]
### 6.5 박스 및 위스커 플롯 (Box and Whisker Plots by Interval)
- 박스 플롯(Box Plot)은 데이터의 분포를 특정 구간(연도, 월 등)별로 요약하여 보여주는 시각화 방법
- 데이터의 중앙값(median), 사분위수(quartiles), 이상치(outliers)를 한눈에 파악할 수 있어 구간별 데이터 분포를 비교하는 데 매우 효과적
1. **연도별 박스 플롯 (Yearly Box Plots)**
- 10년 치 데이터를 **연도별로 그룹화**하여 각 해의 온도 분포를 나란히 비교
-  이를 통해 연도별 기온의 변화 추세, 변동성의 크기, 이상 기후 등을 시각적으로 확인
- **코드 설명**: 앞서 사용했던 `Grouper(freq='A')`를 이용해 데이터를 연도별로 그룹화하고, 이를 `boxplot()` 함수로 시각화
```python
# create a boxplot of yearly data
from pandas import read_csv
from pandas import DataFrame
from pandas import Grouper
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

groups = series.groupby(Grouper(freq='A'))
years = DataFrame()

for name, group in groups:
    years[name.year] = group.values

years.boxplot()
pyplot.show()
```
[image omitted: temporary Notion asset]
1. **월별 박스 플롯 (Monthly Box Plots)**
- 특정 연도(여기서는 1990년)의 데이터를 **월별로 그룹화**하여 12개의 박스 플롯을 그림
-  이를 통해 1년 동안의 계절적 온도 변화 패턴을 명확하게 볼 수 있음
- **코드 설명**: 1990년 데이터(`series['1990']`)를 선택한 후, `Grouper(freq='M')`을 사용해 월('M': Month-end) 기준으로 그룹화하여 시각화
```python
# create a boxplot of monthly data
from pandas import read_csv
from pandas import DataFrame
from pandas import Grouper
from matplotlib import pyplot
from pandas import concat

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

one_year = series['1990']
groups = one_year.groupby(Grouper(freq='M'))
months = concat([DataFrame(x[1].values) for x in groups], axis=1)
months = DataFrame(months)
months.columns = range(1,13)

months.boxplot()
pyplot.show()
```
[image omitted: temporary Notion asset]
### 6.6 히트맵 (Heat Maps)
- **히트맵**은 숫자 데이터를 색상으로 변환하여 매트릭스(행렬) 형태로 보여주는 시각화 기법
-  온도는 색깔로 표현되며, 보통 따뜻한 색(붉은색/노란색)은 높은 값을, 차가운 색(푸른색/녹색)은 낮은 값을 나타냄
-  시간의 흐름에 따른 값의 변화를 색상 패턴으로 직관적으로 이해할 수 있음
1. **연도별 히트맵 (Yearly Heat Map)**
- 10년 치 전체 데이터에 대한 히트맵
- 각 **행은 연도**를, 열은 해당 연도의 일(1일\~365일)을 나타냄
```python
# create a heat map of yearly data
from pandas import read_csv
from pandas import DataFrame
from pandas import Grouper
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

groups = series.groupby(Grouper(freq='A'))
years = DataFrame()

for name, group in groups:
    years[name.year] = group.values

years = years.T
pyplot.matshow(years, interpolation=None, aspect='auto')
pyplot.show()
```
[image omitted: temporary Notion asset]
**해석**: 
- 매년 반복되는 뚜렷한 계절 패턴을 볼 수 있음 
- 연초와 연말(여름)은 따뜻한 색이, 연중(겨울, 약 150\~250일 사이)에는 차가운 파란색이 띠를 형성하고 있음
-  이를 통해 10년간 계절성이 일정하게 유지되었음을 알 수 있음
1. **월별 히트맵 (Monthly Heat Map)**
- 특정 연도(1990년)에 대해 더 상세하게 표현한 히트맵
-  행은 월(1\~12월)을, 열은 일(1일\~31일)을 나타냄
```python
# create a heat map of monthly data
from pandas import read_csv
from pandas import DataFrame
from pandas import Grouper
from matplotlib import pyplot
from pandas import concat

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

one_year = series['1990']
groups = one_year.groupby(Grouper(freq='M'))
months = concat([DataFrame(x[1].values) for x in groups], axis=1)
months = DataFrame(months)
months.columns = range(1,13)

pyplot.matshow(months, interpolation=None, aspect='auto')
pyplot.show()
```
[image omitted: temporary Notion asset]
### 6.7 지연 산점도 (Lag Scatter Plots)
- 지연(Lag)이란 시계열 데이터에서 현재 시점(t)으로부터 과거로 얼마나 떨어져 있는지를 나타내는 값
- 예를 들어, 'lag 1'은 바로 이전 시점(t−1)의 데이터를 의미
- **지연 산점도**는 현재 값(t)과 과거 값(t−1, t−2 등) 사이의 관계를 시각화하여 보여주는 방법
 
**해석 방법**:
- 점이 **왼쪽 아래에서 오른쪽 위**로 대각선 형태로 모이면 **양의 상관관계** <br>(어제의 온도가 높으면 오늘의 온도도 높을 가능성이 큼)
- 점이 **왼쪽 위에서 오른쪽 아래**로 모이면 **음의 상관관계**
- 점이 뚜렷한 패턴 없이 흩어져 있으면 상관관계가 약하거나 없음
1. **기본 지연 산점도 (Lag 1 Plot)**
- 가장 기본적으로 현재 시점(t)의 값과 바로 이전 시점(t+1 또는 t−1)의 값을 비교
```python
# create a scatter plot
from pandas import read_csv
from matplotlib import pyplot
from pandas.plotting import lag_plot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

lag_plot(series)
pyplot.show()
```
[image omitted: temporary Notion asset]
1. **다중 지연 산점도 (Multiple Lag Scatter Plots)**
- 여러 지연 값(예: 1일 전, 2일 전, ..., 7일 전)에 대한 산점도를 한 번에 그려서, 시간 차이에 따라 상관관계가 어떻게 변하는지 확인 가능
```python
# create multiple scatter plots
from pandas import read_csv
from pandas import DataFrame
from pandas import concat
from matplotlib import pyplot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

values = DataFrame(series.values)
lags = 7
columns = [values]
for i in range(1, (lags + 1)):
    columns.append(values.shift(i))
dataframe = concat(columns, axis=1)
columns = ['t']
for i in range(1, (lags + 1)):
    columns.append('t-' + str(i))
dataframe.columns = columns

pyplot.figure(1)
for i in range(1, (lags + 1)):
    ax = pyplot.subplot(240 + i)
    ax.set_title('t vs t-' + str(i))
    pyplot.scatter(x=dataframe['t'].values, y=dataframe['t-' + str(i)].values)
pyplot.show()
```
[image omitted: temporary Notion asset]
**해석**: 아래 그래프를 보면, 바로 전날(t vs t-1)의 상관관계가 가장 강하고, 시간이 멀어질수록 점들이 점차 흩어지며 상관관계가 약해지는 것을 볼 수 있음
### <br>6.8 자기상관 플롯 (Autocorrelation Plots)
- 자기상관(Autocorrelation)은 지연 산점도에서 본 관계를 통계적으로 수치화한 것
-  즉, 현재 데이터와 특정 시간만큼 지연된 과거 데이터 사이의 **상관계수**를 계산한 값
- 자기상관 플롯은 각 지연(Lag)에 대한 상관계수를 그래프로 보여줍니다.
```python
# create an autocorrelation plot
from pandas import read_csv
from matplotlib import pyplot
from pandas.plotting import autocorrelation_plot

series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)

autocorrelation_plot(series)
pyplot.show()
```
[image omitted: temporary Notion asset]
- **해석**:
- **X축**은 지연(Lag), **Y축**은 상관계수(-1에서 1 사이)를 나타냄
- 상관계수가 1에 가까우면 강한 양의 상관관계, -1에 가까우면 강한 음의 상관관계를 의미
- **점선**으로 표시된 영역은 통계적 유의성 임계값으로, 막대가 이 영역을 벗어나면 해당 지연 값과의 상관관계가 통계적으로 의미가 있다고 봄
- 아래 그래프처럼 사인파(sine wave) 형태의 패턴이 나타나는 것은 데이터에 강한 **계절성**이 존재함을 의미

---

# 7장.  Resampling and Interpolation

---

이 장에서는 시계열 데이터의 시간 간격(frequency)을 조절하는 **리샘플링**과, 이 과정에서 발생하는 빈 데이터를 채우는 **보간**에 대해 다룸

### **7.1 리샘플링 (Resampling)**
= 리샘플링은 시계열 데이터의 관측 빈도를 변경하는 과정 두 가지 주요 유형:
- **업샘플링 (Upsampling)**: 데이터의 빈도를 높이는 것 (예: 월별 → 일별 데이터)
-  이 경우 새로운 데이터를 "만들어내야" 하며, 주로 **보간(Interpolation)** 기법이 사용
- **다운샘플링 (Downsampling)**: 데이터의 빈도를 낮추는 것 (예: 일별 → 월별 데이터)
-  이 경우 기존 데이터를 요약(예: 평균, 합계)하는 과정이 필요
리샘플링은 **예측하려는 시간 단위와 데이터의 단위를 맞추거나(Problem Framing)**, 새로운 분석 피처를 생성(Feature Engineering)하기 위해 사용
### **7.2 샴푸 판매량 데이터셋 (Shampoo Sales Dataset)**
이 장에서는 3년간의 월별 샴푸 판매량 데이터를 예제로 사용
### **7.3 업샘플링 (Upsampling Data)**
> 월별 판매량 데이터를 일별 데이터로 업샘플링하는 과정
1. **빈도 변경**: `resample('D')` 함수를 사용해 월별 데이터를 일별 데이터로 변
- 기존 데이터가 없는 날짜는 `NaN`(Not a Number)으로 채워짐
```python
# upsample to daily intervals
from pandas import read_csv
from pandas import datetime

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True, date_parser=parser)
upsampled = series.resample('D').mean()
print(upsampled.head(32))
```
```bash
 Month
 1901-01-01 266.0
 1901-01-02 NaN
 1901-01-03 NaN
 1901-01-04 NaN
 1901-01-05 NaN
 1901-01-06 NaN
 1901-01-07 NaN
 1901-01-08 NaN
 1901-01-09 NaN
 1901-01-10 NaN
 1901-01-11 NaN
 1901-01-12 NaN
 1901-01-13 NaN
 1901-01-14 NaN
 1901-01-15 NaN
 1901-01-16 NaN
 1901-01-17 NaN
 1901-01-18 NaN
 1901-01-19 NaN
 1901-01-20 NaN
 1901-01-21 NaN
 1901-01-22 NaN
 1901-01-23 NaN
 1901-01-24 NaN
 1901-01-25 NaN
 1901-01-26 NaN
 1901-01-27 NaN
 1901-01-28 NaN
 1901-01-29 NaN
 1901-01-30 NaN
 1901-01-31 NaN
 1901-02-01 145.9
 Freq:D,Name:Sales,dtype:float64
```
1. **결측치 보간 (Interpolation)**: `NaN`으로 채워진 값을 채우기 위해 `interpolate()` 함수를 사용
- **선형 보간 (Linear Interpolation)**: 두 개의 기존 데이터 포인트를 직선으로 연결하여 그 사이의 값을 채웁니다. 가장 간단하고 기본적인 방법
```python
# upsample to daily intervals with linear interpolation
from pandas import read_csv
from pandas import datetime
from matplotlib import pyplot

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True, date_parser=parser)
upsampled = series.resample('D').mean()
interpolated = upsampled.interpolate(method='linear')
print(interpolated.head(32))
interpolated.plot()
pyplot.show()
```
```bash
Month
 1901-01-01 266.000000
 1901-01-02 262.125806
 1901-01-03 258.251613
 1901-01-04 254.377419
 1901-01-05 250.503226
 1901-01-06 246.629032
 1901-01-07 242.754839
 1901-01-08 238.880645
 1901-01-09 235.006452
 1901-01-10 231.132258
 1901-01-11 227.258065
 1901-01-12 223.383871
 1901-01-13 219.509677
 1901-01-14 215.635484
 1901-01-15 211.761290
 1901-01-16 207.887097
 1901-01-17 204.012903
 1901-01-18 200.138710
 1901-01-19 196.264516
 1901-01-20 192.390323
 1901-01-21 188.516129
 1901-01-22 184.641935
 1901-01-23 180.767742
 1901-01-24 176.893548
 1901-01-25 173.019355
 1901-01-26 169.145161
 1901-01-27 165.270968
 1901-01-28 161.396774
 1901-01-29 157.522581
 1901-01-30 153.648387
 1901-01-31 149.774194
 1901-02-01 145.900000
 Freq: D, Name: Sales, dtype: float64
```
[image omitted: temporary Notion asset]
- **스플라인 보간 (Spline Interpolation)**: 다항식 곡선을 사용하여 데이터를 연결
- 선형 보간보다 더 부드러운 곡선 형태의 데이터를 생성하여 자연스러운 추세를 보일 수 있음
```python
# upsample to daily intervals with spline interpolation
from pandas import read_csv
from pandas import datetime
from matplotlib import pyplot

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True, date_parser=parser)
upsampled = series.resample('D').mean()
interpolated = upsampled.interpolate(method='spline', order=2)
print(interpolated.head(32))
interpolated.plot()
pyplot.show()
```
```python
Month
 1901-01-01 266.000000
 1901-01-02 258.630160
 1901-01-03 251.560886
 1901-01-04 244.720748
 1901-01-05 238.109746
 1901-01-06 231.727880
 1901-01-07 225.575149
 1901-01-08 219.651553
 1901-01-09 213.957094
 1901-01-10 208.491770
 1901-01-11 203.255582
 1901-01-12 198.248529
 1901-01-13 193.470612
 1901-01-14 188.921831
 1901-01-15 184.602185
 1901-01-16 180.511676
 1901-01-17 176.650301
 1901-01-18 173.018063
 1901-01-19 169.614960
 1901-01-20 166.440993
 1901-01-21 163.496161
 1901-01-22 160.780465
 1901-01-23 158.293905
 1901-01-24 156.036481
 1901-01-25 154.008192
 1901-01-26 152.209039
 1901-01-27 150.639021
 1901-01-28 149.298139
 1901-01-29 148.186393
 1901-01-30 147.303783
 1901-01-31 146.650308
 1901-02-01 145.900000
 Freq: D, Name: Sales, dtype: float64
```
[image omitted: temporary Notion asset]
### 7.4 다운샘플링 (Downsampling Data)
- 다운샘플링은 데이터의 빈도를 낮추는 과정 (예: 월별 → 분기별 또는 연도별)
- 이 과정은 기존 데이터를 더 큰 시간 단위로 **그룹화**하고, 각 그룹을 대표하는 하나의 값으로 요약(aggregation)하는 방식으로 이루어짐
1. **분기별 다운샘플링 (Quarterly Downsampling)**
- 월별 판매량 데이터를 분기별 평균 판매량으로 변환
- `resample('Q')` 코드는 데이터를 분기(Quarter)별로 그룹화하며, `.mean()`을 통해 각 분기의 평균값을 계산
```python
# downsample to quarterly intervals
from pandas import read_csv
from pandas import datetime

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True, date_parser=parser)
quarterly_mean_sales = series.resample('Q').mean()
print(quarterly_mean_sales.head())
quarterly_mean_sales.plot()
pyplot.show()
```
```python
 Month
 1901-03-31 198.333333
 1901-06-30 156.033333
 1901-09-30 216.366667
 1901-12-31 215.100000
 1902-03-31 184.633333
 Freq: Q-DEC, Name: Sales, dtype: float64
```
[image omitted: temporary Notion asset]
1. **연도별 다운샘플링 (Yearly Downsampling)**
- 월별 데이터를 연도별 총 판매량으로 변환
-  `resample('A')` 코드는 데이터를 연도(Annual)별로 그룹화하고, `.sum()`을 통해 각 연도의 판매량 합계를 계산
```python
# downsample to yearly intervals
from pandas import read_csv
from pandas import datetime
from matplotlib import pyplot

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True, date_parser=parser)
yearly_mean_sales = series.resample('A').sum()
print(yearly_mean_sales.head())
yearly_mean_sales.plot()
pyplot.show()
```
[image omitted: temporary Notion asset]

---

# 8장. Power Transforms

---

이 장에서는 시계열 데이터의 추세를 제거하거나 분산을 안정시키는 등, 예측 모델의 성능을 높이기 위해 데이터를 수학적으로 변환하는 **파워 변환**에 대해 다룸

### **8.1 항공 승객 데이터셋 (Airline Passengers Dataset)**
- 이 장에서는 시간 흐름에 따라 평균과 분산이 모두 증가하는 추세를 보이는 '월별 국제 항공 승객 수' 데이터를 예제로 사용
- 이러한 데이터는 불안정(non-stationary)하여 모델링하기 어려움
```python
# load and plot a time series
 from pandas import read_csv
 from matplotlib import pyplot
 series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True,
 squeeze=True)
 pyplot.figure(1)
 # line plot
 pyplot.subplot(211)
 pyplot.plot(series)
 # histogram
 pyplot.subplot(212)
 pyplot.hist(series)
 pyplot.show()
```
[image omitted: temporary Notion asset]
### **8.2 제곱근 변환 (Square Root Transform)**
- 제곱근 변환은 데이터에 **제곱근(sqrt)을 취하는** 간단한 파워 변환
- 이 방법은 데이터의 이차 함수적(quadratic) 성장 추세를 선형(linear)으로 만들고, 분산이 점차 커지는 현상을 완화하는 데 효과적
1. **이론 예제: 이차 함수 데이터 변환**
- 제곱근 변환의 효과를 명확히 보여주기 위해, `y = x^2` 형태의 완벽한 이차 함수(quadratic) 데이터를 생성하여 변환을 적용
1. **원본 이차 함수 데이터 생성 및 시각화 코드**
→ 라인 플롯은 위로 볼록한 곡선 형태를 띈다.
```python
from matplotlib import pyplot
series = [i**2 for i in range(1,100)]
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(series)
# histogram
pyplot.subplot(212)
pyplot.hist(series)
pyplot.show()
```
[image omitted: temporary Notion asset]
2. **제곱근 변환 적용 코드**
→ 위에서 생성한 이차 함수 데이터에 제곱근을 적용하면, 곡선 형태의 라인 플롯이 완벽한 **직선**으로 변환
```python
from matplotlib import pyplot
from numpy import sqrt
series = [i**2 for i in range(1,100)]
# sqrt transform
transform = sqrt(series)
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(transform)
# histogram
pyplot.subplot(212)
pyplot.hist(transform)
pyplot.show()
```
[image omitted: temporary Notion asset]
1. **실제 데이터 적용: 항공 승객 데이터 변환**
- 이제 항공 승객 데이터에 제곱근 변환을 적용하여 증가하는 추세와 분산을 완화
- **제곱근 변환 적용 코드**
변환 후 라인 플롯을 보면, 원본 데이터의 가파른 증가세가 완만해지고 시간에 따른 변동폭이 이전보다 일정해진 것을 확인할 수 있음
```python
from pandas import read_csv
from pandas import DataFrame
from numpy import sqrt
from matplotlib import pyplot
series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True, squeeze=True)
dataframe = DataFrame(series.values)
dataframe.columns = ['passengers']
dataframe['passengers'] = sqrt(dataframe['passengers'])
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(dataframe['passengers'])
# histogram
pyplot.subplot(212)
pyplot.hist(dataframe['passengers'])
pyplot.show()
```
[image omitted: temporary Notion asset]
### **8.3 로그 변환 (Log Transform)**
- 로그 변환(Log Transform)은 제곱근 변환보다 더 강한 변환 기법으로, 데이터가 기하급수적(exponential)으로 매우 빠르게 증가할 때 효과적
-  로그(`log`)를 적용하여 급격한 성장 추세를 선형으로 만들 수 있음
1. **이론 예제: 지수 함수 데이터 변환**
→ 로그 변환의 원리를 보여주기 위해, `y = e^x` 형태의 완벽한 지수 함수 데이터를 생성하고 변환을 적용
1. **원본 지수 함수 데이터 생성 및 시각화 코드**
```python
from matplotlib import pyplot
from math import exp
series = [exp(i) for i in range(1,100)]
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(series)
# histogram
pyplot.subplot(212)
pyplot.hist(series)
pyplot.show()
```
[image omitted: temporary Notion asset]
→ 라인 플롯은 후반부로 갈수록 수직에 가깝게 치솟는 '하키 스틱' 모양
2. **로그 변환 적용 코드**
→ 위 데이터에 로그를 적용하면, 폭발적으로 증가하던 그래프가 완벽한 **직선**으로 변환
```python
from matplotlib import pyplot
from numpy import log
series = [exp(i) for i in range(1,100)]
transform = log(series)
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(transform)
# histogram
pyplot.subplot(212)
pyplot.hist(transform)
pyplot.show()
```
[image omitted: temporary Notion asset]
1. **실제 데이터 적용: 항공 승객 데이터**
- 항공 승객 데이터에 로그 변환을 적용하면, 제곱근 변환보다 추세가 더 선형에 가까워지고 분산도 안정화되는 경향을 보임
-  히스토그램 또한 더 정규분포에 가까운 모습
```python
from pandas import read_csv
from pandas import DataFrame
from numpy import log
from matplotlib import pyplot
series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True, squeeze=True)
dataframe = DataFrame(series.values)
dataframe.columns = ['passengers']
dataframe['passengers'] = log(dataframe['passengers'])
pyplot.figure(1)
# line plot
pyplot.subplot(211)
pyplot.plot(dataframe['passengers'])
# histogram
pyplot.subplot(212)
pyplot.hist(dataframe['passengers'])
pyplot.show()
```
[image omitted: temporary Notion asset]
### 8.4 박스-칵스 변환 (Box-Cox Transform)
- **박스-칵스 변환**은 제곱근, 로그 변환 등을 모두 포함하는 일반화된 변환 기법
- 이 변환의 가장 큰 장점은 데이터에 가장 적합한 변환을 **자동으로 찾아준다**는 것
- **주요 파라미터**: **람다(lambda)**
- **λ=1.0**: 변환 없음 (원본 데이터 그대로)
- **λ=0.5**: 제곱근 변환 (Square Root Transform)
- **λ=0.0**: 로그 변환 (Log Transform)
- **λ=−0.5**: 역 제곱근 변환 (Reciprocal Square Root Transform)
- **λ=−1.0**: 역수 변환 (Reciprocal Transform)
1. **람다(λ) 값을 직접 지정하는 방법 (수동 변환)**
- 가장 기본적인 방법은 특정 변환을 수행하기 위해 λ 값을 직접 코드에 명시하는 것
```python
# 수동으로 람다(lambda) 값을 0으로 지정하여 로그 변환 수행
from pandas import read_csv
from pandas import DataFrame
from scipy.stats import boxcox
from matplotlib import pyplot

# 데이터 불러오기
series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True)

# 데이터프레임으로 변환
dataframe = DataFrame(series.values)
dataframe.columns = ['passengers']

# boxcox 변환 (lambda=0은 로그 변환을 의미)
dataframe['passengers'] = boxcox(dataframe['passengers'], lmbda=0.0)

# 변환된 데이터 시각화
pyplot.figure(1)
# 라인 플롯
pyplot.subplot(211)
pyplot.plot(dataframe['passengers'])
# 히스토그램
pyplot.subplot(212)
pyplot.hist(dataframe['passengers'])
pyplot.show()
```
[image omitted: temporary Notion asset]
1. **최적의 람다(λ) 값을 자동으로 찾는 방법 (자동 최적화)**
- `boxcox` 함수의 `lmbda` 인자를 `None`으로 설정하거나 생략하면, 라이브러리가 **데이터에 가장 적합한(최적의) λ 값을 자동으로 계산**
- 이 함수는 변환된 데이터와 함께 최적의 λ 값을 반환
```python
# 자동으로 최적의 람다(lambda) 값을 찾아 변환 수행
from pandas import read_csv
from pandas import DataFrame
from scipy.stats import boxcox
from matplotlib import pyplot

# 데이터 불러오기
series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True)

# 데이터프레임으로 변환
dataframe = DataFrame(series.values)
dataframe.columns = ['passengers']

# boxcox 변환 (lmbda를 지정하지 않으면 자동으로 최적의 값을 찾음)
dataframe['passengers'], lam = boxcox(dataframe['passengers'])
print('Optimal Lambda: %f' % lam)

# 변환된 데이터 시각화
pyplot.figure(1)
# 라인 플롯
pyplot.subplot(211)
pyplot.plot(dataframe['passengers'])
# 히스토그램
pyplot.subplot(212)
pyplot.hist(dataframe['passengers'])
pyplot.show()
```
```python
Lambda: 0.148023
```
[image omitted: temporary Notion asset]

---

# 9장.  Moving Average Smoothing

---
### **9.1 이동 평균 평활 (Moving Average Smoothing)**
- 평활(Smoothing)은 시계열 데이터의 미세한 변동(노이즈)을 제거하여 근본적인 인과 과정을 더 잘 드러내기 위해 적용되는 기법
-  이동 평균은 지정된 '윈도우 크기' 내의 원본 데이터 값들의 평균으로 구성된 새로운 시계열을 생성하는 간단한 평활 기법
**9.1.1 중심 이동 평균 (Centered Moving Average)**
- 현재 시점(t)의 값은 t 시점을 중심으로 이전, 현재, 그리고 이후 시점의 원본 데이터 값들의 평균으로 계산
-  예를 들어, 윈도우 크기가 3일 경우의 계산식: 
```math
center\_ma(t)=mean(obs(t−1),obs(t),obs(t+1))
```
**9.1.2 후행 이동 평균 (Trailing Moving Average)**
- 현재 시점(t)의 값은 t 시점과 그 이전의 원본 데이터 값들의 평균으로 계산
-  이 방법은 과거 데이터만을 사용하므로 시계열 예측에 주로 사용
- 윈도우 크기가 3일 경우의 계산식: 
```math
trail\_ma(t)=mean(obs(t−2),obs(t−1),obs(t))
```
### **9.2 데이터에 대한 가정 (Data Expectations)**
- 이동 평균을 계산하는 것은 데이터에 대한 몇 가지 가정을 전제로 함
- 이동 평균을 적용하면 데이터의 \*\*추세(trend)\*\*와 \*\*계절성(seasonality)\*\*이 제거되었다고 가정
-  즉, 데이터가 뚜렷한 장기적 증감이나 주기적인 패턴이 없는 \*\*정상성(stationary)\*\*을 가진다고 봄
### **9.3 일일 여성 출생아 수 데이터셋 (Daily Female Births Dataset)**
이 학습에서는 1959년 캘리포니아의 일일 여성 출생아 수를 기록한 데이터셋을 예제로 사용
### **9.4 데이터 준비로서의 이동 평균 (Moving Average as Data Preparation)**
- 이동 평균은 원본 데이터셋의 무작위 변동을 줄여 평활화된 버전을 만드는 데이터 준비 기법으로 사용될 수 있음
-  이를 통해 데이터의 근본적인 패턴을 더 잘 파악할 수 있음
- Pandas의 `rolling()` 함수를 사용하면 데이터 위에 지정된 크기의 윈도우를 생성하여 이동 평균을 쉽게 계산할 수 있음
- 예를 들어, '일일 여성 출생아 수' 데이터셋의 첫 번째 이동 평균 값(1월 3일)은 다음과 같이 계산:
```math
obs(t)=31×(obs(t−2)+obs(t−1)+obs(t))
```
```math
=\dfrac{1}{3}×(35+32+30)=32.333
```
```python
# 필요한 라이브러리 임포트
import pandas as pd
from matplotlib import pyplot

# 데이터셋 로드
series = pd.read_csv('daily-total-female-births.csv', header=0, index_col=0, parse_dates=True, squeeze=True)

# 윈도우 크기 3으로 후행 이동 평균 계산
rolling = series.rolling(window=3)
rolling_mean = rolling.mean()

# 처음 10개 결과 출력
print(rolling_mean.head(10))

# 원본(파란색)과 변환된 데이터(빨간색) 플롯
series.plot()
rolling_mean.plot(color='red')
pyplot.show()

# 처음 100개 관측치 확대
series[:100].plot()
rolling_mean[:100].plot(color='red')
pyplot.show()
```


```python
Date
 1959-01-01
 1959-01-02
 NaN
 NaN
 1959-01-03 32.333333
 1959-01-04 31.000000
 1959-01-05 35.000000
 1959-01-06 34.666667
 1959-01-07 39.333333
 1959-01-08 39.000000
 1959-01-09 42.000000
 1959-01-10 36.000000
 Name: Births, dtype: float64
```
**출력:<br>** 처음 두 값은 윈도우(3)를 채울 데이터가 부족하여 `NaN`으로 표시<br><br>


[image omitted: temporary Notion asset]
**그래프:** 
- 아래 그래프는 원본 데이터(파란색)와 그 위에 겹쳐진 이동 평균(빨간색)을 보여줌
- 이동 평균선이 원본 데이터의 변동성을 줄여 더 부드러운 형태로 나타나는 것을 볼 수 있음
-  후행 이동 평균의 특성상 변환된 데이터에서 약간의 \*\*지연(lag)\*\*이 뚜렷하게 관찰<br><br>


### **9.5 특성 공학으로서의 이동 평균 (Moving Average as Feature Engineering)**
- 이동 평균은 시계열 예측을 지도 학습(supervised learning) 문제로 다룰 때 새로운 입력 정보(feature)로 사용될 수 있음
- 즉, **과거 데이터의 이동 평균 값을 다음 시간 단계의 값을 예측하는 데 사용하는 것**
- 이를 위해서는 예측하려는 값보다 이전의 데이터만을 사용해야 함
-  예를 들어, 윈도우 크기가 3일 때 `t+1` 시점의 값을 예측하려면, `t`, `t-1`, `t-2` 시점의 값들을 사용해 이동 평균을 계산하고 이를 입력 특성으로 활용
1. ** 시계열 데이터를 지도 학습용으로 변환 (Lag Variable 생성)**
- 가장 먼저 해야 할 일은 연속된 시간 순서의 데이터를 **'입력(X)과 정답(y)'** 의 쌍으로 만드는 것
- **X, y 구조:** `obs1`을 보고 `obs2`를 맞추고, `obs2`를 보고 `obs3`를 맞추는 식으로 데이터 구조를 변경
- 입력 X (t-1 시점): `obs1`, `obs2`, `obs3`, ...
- 정답 y (t 시점): `obs2`, `obs3`, `obs4`, ...
>  이렇게 이전 시점의 데이터를 현재 시점의 입력값으로 사용하는 것을 지연 변수(Lag Variable)를 만든다고 하며, 이는 시계열 문제를 지도 학습으로 풀기 위한 가장 기본적인 변환
1. **미래 정보 누수 방지를 위한 이동 평균 계산 (Data Shift)**
그다음, 이동 평균을 '추가적인 입력 정보'로 사용하려고 할 때 매우 중요한 주의사항:
- **문제점 (미래 정보 누수):** 
- `obs3`을 예측해야 하는 상황을 가정
- 만약 이동 평균을 계산할 때 `obs1`, `obs2`, **`obs3`** 를 포함시킨다면, 이것은 아직 일어나지 않은 미래의 정답(`obs3`)을 보고 예측하는 것과 같아서 모델 훈련의 의미가 X
- **해결책 (데이터 시프트):** 이 문제를 해결하기 위해 의도적으로 데이터를 **'이동(shift)'** 
- `obs3`을 예측하기 위한 이동 평균 특성은 그 이전 데이터인 `obs1`과 `obs2`까지만 사용해서 계산되도록 정렬하는 것
- **코드 예제**
> 아래 코드는 '일일 여성 출생아 수' 데이터셋을 지도 학습 형식으로 변환하는 예제<br> `t+1`(예측 대상), `t`(현재 값), 그리고 `mean`(과거 3개 값의 이동 평균)을 포함하는 데이터프레임을 생성
```python
# 필요한 라이브러리 임포트
import pandas as pd
from pandas import DataFrame
from pandas import concat

# 데이터셋 로드
series = pd.read_csv('daily-total-female-births.csv', header=0, index_col=0, parse_dates=True, squeeze=True)

# 데이터프레임으로 변환
df = DataFrame(series.values)

# 윈도우 크기 설정
width = 3

# 지연(lag) 데이터 생성 및 이동 평균 계산
lag1 = df.shift(1)
lag3 = df.shift(width - 1)
window = lag3.rolling(window=width)
means = window.mean()

# 데이터프레임 병합
dataframe = concat([means, lag1, df], axis=1)
dataframe.columns = ['mean', 't', 't+1']

# 처음 10개 행 출력
print(dataframe.head(10))
```
```python
 mean t t+1
 0 NaN NaN 35
 1 NaN 35.0 32
 2 NaN 32.0 30
 3 NaN 30.0 31
 4 32.333333 31.0 44
 5 31.000000 44.0 29
 6 35.000000 29.0 45
 7 34.666667 45.0 43
 8 39.333333 43.0 38
 9 39.000000 38.0 27
```
- 초기 몇몇 행은 지연(shift) 및 롤링 윈도우 계산에 필요한 데이터가 부족하여 `NaN` 값을 가짐
- 4번째 행부터 `mean`, `t`, `t+1` 값이 모두 채워진 것을 볼 수 있음<br>
### **9.6 예측으로서의 이동 평균 (Moving Average as Prediction)**
- 이동 평균값은 그 자체로 **다음 시점에 대한 예측값**으로 직접 사용될 수 있음
-  이는 시계열의 추세나 계절성이 이미 제거되었다고 가정하는 단순한(naive) 예측 모델
- 예측은 **워크 포워드(walk-forward)** 방식으로 이루어짐
-  즉, 새로운 데이터가 관측될 때마다 모델이 업데이트되어 다음 날을 예측
- **코드 예제**
> 아래 코드는 이동 평균을 사용하여 예측을 수행하고, 실제 값과 비교하여 모델의 성능을 평가
```python
# 필요한 라이브러리 임포트
from math import sqrt
from pandas import read_csv
from numpy import mean
from sklearn.metrics import mean_squared_error
from matplotlib import pyplot

# 데이터셋 로드
series = read_csv('daily-total-female-births.csv', header=0, index_col=0, parse_dates=True, squeeze=True)
X = series.values

# 윈도우 크기 및 데이터 분할
window = 3
history = [X[i] for i in range(window)]
test = [X[i] for i in range(window, len(X))]
predictions = list()

# 워크 포워드 검증
for t in range(len(test)):
    length = len(history)
    yhat = mean([history[i] for i in range(length-window, length)]) # 예측
    obs = test[t] # 실제 값
    predictions.append(yhat)
    history.append(obs)
    print('predicted=%f, expected=%f' % (yhat, obs))

# 성능 평가 (RMSE)
rmse = sqrt(mean_squared_error(test, predictions))
print('Test RMSE: %.3f' % rmse)

# 예측 결과 시각화
pyplot.plot(test)
pyplot.plot(predictions, color='red')
pyplot.show()
```
```python
 predicted=32.333333, expected=31.000000
 predicted=31.000000, expected=44.000000
 predicted=35.000000, expected=29.000000
 ...
 predicted=38.666667, expected=37.000000
 predicted=38.333333, expected=52.000000
 predicted=41.000000, expected=48.000000
 predicted=45.666667, expected=55.000000
 predicted=51.666667, expected=50.000000
 Test RMSE: 7.834
```


[image omitted: temporary Notion asset]
- **파란색 선:** 실제 일일 출생아 수 (정답 값)
- **빨간색 선:** 이동 평균 모델이 예측한 값


[image omitted: temporary Notion asset]
Figure 9.3 그래프의 첫 100일 구간만 확대한 것
- **지연(Lag) 현상 확인:** 예측값(빨간색)이 실제값(파란색)의 움직임을 한 박자씩 늦게 따라가는 **지연(lag)** 현상을 명확하게 관찰
- **변동성:** 이동 평균 예측은 본질적으로 여러 값의 평균이므로, 실제 데이터의 급격한 변동(뾰족한 피크)을 제대로 따라가지 못하고 더 완만하게 움직이는 것을 볼 수 있음

---

# 10장. A Gentle Introduction to White Noise

---

백색 소음(White Noise)은 시계열 예측에서 중요한 개념입니다. 어떤 시계열이 백색 소음이라면, 그 데이터는 무작위 숫자들의 나열이며 예측할 수 없습니다. 예측 모델의 오차(error)가 백색 소음이 아니라면, 모델을 개선할 여지가 있다는 뜻입니다.

### **10.1 백색 소음이란? (What is a White Noise?)**
> 백색 소음은 시계열의 모든 값들이 **서로 독립적이고 동일한 분포**를 따르는 상태를 말하며, 다음과 같은 특징을 가짐: 
- **평균(mean)이 0이다**
- **분산(variance)이 일정하다 (sigma2)**
- **모든 값들은 서로 0의 상관관계(zero correlation)를 가진다**
만약 이 값들이 정규분포(Gaussian distribution)에서 추출되었다면 가우시안 백색 소음(Gaussian white noise)이라고 부른다.
### **10.2 왜 중요한가? (Why Does it Matter?)**
- 백색 소음은 두 가지 중요한 이유:
1. **예측 가능성 (Predictability):** 만약 당신의 시계열 데이터가 백색 소음이라면, 정의상 그것은 **무작위**하므로 합리적으로 모델링하거나 **예측할 수 X**
2. **모델 진단 (Model Diagnostics):** 시계열 예측 모델이 만들어낸 **오차(error)들의 시계열은 이상적으로 백색 소음**이어야 함 <br>→ 만약 오차가 백색 소음이 아니라면, 모델이 데이터에 존재하는 특정 패턴을 포착하지 못했다는 신호이며, 모델을 더 개선할 수 있음을 의미
### **10.3 당신의 시계열은 백색 소음인가? (Is your Time Series White Noise?)**
- 어떤 시계열이 다음 조건 중 하나라도 해당하면 백색 소음이 X
- 평균이 0이 아닌가?
- 시간에 따라 분산이 변하는가?
- 과거 값(lag values)과 상관관계가 있는가?
- 이를 확인하기 위해 다음과 같은 도구들을 사용할 수 있음: 
- **라인 그래프 (Line plot):** 눈에 띄는 패턴이 있는지 확인
- **요약 통계 (Summary statistics):** 평균이 0에 가깝고 분산이 일정한지 확인
- **자기상관 그래프 (Autocorrelation plot):** 과거 값과의 상관관계가 있는지 확인
### 10.4장: 백색잡음(White Noise) 시계열 예제 요약
1. **백색잡음 시계열 생성**
- 먼저, `random` 모듈의 `gauss()` 함수를 사용하여 평균(μ)이 0.0이고 표준편차(σ)가 1.0인 정규분포(가우시안분포)에서 1,000개의 무작위 변수를 추출
- 그런 다음 이 리스트를 다루기 쉽게 Pandas `Series` 객체로 변환
```python
from random import gauss
from random import seed
from pandas import Series
from pandas.plotting import autocorrelation_plot
from matplotlib import pyplot

# seed a random number generator
seed(1)
# create white noise series
series = [gauss(0.0, 1.0) for i in range(1000)]
series = Series(series)
```
1. **요약 통계량 계산**
- 생성된 시계열 데이터의 기본적인 통계치를 확인하기 위해 `describe()` 함수를 사용
-  이를 통해 데이터의 개수(count), 평균(mean), 표준편차(std) 등을 확인할 수 있음
```python
# summary stats
print(series.describe())
```
```bash
 count  1000.000000
 mean   -0.013222
 std    1.003685
 min    -2.961214
 25%    -0.684192
 50%    -0.010934
 75%    0.703915
 max    2.737260
```
> 실행 결과, 평균은 약 -0.013으로 0에 가깝고 표준편차는 약 1.003으로 1에 가까운 것을 볼 수 있어, 데이터가 우리가 설정한 분포를 잘 따르고 있음을 알 수 있음
1. **시각화를 통한 백색잡음 확인**
1. 선 그래프 (Line Plot)
- 데이터를 선 그래프로 시각화하여 시간의 흐름에 따른 데이터의 무작위성을 확인
-  백색잡음은 뚜렷한 추세나 패턴이 없어야 함
```bash
# line plot
series.plot()
pyplot.show()
```
[image omitted: temporary Notion asset]
→ 그래프는 특별한 패턴 없이 무작위로 움직이는 것처럼 보임
2. 히스토그램 (Histogram)
- 데이터의 분포를 확인하기 위해 히스토그램을 그림
- 데이터가 가우시안분포(정규분포)를 따르므로, 히스토그램은 종 모양(bell-curve)을 보여야 함
```bash
# histogram plot
series.hist()
pyplot.show()
```
[image omitted: temporary Notion asset]
→ 히스토그램은 예상대로 종 모양을 나타내어 데이터가 정규분포를 따름을 시각적으로 확인
3. 자기상관도(Correlogram) 플롯
- 시계열 데이터의 자기상관(autocorrelation)을 확인하기 위해 코렐로그램을 그림
-  백색잡음은 시간의 지연(lag)에 따른 자기상관이 없어야 함
-  즉, 대부분의 시차에서 상관계수가 0에 가까워야 함
```bash
# autocorrelation
autocorrelation_plot(series)
pyplot.show()
```
[image omitted: temporary Notion asset]

---

# 11장. A Gentle Introduction to the Random Walk

---
### **11.1 랜덤 시리즈 (Random Series)**
- 파이썬의 `random` 모듈을 사용하여 0과 10 사이의 무작위 정수 1,000개로 구성된 시계열 데이터를 생성하고 시각화 함
```python
# create and plot a random series
from random import seed
from random import randrange
from matplotlib import pyplot
seed(1)
series = [randrange(10) for i in range(1000)]
pyplot.plot(series)
pyplot.show()
```
[image omitted: temporary Notion asset]
- 이 그래프는 특별한 패턴이나 구조 없이 무질서하게 나타나는 것을 확인할 수 있음
- 이는 "백색 잡음(white noise)"이라고도 불리며, 아직 랜덤 워크는 X
### **11.2 랜덤 워크 (Random Walk)**
- 랜덤 워크는 이전 값에 무작위적인 값을 더해 다음 값을 만드는 방식으로 생성
- 이 과정은 데이터에 종속성과 일관성을 부여하여 주식 시장의 가격 변동과 같은 실제 시계열 데이터와 유사한 형태를 보임
랜덤 워크는 다음과 같은 과정으로 생성: 
1. 1 또는 1로 시작
2. 이전 값에 무작위로 -1 또는 1을 더함
3. 원하는 길이만큼 2번 과정을 반복
이를 수식으로 표현:
```math
y(t)=B0+B1×X(t−1)+e(t)
```
```python
# create and plot a random walk
from random import seed
from random import random
from matplotlib import pyplot
seed(1)
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
pyplot.plot(random_walk)
pyplot.show()
```
[image omitted: temporary Notion asset]
### **11.3 랜덤 워크와 자기상관 (Random Walk and Autocorrelation)**
- 랜덤 워크는 현재 관측치가 이전 관측치와 강한 상관관계를 가짐
- 이를 확인하기 위해 자기상관(autocorrelation) 플롯을 사용
- 자기상관 플롯은 시점(lag)에 따른 관측치 간의 상관관계를 보여주며, 랜덤 워크의 경우 시점이 멀어질수록 상관관계가 선형적으로 감소하는 경향을 보임
```python
# plot the autocorrelation of a random walk
from random import seed
from random import random
from matplotlib import pyplot
from pandas.plotting import autocorrelation_plot
seed(1)
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
autocorrelation_plot(random_walk)
pyplot.show()
```
[image omitted: temporary Notion asset]
### **11.4 랜덤 워크와 정상성 (Random Walk and Stationarity)**
- 랜덤 워크는 **비정상성(non-stationary)** 시계열
-  즉, 시간의 흐름에 따라 평균과 분산이 일정하지 않음
- 데이터의 정상성은 ADF(Augmented Dickey-Fuller) 검정을 통해 통계적으로 확인 가능
- ADF 검정 결과, 통계량(ADF Statistic)이 임계값(Critical Values)보다 크면 데이터가 비정상성이라는 귀무가설을 기각할 수 없음
-  랜덤 워크 데이터의 경우, 통계량이 임계값들보다 크므로 비정상성임을 알 수 있음
```python
# calculate the stationarity of a random walk
from random import seed
from random import random
from statsmodels.tsa.stattools import adfuller
seed(1)
# generate random walk
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
# statistical test
result = adfuller(random_walk)
print('ADF Statistic: %f' % result[0])
print('p-value: %f' % result[1])
print('Critical Values:')
for key, value in result[4].items():
    print('\t%s: %.3f' % (key, value))
```


- output


```bash
ADF Statistic: 0.341605
p-value: 0.979175
Critical Values:
5%: -2.864
1%: -3.437
10%: -2.568
```


- 이러한 비정상성 데이터는 현재 관측치와 이전 관측치의 차이를 계산하는 \*\*차분(differencing)\*\*을 통해 정상성 데이터로 변환할 수 있음
-  차분된 데이터는 -1과 1의 무작위적인 움직임만 남아 구조가 없는 것처럼 보임
- 코드 예시 (차분):
```python
# calculate and plot a differenced random walk
from random import seed
from random import random
from matplotlib import pyplot
seed(1)
# create random walk
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
# take difference
diff = list()
for i in range(1, len(random_walk)):
    value = random_walk[i] - random_walk[i - 1]
    diff.append(value)
# line plot
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
- 차분된 시리즈의 자기상관 플롯을 확인하면, 대부분의 시차에서 상관관계가 거의 0에 가깝고 신뢰구간을 벗어나지 않는 것을 볼 수 있음
-  이는 데이터가 정상성을 띠게 되었음을 의미
- 코드 예시 (차분된 데이터의 자기상관 플롯):
```python
# plot the autocorrelation of a differenced random walk
from random import seed
from random import random
from matplotlib import pyplot
from pandas.plotting import autocorrelation_plot
seed(1)
# create random walk
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
# take difference
diff = list()
for i in range(1, len(random_walk)):
    value = random_walk[i] - random_walk[i - 1]
    diff.append(value)
# line plot
autocorrelation_plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
### **11.5 랜덤 워크 예측하기 (Predicting a Random Walk)**
- 랜덤 워크는 본질적으로 **예측이 불가능**
-  다음 시점의 값은 이전 시점의 값에 무작위적인 변동이 더해져 결정되기 때문
- 따라서, 할 수 있는 최선의 예측은 이전 시점의 관측값을 그대로 사용하는 것
= 이를 **"Persistence Model"** 또는 \*\*"Naive Forecast"\*\*라고 부름
- 이 모델의 성능을 평가하기 위해 데이터를 훈련(train) 세트와 테스트(test) 세트로 나누고, 테스트 세트의 예측값에 대한 평균 제곱근 오차(RMSE)를 계산
- 코드 예시(Peristence Model):
```python
# persistence forecasts for a random walk
from random import seed
from random import random
from sklearn.metrics import mean_squared_error
from math import sqrt
# generate the random walk
seed(1)
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
# prepare dataset
train_size = int(len(random_walk) * 0.66)
train, test = random_walk[0:train_size], random_walk[train_size:]
# persistence
predictions = list()
history = train[-1]
for i in range(len(test)):
    yhat = history
    predictions.append(yhat)
    history = test[i]
rmse = sqrt(mean_squared_error(test, predictions))
print('Persistence RMSE: %.3f' % rmse)
```
```bash
Persistence RMSE: 1.000
```
- 결과적으로 RMSE는 1.000이 나오는데, 이는 매 시점의 변화량이 +1 또는 -1이기 때문에 예상할 수 있는 결과
- 만약 변화량의 범위(분산)를 알고 있다는 가정하에, 이전 값에 무작위로 -1 또는 1을 더해 예측하는 모델을 만들 수도 있음
-  하지만 이 방법은 Persistence 모델보다 더 나쁜 성능을 보임
- 코드 예시 (무작위 예측):
```python
# random predictions for a random walk
from random import seed
from random import random
from sklearn.metrics import mean_squared_error
from math import import sqrt
# generate the random walk
seed(1)
random_walk = list()
random_walk.append(-1 if random() < 0.5 else 1)
for i in range(1, 1000):
    movement = -1 if random() < 0.5 else 1
    value = random_walk[i-1] + movement
    random_walk.append(value)
# prepare dataset
train_size = int(len(random_walk) * 0.66)
train, test = random_walk[0:train_size], random_walk[train_size:]
# random prediction
predictions = list()
history = train[-1]
for i in range(len(test)):
    yhat = history + (-1 if random() < 0.5 else 1)
    predictions.append(yhat)
    history = test[i]
rmse = sqrt(mean_squared_error(test, predictions))
print('Random RMSE: %.3f' % rmse)
```
```python
Random RMSE: 1.328
```
- RMSE가 1.328로, Persistence 모델보다 성능이 떨어지는 것을 확인할 수 있음
- 따라서 랜덤 워크 시계열에서는 Naive Forecast가 가장 좋은 예측 방법
### **11.6 당신의 시계열은 랜덤 워크인가? (Is Your Time Series a Random Walk?)**
> 어떤 시계열 데이터가 랜덤 워크인지 확인하는 몇 가지 방법은 다음과 같음:
- **강한 시계열 의존성:** 데이터가 시간에 따라 강한 의존성을 보이며, 그 의존성이 선형적으로 감소하는 패턴을 보임
- **비정상성:** 데이터가 비정상성을 띠며, 차분을 통해 정상성으로 변환했을 때 뚜렷하게 학습할 만한 구조가 나타나지 않음
- **Persistence 모델의 성능:** Persistence 모델이 가장 좋은 예측 성능을 보입니다. 만약 더 복잡한 모델을 사용해도 이 기준 모델보다 성능이 향상되지 않는다면, 해당 데이터는 랜덤 워크일 가능성이 높음
- 랜덤 워크 가설은 특히 주식 시장 분석에 적용되며, 주가의 단기적인 움직임은 과거의 이력만으로는 예측할 수 없다는 이론의 근거가 된다.
- 인간은 모든 곳에서 패턴을 찾으려는 경향이 있지만, 랜덤 워크 프로세스를 정교한 모델로 분석하려 하는 것은 시간 낭비가 될 수 있음을 경계해야 함

---

# 12장. Decompose Time Series Data

---
### **12.1 시계열 구성 요소 (Time Series Components)**
> 시계열 데이터는 예측 모델 선택을 돕기 위해 체계적인(Systematic) 요소와 비체계적인(Non-Systematic) 요소로 나눌 수 있음
- **체계적 요소:** 일관성이나 반복성이 있어 설명하고 모델링할 수 있는 부분
- **수준 (Level):** 시계열 데이터의 평균적인 값
- **추세 (Trend):** 시간에 따라 데이터가 전반적으로 증가하거나 감소하는 경향
- **계절성 (Seasonality):** 특정 기간(예: 1년, 1주일)을 주기로 반복되는 패턴
- **비체계적 요소:** 직접 모델링할 수 없는 무작위적인 변동
- **노이즈 (Noise) 또는 잔차 (Residual):** 위의 세 가지 요소로 설명되지 않는 나머지 부분
### **12.2 시계열 구성 요소의 결합 (Combining Time Series Components)**
이 네 가지 구성 요소는 주로 덧셈 또는 곱셈 형태로 결합되어 하나의 시계열을 형성
**12.2.1 덧셈 모델 (Additive Model)**
구성 요소들이 서로 더해져 시계열을 형성하는 모델입니다. 추세가 직선에 가깝고, 계절성의 진폭이 시간에 따라 일정할 때 사용됩니다.
```math
y(t)=Level+Trend+Seasonality+Noise
```
**12.2.2 곱셈 모델 (Multiplicative Model)**
구성 요소들이 서로 곱해져 시계열을 형성하는 모델입니다. 추세가 지수적으로 변하거나, 계절성의 진폭이 시간에 따라 변할 때(예: 시간이 지날수록 변동성이 커질 때) 적합합니다.
```math
y(t)=Level×Trend×Seasonality×Noise
```
### **12.3 분해를 도구로 활용하기 (Decomposition as a Tool)**
- 분해는 시계열 분석의 핵심 도구
- 데이터의 구조를 파악하고, 각 구성 요소를 어떻게 모델링할지 전략을 세우는 데 도움을 줌
- 예를 들어, 분해를 통해 추세를 파악하고 이를 모델에서 제거하거나, 계절성을 명시적으로 모델링하는 등의 결정을 내릴 수 있음
- 실제 데이터는 덧셈과 곱셈 모델이 혼합된 복잡한 형태일 수 있지만, 이 두 가지 기본 모델은 데이터를 탐색하고 이해하는 유용한 프레임워크를 제공
### **12.4 자동 시계열 분해 (Automatic Time Series Decomposition)**
- Python의 `statsmodels` 라이브러리는 `seasonal_decompose()` 함수를 통해 시계열 데이터를 자동으로 분해하는 기능을 제공
- 이 함수를 사용하려면 모델을 'additive' 또는 'multiplicative'로 지정해야 함
```python
from statsmodels.tsa.seasonal import seasonal_decompose
# series = ... (시계열 데이터 로드)
result = seasonal_decompose(series, model='additive')
print(result.trend)
print(result.seasonal)
print(result.resid)
print(result.observed)
```
**12.4.1 덧셈 분해 (Additive Decomposition)**
- 선형적으로 증가하는 추세와 임의의 노이즈로 구성된 인위적인 데이터를 생성하여 덧셈 모델로 분해하는 예시
```python
# additive decompose a contrived additive time series
from random import randrange
from matplotlib import pyplot
from statsmodels.tsa.seasonal import seasonal_decompose
series = [i+randrange(10) for i in range(1,100)]
result = seasonal_decompose(series, model='additive', freq=1)
result.plot()
pyplot.show()
```
[image omitted: temporary Notion asset]
- 결과 그래프를 보면 원본 데이터(Observed)가 추세(Trend)와 잔차(Residual)로 잘 분리된 것을 볼 수 있음
- 이 데이터는 계절성이 없으므로 계절성(Seasonal) 구성 요소는 0에 가깝게 나타남
**12.4.2 곱셈 분해 (Multiplicative Decomposition)**
- 시간에 따라 제곱 형태로 증가하는(지수적 변화) 인위적인 데이터를 생성하여 곱셈 모델로 분해하는 예시
-  덧셈 모델과 마찬가지로 추세가 성공적으로 추출된 것을 볼 수 있음
```python
# multiplicative decompose a contrived multiplicative time series
from matplotlib import pyplot
from statsmodels.tsa.seasonal import seasonal_decompose
series = [i**2.0 for i in range(1,100)]
result = seasonal_decompose(series, model='multiplicative', freq=1)
result.plot()
pyplot.show()
```
[image omitted: temporary Notion asset]
**12.4.3 항공 승객 데이터셋 예제 (Airline Passengers Dataset)**
- 실제 데이터인 항공 승객 데이터셋을 곱셈 모델로 분해하는 예제
- 이 데이터는 시간이 지남에 따라 승객 수가 증가하는 추세와 매년 반복되는 계절적 패턴을 보이며, 변동성 또한 커지므로 곱셈 모델이 적합
- 분해 결과, 추세와 계절성 정보가 합리적으로 추출된 것을 확인할 수 있음
```python
# multiplicative decompose time series
from pandas import read_csv
from matplotlib import pyplot
from statsmodels.tsa.seasonal import seasonal_decompose
series = read_csv('airline-passengers.csv', header=0, index_col=0, parse_dates=True, squeeze=True)
result = seasonal_decompose(series, model='multiplicative')
result.plot()
pyplot.show()
```
[image omitted: temporary Notion asset]

---

# 13장. Use and Remove Trends

---
### **13.1 시계열의 추세 (Trends in Time Series)**
- 추세(Trend)란 시계열 데이터의 수준(level)이 장기적으로 증가하거나 감소하는 현상을 의미
-  추세를 파악하고 활용하면 모델링 성능을 향상시킬 수 있으며, 그 이유는 다음과 같음
- **더 빠른 모델링:** 추세의 유무를 알면 모델 선택과 평가를 더 효율적으로 할 수 있음
- **더 간단한 문제:** 추세를 제거함으로써 모델링 문제를 단순화할 수 있음
- **더 많은 데이터:** 추세 정보를 모델의 입력 변수로 직접 사용하거나 요약 정보로 활용할 수 있음
**13.1.1 추세의 종류 (Types of Trends)**
- **결정론적 추세 (Deterministic Trends):** 일정하게 증가하거나 감소하는 추세
- **확률적 추세 (Stochastic Trends):** 불규칙하게 증가하거나 감소하는 추세
- **전역적 추세 (Global Trends):** 전체 시계열에 걸쳐 나타나는 추세
- **지역적 추세 (Local Trends):** 시계열의 특정 부분에만 나타나는 추세
**13.1.2 추세 식별하기 (Identifying a Trend)**
- 가장 기본적인 방법은 데이터를 시각화하여 명확한 추세가 있는지 눈으로 확인하는 것
- 선형 또는 비선형 추세선을 그려보면 추세를 더 쉽게 파악할 수 있음
**13.1.3 추세 제거하기 (Removing a Trend)**
- 추세가 있는 시계열은 **비정상성(non-stationary)** 데이터
- 추세를 모델링하고 제거하는 과정을 \*\*추세 제거(detrending)\*\*라고 하며, 이 과정을 거친 데이터는 \*\*정상성(stationary)\*\*을 띠게 됨
**13.1.4 머신러닝에서 추세 활용하기 (Using Time Series Trends in Machine Learning)**
머신러닝 관점에서 추세는 두 가지 기회를 제공:
1. **정보 제거:** 입력과 출력 변수 간의 관계를 왜곡할 수 있는 체계적인 정보를 제거
2. **정보 추가:** 입력과 출력 변수 간의 관계를 개선하기 위해 체계적인 정보를 모델에 추가
### **3.2 샴푸 판매 데이터셋 (Shampoo Sales Dataset)**
- 이 장에서는 3년간의 월별 샴푸 판매량 데이터셋을 예제로 사용하여 추세를 제거하는 방법을 알아봄
### **13.3 차분을 이용한 추세 제거 (Detrend by Differencing)**
- 추세를 제거하는 가장 간단한 방법 중 하나는 \*\*차분(differencing)\*\*
- 차분은 현재 시점의 관측값에서 이전 시점의 관측값을 빼서 새로운 시계열을 만드는 방법
```math
value(t)=observation(t)−observation(t−1)
```
- 코드 예시
```python
# detrend a time series using differencing
from pandas import read_csv
from pandas import datetime
from matplotlib import pyplot

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0, parse_dates=True,
                  squeeze=True, date_parser=parser)
X = series.values
diff = list()
for i in range(1, len(X)):
    value = X[i] - X[i - 1]
    diff.append(value)
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
- 차분을 통해 생성된 데이터는 추세가 제거된 것처럼 보임
- 이 방법은 선형적인 추세에 효과적이며, 2차 또는 3차 추세가 있는 경우 차분을 여러 번 반복 가능
### **13.4 모델 피팅을 이용한 추세 제거 (Detrend by Model Fitting)**
- 데이터에 선형 모델과 같은 추세선을 피팅(fitting)한 후, 원본 데이터에서 모델이 예측한 값을 빼서 추세를 제거하는 방법
```math
value(t)=observation(t)−prediction(t)
```
- 이 방법은 데이터에 어떤 종류의 추세(선형, 지수형 등)가 있는지 파악하는 데 도움이 된다.
-  먼저 샴푸 판매 데이터에 선형 회귀 모델을 적용하여 추세선을 만듦
- 그 다음, 원본 데이터에서 이 추세선을 빼서 추세가 제거된 데이터를 얻음
- 코드 예시
```python
# use a linear model to detrend a time series
from pandas import read_csv
from pandas import datetime
from sklearn.linear_model import LinearRegression
from matplotlib import pyplot
import numpy

def parser(x):
    return datetime.strptime('190'+x, '%Y-%m')

series = read_csv('shampoo-sales.csv', header=0, index_col=0, parse_dates=True,
                  squeeze=True, date_parser=parser)
# fit linear model
X = [i for i in range(0, len(series))]
X = numpy.reshape(X, (len(X), 1))
y = series.values
model = LinearRegression()
model.fit(X, y)
# calculate trend
trend = model.predict(X)
# plot trend
pyplot.plot(y)
pyplot.plot(trend)
pyplot.show()
# detrend
detrended = [y[i]-trend[i] for i in range(0, len(series))]
# plot detrended
pyplot.plot(detrended)
pyplot.show()
```
- 추세 제거 전 - 원본 데이터
[image omitted: temporary Notion asset]
- 추세 제거된 후
[image omitted: temporary Notion asset]
- 이 접근법은 데이터를 효과적으로 추세 제거했지만, 남은 잔차(residuals)에 여전히 곡선 형태(포물선)가 남아있는 것으로 보아 다항식 모델(polynomial fit)이 더 나은 결과를 가져왔을 수도 있음을 시사

---

# 14장.  Use and Remove Seasonality

---
### **14.1 시계열의 계절성 (Seasonality in Time Series)**
> **계절성(Seasonality)** 또는 계절적 변동은 시계열 데이터에서 고정된 주기(예: 1년, 1주일)로 반복되는 패턴을 의미 → 이러한 반복적인 사이클은 예측 모델의 성능을 저해하는 노이즈가 될 수 있음
**14.1.1 머신러닝에서의 이점 (Benefits to Machine Learning)**
계절성을 이해하고 처리하면 머신러닝 모델의 성능을 두 가지 방식으로 향상시킬 수 있음:
1. **명확한 관계 식별:** 계절성 요소를 제거하여 입력과 출력 변수 간의 관계를 더 명확하게 파악할 수 있음
2. **추가 정보 활용:** 계절성 자체를 모델의 입력 변수로 사용하여 성능을 개선할 수 있음
**14.1.2 계절성의 종류 (Types of Seasonality)**
계절성은 다양한 주기로 나타날 수 있음:
- 하루 주기
- 일일 주기
- 주간 주기
- 월간 주기
- 연간 주기
**14.1.3 계절성 제거하기 (Removing Seasonality)**
- 계절성을 식별한 후에는 이를 모델링하여 시계열에서 제거할 수 있음
- 이 과정을 **계절 조정(Seasonal Adjustment)** 또는 \*\*계절성 제거(Deseasonalizing)\*\*
- 계절성이 제거된 시계열을 **계절 조정된(seasonally adjusted)** 시계열이라고 하며, 뚜렷한 계절성을 가진 데이터는 \*\*비정상성(non-stationary)\*\*으로 간주
### **14.2 일일 최저 기온 데이터셋 (Minimum Daily Temperatures Dataset)**
- 이 장에서는 호주 멜버른의 10년간(1981-1990) 일일 최저 기온 데이터를 예제로 사용
- 이 데이터는 여름과 겨울에 따라 기온이 변하는 뚜렷한 **연간 계절성**을 보여줌
### **14.3 차분을 이용한 계절 조정 (Seasonal Adjustment with Differencing)**
> \*\*차분(differencing)\*\*은 시계열 데이터에서 계절성을 제거하는 간단한 방법<br>→ 특정 시점의 관측값에서 이전 주기의 관측값을 빼서 계절적 패턴을 제거
1. **일일 데이터 차분 (Daily Differencing)**
- 1년(365일)을 주기로 간주하고, 오늘 데이터에서 작년 같은 날의 데이터를 빼는 방식
- **설명:** `X[i]`에서 365일 전의 값인 `X[i - 365]`를 빼서 계절성을 제거
- 첫 1년 데이터는 계산할 수 없으므로 제외
```python
# deseasonalize a time series using differencing
from pandas import read_csv
from matplotlib import pyplot
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
                  parse_dates=True, squeeze=True)
X = series.values
days_in_year = 365
diff = list()
for i in range(days_in_year, len(X)):
    value = X[i] - X[i - days_in_year]
    diff.append(value)
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
Figure 14.1은 차분을 통해 계절성이 제거된 데이터를 보여줌<br>⚠️ 하지만 이 방법은 윤년(leap year)을 제대로 처리하지 못해 약간의 오차가 발생할 수 있음
1. ** 월별 데이터 차분 (Monthly Differencing)**
> 일일 데이터의 변동성을 줄이고 더 안정적인 계절성 패턴을 다루기 위해, 데이터를 월별 평균으로 변환하여 차분을 적용하는 방법
**2-1. 월별 평균 데이터 생성**
- 먼저, 일일 데이터를 월별 평균 데이터로 리샘플링(resampling)
- **설명**: Pandas의 `resample('M')` 함수를 사용해 데이터를 월 단위로 묶고, `.mean()`으로 각 월의 평균 최저 기온을 계산
```python
# calculate and plot monthly average
from pandas import read_csv
from matplotlib import pyplot
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
parse_dates=True, squeeze=True)
resample = series.resample('M')
monthly_mean = resample.mean()
print(monthly_mean.head(13))
monthly_mean.plot()
pyplot.show()
```
```python
Date
1981-01-31 17.712903
1981-02-28 17.678571
1981-03-31 13.500000
1981-04-30 12.356667
1981-05-31 9.490323
1981-06-30 7.306667
1981-07-31 7.577419
1981-08-31 7.238710
1981-09-30 10.143333
1981-10-31 10.087097
1981-11-30 11.890000
1981-12-31 13.680645
1982-01-31 16.567742
```
[image omitted: temporary Notion asset]
- 이 코드를 실행하면 월별 평균 데이터가 생성되고, Figure 14.2와 같이 연간 계절성이 더 명확하게 보이는 그래프가 그려짐
**2-2. 월별 데이터 차분**
- 위에서 생성한 월별 평균 데이터에 차분을 적용
- **설명**: 현재 월의 평균 기온에서 12개월 전, 즉 작년 같은 달의 평균 기온을 뺀다
```python
# deseasonalize monthly data by differencing
from pandas import read_csv
from matplotlib import pyplot
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
parse_dates=True, squeeze=True)
resample = series.resample('M')
monthly_mean = resample.mean()
X = monthly_mean.values
diff = list()
months_in_year = 12
for i in range(months_in_year, len(monthly_mean)):
    value = X[i] - X[i - months_in_year]
    diff.append(value)
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
- 월별 데이터의 계절성이 제거된 안정적인 시계열 그래프를 얻을 수 있음
**3. 월별 평균을 이용한 일일 데이터 차분 (개선된 방법)**
> 일일 데이터의 계절성을 제거하되, 윤년 문제 등에 더 강건하게 대처하기 위해 **작년 해당 월의 평균값**을 빼는 방식
- **설명**: 예를 들어 1982년 1월 15일의 데이터에서 작년 같은 날(1981년 1월 15일)의 값을 빼는 대신, **1981년 1월 전체의 평균 기온**을 뺀다
-  이 방법은 일일 변동에 덜 민감하고 더 안정적인 결과를 제공
```python
# deseasonalize a time series using month-based differencing
from pandas import read_csv
from matplotlib import pyplot
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
parse_dates=True, squeeze=True)
X = series.values
diff = list()
days_in_year = 365
for i in range(days_in_year, len(X)):
    # get month and year from last year
    month_str = str(series.index[i].year-1)+'-'+str(series.index[i].month)
    # get all observations from last year's month
    month_mean_last_year = series[month_str].mean()
    # difference
    value = X[i] - month_mean_last_year
    diff.append(value)
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
**4. 차분 방법의 한계**
- 차분은 유용하지만, 달력이라는 인위적인 경계를 사용한다는 한계가 있음
- 또한 계절성은 1년 단위뿐만 아니라 **주(week), 분기(quarter)** 등 다양한 시간 단위로 존재할 수 있어, 단순 차분만으로는 모든 패턴을 제거하기 어려움
## 14.4 계절성 조정: 모델링 (Modeling)
- 차분의 대안으로, 계절성 자체를 하나의 \*\*수학적 모델(mathematical model)\*\*로 만든 후, 원본 데이터에서 모델의 예측값을 빼서 계절성을 제거하는 접근법
**1. 다항식 모델 생성 및 피팅**
> 연중 날짜(1\~365일)를 입력 변수(X)로, 온도를 결과 변수(y)로 하는 \*\*다항식 모델(polynomial model)\*\*을 생성하여 데이터의 계절적 흐름을 학습시킴
- **설명**: NumPy의 `polyfit()` 함수를 사용해 데이터에 가장 적합한 4차 다항식 곡선을 찾습니다.
- **수식**:
```math
 y=(x^{4}×b1)+(x^{3}×b2)+(x^{2}×b3)+(x^{1}×b4)+b5
```
- **코드**:
```python
# model seasonality with a polynomial model
from pandas import read_csv
from matplotlib import pyplot
from numpy import polyfit
series = read_csv('daily-minimum-temperatures.csv', header=0, index_col=0,
parse_dates=True, squeeze=True)
# fit polynomial: x^2*b1 + x*b2 + ... + bn
X = [i%365 for i in range(0, len(series))]
y = series.values
degree = 4
coef = polyfit(X, y, degree)
print('Coefficients: %s' % coef)
```
**2. 계절성 곡선 생성 및 시각화**
> 학습된 모델을 이용해 전체 기간에 대한 계절성 예측 곡선을 생성하고, 원본 데이터와 함께 시각화하여 모델이 계절성을 잘 포착했는지 확인
- **코드**:
```python
# create curve
curve = list()
for i in range(len(X)):
    value = coef[-1]
    for d in range(degree):
        value += X[i]**(degree-d) * coef[d]
    curve.append(value)
# plot curve over original data
pyplot.plot(series.values)
pyplot.plot(curve, color='red', linewidth=3)
pyplot.show()
```
[image omitted: temporary Notion asset]
**결과 (Figure 14.5)**: 원본 데이터(파란색) 위에 모델이 예측한 계절성 곡선(빨간색)이 그려짐
→ 곡선이 데이터의 전반적인 계절적 흐름을 잘 따라가는 것을 볼 수 있음
**3. 모델을 이용한 계절성 제거**
> 마지막으로, 원본 데이터의 각 값에서 모델이 예측한 계절성 값을 빼서 최종적으로 계절성이 조정된 데이터를 만듦
- **설명**: `실제 관측값 - 모델의 계절성 예측값`을 계산
```python
# create seasonally adjusted
values = series.values
diff = list()
for i in range(len(values)):
    value = values[i] - curve[i]
    diff.append(value)
pyplot.plot(diff)
pyplot.show()
```
[image omitted: temporary Notion asset]
**결과 (Figure 14.6)**: 모델링을 통해 계절성이 제거된 최종 데이터 그래프
→ 차분 방법과 마찬가지로 평균 0을 중심으로 안정된 시계열 데이터가 생성<br><br>
