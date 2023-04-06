# 2022-1-Capstone-Design

```
Title : 서울특별시 예비 창업자를 위한 상권가이드 포털 (졸업작품)
Date : 2021-09 ~ 2022-05
Members : 홍성재, 박현일, 윤준호, 윤재승
Rank : 공동 3위 (총 8팀)

Title: Commercial district guide portal for prospective founders in Seoul (graduation work)
Date : 2021-09 ~ 2022-05
Members: Hong Sungjae, Park Hyunil, Yoon Junho, Yoon Jaeseung
Rank: Joint 3rd place (8 teams in total)
```

## 배경 및 목적
- 자영업 또는 창업을 처음 시도해보려는 일반인은 기존 상권, 업종 정보를 찾아보기 어려울 뿐더러 각 상권, 업종마다 어떤 강점을 갖고 있을지 고려해보기 어렵다.
- 'SEOUL COMMERCE PORTAL' 을 통해 특정 지역에서의 각 업종들의 강점을 쉽게 알아볼 수 있으며, 해당 상권의 유동 인구와 분기별 매출액, 소비자의 성별 비율, 프랜차이즈 비율 등 세부적인 지표까지 확인해 볼 수 있다.
## Background and Purpose
- It is difficult for ordinary people who want to try self-employment or start a business for the first time to find information on existing commercial districts and industries, and it is difficult to consider what strengths each commercial district and industry will have.
- Through "SEOUL COMMERCE PORTAL," the strengths of each industry in a specific region can be easily identified, and detailed indicators such as the floating population of the commercial district, quarterly sales, the gender ratio of consumers, and franchise ratio can be seen.

## 데이터
- '서울 열린데이터 광장' 상권 데이터 이용
  - [서울 열린데이터 광장](https://data.seoul.go.kr/)
- Dataset Feature 목록
  - 유동인구 수
  - 직장인구 수
  - 상주인구 수
  - 상권 주소(좌표)
  - 추정매출액
  - 점포 수
  - ETC
## Data
- Using commercial data of 'Seoul Open Data Plaza'
  - [Seoul Open Data Plaza] (https://data.seoul.go.kr/)
- Dataset Feature List
- Number of floating populations
  - Number of working people
  - Number of resident populations
  - Commercial district address (coordinate)
  - Estimated sales
  - Number of stores
  - ETC
  
## 프로젝트 진행 과정 / Project Progress
![프로젝트 진행 과정 도식](https://github.com/Mintflavor/2022-1-Capstone-Design/blob/main/assets/img1.png)

### 1. 데이터 시각화 포털
![데이터 시각화 포털](https://github.com/Mintflavor/2022-1-Capstone-Design/blob/main/assets/img2.png)
- 선택한 상권 및 업종의 유동인구 추이와 매출 비율, 매출 규모 등 예비 창업자에게 도움이 될 수 있는 시각 자료 주변 상권과 비교할 수 있는 기능을 제공한다.
  - 지리적 특성
  - 긍정적 요소
  - 부정적 요소
  - 서울 전체 상권 랭크
  - 지역구 내 상권 랭크
  - 상권 시간대별 유동인구
  - 성별 매출 비율
  - 연령대별 매출 비율
  - 업종 시간대별 매출 규모
  - 프랜차이즈 점포 비율
  - 업종 밀집도 비율
  - 연도별 유동인구 변화
  - 분기별 총 매출 규모
  - 연령대별 유동인구 수
  - 분기별 점포당 평균 매출 규모
  - Feature 간 산점도 제공
  - 상권 위치를 표기한 지도 제공

### 1. Data Visualization Portal
- It provides the ability to compare with the commercial districts around visual data that can help prospective founders, such as the trend of the floating population, sales ratio, and sales size of the selected commercial districts and industries.
  - geographical characteristics
  - a positive factor
  - a negative factor
  - Ranking of all commercial districts in Seoul
  - Ranking of commercial districts in the district
  - Floating population by commercial district time zone
  - Percentage of sales by gender
  - Percentage of sales by age group
  - Sales volume by industry time zone
  - Percentage of Franchise Stores
  - Industry density ratio
  - Changes in floating population by year
  - Total Quarterly Revenue Size
  - Number of floating populations by age group
  - Average quarterly revenue per store
  - Provides a scatterplot of the features
  - Provides a map indicating the location of the commercial district

### 2. 업종별 랭크 선정
![업종별 랭크 선정](https://github.com/Mintflavor/2022-1-Capstone-Design/blob/main/assets/img3.png)
- 서울 전체와 지역구 내 업종별 매출액 Random Forest 모델을 학습시켜 매출액에 영향을 미치는 Feature를 통해 상권 랭크를 산정한다.

### 2. Ranking by industry
- The ranking of commercial districts is calculated through Feature, which affects sales by learning the Random Forest model for each industry in all Seoul and regional districts.

## 랭크 산정 기준 / Rank calculation criteria
- 업종별 Random Forest 모델에서 매출액에 큰 영향을 미치는 상위 10 개의 Feature Importance 값을 도출한다.
- The top 10 Feature Importance values that have a significant impact on sales are derived from the Random Forest model by industry.
![Feature Importance](https://github.com/Mintflavor/2022-1-Capstone-Design/blob/main/assets/img4.png)
- 매출액에 양, 음의 영향을 미치는 Feature를 상관분석을 활용하여 각 Feature 상관계수의 부호를 Feature Importance에 곱한다.
- Feature, which has a positive and negative effect on sales, is multiplied by the sign of each Feature correlation coefficient by Feature Importance using correlation analysis.
![Correlation](https://github.com/Mintflavor/2022-1-Capstone-Design/blob/main/assets/img5.png)
- 각 상권 데이터의 가장 최근 분기 데이터와 Feature Importance를 내적한다.
- Dot product of most recent quarterly data of each commercial district data and feature importance.
$$[각\;상권\;데이터의\;record]^T\cdot[Feature\;Importance]=Score$$
- Min-Max Scale을 적용하여 각 점수를 표준화 한다.
- Standardize each score by applying the Min-Max Scale.
$$Score_{scaled}=\frac{Score-Score_{min}}{Score_{max}-Score_{min}}$$
- 최종적으로 각 점수를 내림차순으로 정렬하고 순위를 매겨 사용자가 선택한 상권이 어느정도 랭크인지 점수와 함께 보여준다.
- Finally, each score is sorted and ranked in descending order, showing how much the commercial district the user selected is ranked.

## 프로젝트 결론
- 유망상권에도 적용하여 유리한 상권 선정에 도움이 될 것으로 보인다.
- 업종을 변경하려는 자영업자, 일반인 또한 다양한 정보 확인을 통해 서울 상권 및 업종에 대한 내용에 쉽게 접근할 수 있다.
- 더 다양한 데이터(권리금, 임차료, 현금매출정보 등)를 수집한다면 더 정확한 상권 정보를 제공할 수 있을 것으로 보인다.
## Project Conclusion
- It is also applied to promising commercial districts and is expected to help select favorable commercial districts.
- Self-employed people and the general public who want to change their businesses can also easily access the contents of Seoul's commercial districts and industries through various information checks.
- It is expected that more accurate commercial information can be provided by collecting more diverse data (rights, rents, cash sales information, etc.).

## 프레임워크 / Framework
- Python3 Flask
- SB Admin 2
- Bootstrap 4
- Font Awesome 5
- jQuery
- chart.js

## 데모 웹페이지 링크 / Demo Site
- ~~[SEOUL COMMERCE PORTAL](http://ericacap.ddns.net)~~ (EXPIRED)
