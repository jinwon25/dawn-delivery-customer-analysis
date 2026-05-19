# 새벽배송 고객 구매 패턴 분석 — RFM 세분화·연관분석·협업 필터링

새벽배송 서비스의 매출을 증대할 수 있는 지점을 데이터에서 찾기 위해
고객·상품·주문 데이터를 통합하고 RFM 세분화, 연관분석(Apriori),
협업 필터링, 회귀 기반 매출 예측을 한 흐름으로 수행한 데이터 분석 프로젝트.

## 진행 기간
청년 AI 빅데이터 아카데미 부트캠프 — 빅데이터 주간 (C반 과제: 유통·새벽배송 매출 증대)

## 역할
팀 프로젝트 — 부트캠프 산출물

> 본인 담당 영역: _(추후 본인이 채움)_

## 데이터
| 데이터 | 컬럼 |
|---|---|
| `on_users.csv` | idUser, Gender, Age, FamilyCount, MemberYN |
| `on_items.csv` | ItemLargeCode/Name, ItemMiddleCode/Name, ItemSmallCode/Name, ItemCode/Name, PriceYear/Min/Max |
| `on_orders.csv` | OrderID, idUser, OrderDate, ItemCode, Quantity, Spend (~75 MB) |

> 데이터는 부트캠프 제공 자료로 라이선스 사유로 본 저장소에 포함하지 않는다.
> 구조와 재현 방법은 [`data/README.md`](./data/README.md) 참고.

## 분석 흐름

| 단계 | 노트북 | 내용 |
|---|---|---|
| 1 | `notebooks/01_user_eda.ipynb` | 고객 마스터 EDA — 성별·연령·가구원수 분포 |
| 2 | `notebooks/02_member_eda.ipynb` | 멤버십 보유 여부에 따른 구매 패턴 차이 |
| 3 | `notebooks/03_item_eda.ipynb` | 상품 마스터 정제 + 카테고리·가격대 EDA |
| 4 | `notebooks/04_rfm_analysis.ipynb` | **RFM 세분화** — 5분위 점수 + PCA 기반 CV 가중치 + 4등급 부여 |
| 5 | `notebooks/05_association_analysis.ipynb` | **연관분석** — Apriori 기반 장바구니 규칙 도출 |
| 6 | `notebooks/06_collaborative_filtering.ipynb` | **협업 필터링** + 회귀 기반 매출 예측 (XGBoost·LightGBM·GBR 비교) |

## 기술 스택
| 영역 | 도구 |
|---|---|
| 데이터 처리 | pandas, numpy |
| 통계 | scipy (chi2_contingency, f_oneway), statsmodels |
| 시각화 | matplotlib, seaborn, squarify |
| 모델링 | scikit-learn (LinearRegression, DecisionTreeRegressor, RandomForestRegressor, GradientBoostingRegressor), xgboost, lightgbm |
| 연관 규칙 | mlxtend (Apriori) |

## 산출물
- 발표 보고서: [`docs/새벽배송_고객_구매_패턴_매출_증대_보고서.pdf`](./docs/새벽배송_고객_구매_패턴_매출_증대_보고서.pdf)
- RFM 등급이 부여된 고객 데이터: `data/processed/customer_rfm_pca.csv` (재현 시 생성)
- 개인 추천 결과: `data/processed/individual_cf_recommendations.csv` (재현 시 생성)

## 실행 방법
```bash
# 1. 의존성 설치
pip install -r requirements.txt

# 2. 부트캠프 제공 데이터를 data/raw/ 에 배치
#    - on_orders.csv, on_items.csv, on_users.csv

# 3. notebooks/ 의 01 → 06 순서대로 실행
jupyter notebook
```

## 디렉토리 구조
```
dawn-delivery-customer-analysis/
├── README.md
├── LICENSE
├── requirements.txt
│
├── notebooks/
│   ├── 01_user_eda.ipynb
│   ├── 02_member_eda.ipynb
│   ├── 03_item_eda.ipynb
│   ├── 04_rfm_analysis.ipynb
│   ├── 05_association_analysis.ipynb
│   └── 06_collaborative_filtering.ipynb
│
├── data/                       # gitignored (라이선스·100MB 제한)
│   ├── raw/
│   ├── processed/
│   └── README.md               # 데이터 구조·재현 방법
│
└── docs/
    └── 새벽배송_고객_구매_패턴_매출_증대_보고서.pdf
```

---
*원본 작업 폴더: 청년 AI 빅데이터 아카데미 부트캠프 — 빅데이터 주간 — C반 과제.*
