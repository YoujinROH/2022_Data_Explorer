# 2022_Data_Explorer
데이터 청년 캠퍼스 연세대학교 데이터 익스플로러 팀 K-CCRC 최적입지선정

발표 영상
https://youtu.be/BfxRLX3rnZg

●실행방법
[데이터_익스플로러_코드정리] 파일안에 들어있는 3개의 파일([원본데이터] ,[전처리된데이터] ,[코드 & 결과])을
jupyter notebook의 기본작업폴더로 이동 시킨 후 [코드 & 결과] 폴더의 .ipynb 확장자 파일을 
여시면 코드를 확인하실 수 있습니다.

●전처리1.ipynb
-설명
비형평계수를 구할 때 사용할 시군구별_수요(시군구별_수요.csv),
시군구별_공급(시군구별_공급.csv) 데이터를 전처리하고
회귀모델 사용시 필요한 시군구별_공공시설(시군구별_공공시설.csv)
시군구별_문화시설(시군구별_문화시설.csv) 데이터를 전처리한 코드 

-사용된 데이터
*시군구별_법정동코드
(행정동_20220701.xlsx)
*시군구별_수요
('202207_202207_연령별인구현황_월간.xlsx')
*시군구별_공급
(2022_목차_이용안내_총괄표(시.군.구)_.xlsx)
*시군구별_공공시설
(과학기술정보통신부 우정사업본부_전국 우체국 현황_20210630.csv
행정안전부_읍면동 하부행정기관 현황_20211231.csv)
*시군구별_문화시설
(작은도서관 통계데이터_202285221459.xlsx
국립도서관 통계데이터_20228522125.xlsx
공공도서관 통계데이터_20228522141.xlsx
KC_612_PBL_CLT_STATN_BIZAEA_2021.csv)

-완성된 데이터
*시군구별_법정동코드(시군구별_법정동코드.csv)
*시군구별_수요(시군구별_수요.csv')
*시군구별_공급(시군구별_공급.csv)
*시군구별_공공시설(시군구별_공공시설.csv)
*시군구별_문화시설(시군구별_문화시설.csv)

●전처리2.ipynb
-설명
회귀모델 사용시 필요한 시군구별_교육시설(시군구별_교육시설.csv),
시군구별_교통시설(시군구별_교통시설.csv), 시군구별_의료시설(시군구별_의료시설.csv)
시군구별_유통시설(시군구별_유통시설.csv) 데이터를 전처리하고 모든 시군구별 데이터를 통합하여 
시군구별_전체(시군구별_전체.csv) 데이터를 만든 후
노인복지주택과 고령자복지주택, 웰플러스주택, 그 외 고령친화주택의 시설들의 주소와 세대수를 가지고
있는 데이터들을 합친후 그 데이터들을 '시군구'를 기준으로 시군구별_전체(시군구별_전체.csv) 데이터와 
merge를 시켜 시설별 인프라와 세대수가 정리돼 있는 데이터인 시설별_세대수(시설별_전체.csv)를 만든 코드

-사용된 데이터
*시군구별_법정동코드
(시군구별_법정동코드.csv)
*시군구별_교육시설
(학교개황(20220310기준).xls
전국초중등학교위치표준데이터.csv)
*시군구별_교통시설
(한국교통안전공단_전국 지역별 대중교통 서비스별 만족도 현황_20201231.csv)
*시군구별_의료시설
(병원·약국찾기 (종합병원).xls
병원·약국찾기 (상급종합병원).xls')
*시군구별_유통시설
(위치추가] [유통] fulldata_08_25_01_P_대규모점포.csv)
*시군구별_전체
(시군구별_공공시설.csv
시군구별_교육시설.csv
시군구별_교통시설.csv
시군구별_문화시설.csv
시군구별_유통시설.csv
시군구별_의료시설.csv)
*시설별_세대수
(1. 노인복지주택.csv
2. 고령자복지주택.csv
3. 웰플러스주택.csv
4. 그 외 고령친화주택.csv)

-완성된 데이터
*시군구별_교육시설(시군구별_교육시설.csv)
*시군구별_교통시설(시군구별_교통시설.csv)
*시군구별_의료시설(시군구별_의료시설.csv)
*시군구별_유통시설(시군구별_유통시설.csv)
*시군구별_전체(시군구별_전체.csv)
*시설별_세대수(시설별_전체.csv)

●비형평계수.ipynb
-설명
시군구 단위로 정리된 공급과 수요의 데이터를 이용하여 Coulter 비형평계수의 수식에 대입해
노인인구수에 비해 노인복지주택의 공급의 형평성 정도를 알아낸 코드

-사용된 데이터
시군구별_공급.csv
시군구별_수요.csv

-완성된 데이터
시군구별_비형평계수.csv

●모델학습.ipynb
-설명

모델의 train 데이터를 '시설별 세대수' 데이터로 설정하고
모델의 test 데이터를 '시군구별 전체' 데이터 중 '시설별 세대수'가 존재하지 않는 지역만 뽑아 설정
X = 그 시설, 시군구별 인프라(독립변수)
y = 세대수(종속변수)

train 데이터 이용하여 모델 학습
1) sklearn의 LinearRegression
2) sklearn의 LinearRegression + Standard Scaling
3) sklearn의 LinearRegression + Minmax Scaling
4) sklearn의 LinearRegression + Log Transformation
5) sklearn의 LinearRegression + PCA
6) sklearn의 LinearRegression + PCA + Standard Scaling
7) sklearn의 LinearRegression + PCA + Minmax Scaling
8) sklearn의 LinearRegression + PCA + Log Transformation
9) sklearn의 Ridge
10) sklearn의 Ridge + Standard Scaling
11) sklearn의 Ridge + Minmax Scaling
12) sklearn의 Ridge + Log Transformation
13) sklearn의 Lasso
14) sklearn의 Lasso + Standard Scaling
15) sklearn의 Lasso + Minmax Scaling
16) sklearn의 Lasso + Log Transformation
17) sklearn의 ElasticNet
18) sklearn의 ElasticNet + Standard Scaling
19) sklearn의 ElasticNet + Minmax Scaling
20) sklearn의 ElasticNet + Log Transformation
21) statsmodels의 OLS
22) statsmodels의 OLS + Standard Scaling
23) statsmodels의 OLS + Minmax Scaling
24) statsmodels의 OLS + Log Transformation

