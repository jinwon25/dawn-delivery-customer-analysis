# data/

부트캠프 제공 데이터는 라이선스 사유로 본 저장소에 포함하지 않는다.
분석을 직접 재현하려면 동일 구조로 데이터를 채워야 한다.

## 데이터 출처
청년 AI 빅데이터 아카데미 (C반 과제: 유통 — 새벽배송 매출 증대) 제공 데이터.
2년치 새벽배송 거래·고객·상품 마스터.

## 폴더 구조

### `raw/`
부트캠프 원본 CSV 3종.

| 파일 | 컬럼 | 설명 |
|---|---|---|
| `on_orders.csv` | OrderID, idUser, OrderDate, ItemCode, Quantity, Spend | 주문 단위 거래 로그 (~75 MB) |
| `on_items.csv` | ItemLargeCode, ItemLargeName, ItemMiddleCode, ItemMiddleName, ItemSmallCode, ItemSmallName, ItemCode, ItemName, PriceYear, PriceMin, PriceMax | 상품 마스터 (대·중·소 분류 + 가격대) |
| `on_users.csv` | idUser, Gender, Age, FamilyCount, MemberYN | 고객 마스터 (성별·연령·가구원수·멤버십) |

### `processed/`
노트북이 생성하는 가공물. raw에서 재현 가능.

| 파일 | 생성 위치 | 설명 |
|---|---|---|
| `df_merged.csv` | (전처리 노트북) | orders + users + items 머지 결과 (대용량, 약 225 MB) |
| `clean_item.csv` | `03_item_eda.ipynb` | 상품 마스터 정제본 |
| `customer_rfm_pca.csv` | `04_rfm_analysis.ipynb` | RFM + PCA 가중치 기반 고객 등급 |
| `individual_cf_recommendations.csv` | `06_collaborative_filtering.ipynb` | 협업 필터링 기반 개인 추천 결과 |

## 인코딩
모든 CSV는 `cp949` 로 저장되어 있다. 노트북도 `read_csv(..., encoding='cp949')` 로 통일.
(예외: `individual_cf_recommendations.csv` 는 한국어 텍스트 출력 위해 `utf-8-sig` 로 저장)

## 재현 방법
1. `data/raw/` 에 `on_orders.csv`, `on_items.csv`, `on_users.csv` 배치
2. `notebooks/01_user_eda.ipynb` 부터 순서대로 실행
3. 머지 단계에서 `data/processed/df_merged.csv` 가 생성되면 04~06 노트북이 이를 참조