마지막으로는 가장 성능이 좋았던 statsmodels의 OLS + Log Transformation 조합으로
train 데이터를 학습한 후, 학습시킨 모델에 test 데이터를 넣어주어 그 지역 세대 수를 예측하고
K-CCRC 입지 선정을 위해 수도권, 대도시는 제거하여 최적입지를 선정하는 코드

-사용된 데이터
시설별_세대수(시설별_전체.csv)

-완성된 데이터
최종후보지(최종후보지.csv)

●AHP.ipynb
-설명
지역별 인프라 시설의 상대 가중치를 이용하여 지역의 최종세부입지를 선정하기 위한 코드

1. 지역별(시/도) 인프라 시설 수 데이터를 log 변환기법으로 scaling 적용하여 시설 수 편차를 줄인 뒤, 이를 활용해 상대가중치를 계산.
2.  인프라 별 상대가중치를 지역별(읍면동) 인프라 시설 수(log scaling 적용된 데이터)에 각각 곱하여 지역별(읍면동) 합산점수를 산출
3. 정렬해서 합산점수가 가장 높은 지역 상위 3곳을 최종 세부입지로 선정

-사용된 데이터
시군구별_전체.csv
시군구별_법정동코드.csv
*포항
포항시_읍면동_인프라/포항시_읍면동_초중고.xlsx
포항시_읍면동_인프라/포항시_읍면동_대학교.xlsx
포항시_읍면동_인프라/포항시_읍면동_도서관.xlsx
포항시_읍면동_인프라/포항시_읍면동_상급종합병원.xlsx
포항시_읍면동_인프라/포항시_읍면동_종합병원.xlsx'
포항시_읍면동_인프라/포항시_읍면동_우체국.xlsx
포항시_읍면동_인프라/포항시_읍면동_유통.xlsx
포항시_읍면동_인프라/포항시_읍면동_주민센터.xlsx
*구미
구미시_읍면동_인프라/포항시_읍면동_초중고.xlsx
구미시_읍면동_인프라/포항시_읍면동_대학교.xlsx
구미시_읍면동_인프라/포항시_읍면동_도서관.xlsx
구미시_읍면동_인프라/포항시_읍면동_상급종합병원.xlsx
구미시_읍면동_인프라/포항시_읍면동_종합병원.xlsx'
구미시_읍면동_인프라/포항시_읍면동_우체국.xlsx
구미시_읍면동_인프라/포항시_읍면동_유통.xlsx
구미시_읍면동_인프라/포항시_읍면동_주민센터.xlsx
*사천
사천시_읍면동_인프라/포항시_읍면동_초중고.xlsx
사천시_읍면동_인프라/포항시_읍면동_대학교.xlsx
사천시_읍면동_인프라/포항시_읍면동_도서관.xlsx
사천시_읍면동_인프라/포항시_읍면동_상급종합병원.xlsx
사천시_읍면동_인프라/포항시_읍면동_종합병원.xlsx'
사천시_읍면동_인프라/포항시_읍면동_우체국.xlsx
사천시_읍면동_인프라/포항시_읍면동_유통.xlsx
사천시_읍면동_인프라/포항시_읍면동_주민센터.xlsx

-완성된 데이터
*포항
AHP_결과/포항시_가중치.csv
AHP_결과/포항시_인프라시설.csv
AHP_결과/포항시_세부입지.csv
*구미
AHP_결과/구미시_가중치.csv
AHP_결과/구미시_인프라시설.csv
AHP_결과/구미시_세부입지.csv
*사천
AHP_결과/사천시_가중치.csv
AHP_결과/사천시_인프라시설.csv
AHP_결과/사천시_세부입지.csv
