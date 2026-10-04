# data/

부트캠프 제공 데이터는 라이선스 사유로 본 저장소에 포함하지 않는다.
분석을 직접 재현하려면 동일 구조로 데이터를 채워야 한다.

## 데이터 출처
청년 AI 빅데이터 아카데미 (C반 과제: 유통 — 새벽배송 매출 증대) 제공 데이터.
3년치 (2023-01-02–2025-12-29) 새벽배송 거래·고객·상품 마스터.

## 폴더 구조

### `raw/`
부트캠프 원본 CSV 3종.

| 파일 | 컬럼 | 설명 |
|---|---|---|
| `on_orders.csv` | OrderID, idUser, OrderDate, ItemCode, Quantity, Spend | 주문 단위 거래 로그 (약 75 MB) |
| `on_items.csv` | ItemLargeCode, ItemLargeName, ItemMiddleCode, ItemMiddleName, ItemSmallCode, ItemSmallName, ItemCode, ItemName, PriceYear, PriceMin, PriceMax | 상품 마스터 (대·중·소 분류 + 가격대) |
| `on_users.csv` | idUser, Gender, Age, FamilyCount, MemberYN | 고객 마스터 (성별·연령·가구원수·멤버십) |

### `processed/`
당시 분석에서 사용한 전처리본과 생성 산출물입니다. 현재 저장소에는 원본 3종을 `df_merged.csv`로 결합하는 독립 전처리 진입점이 포함되어 있지 않습니다. 병합 전처리본은 별도로 준비해야 합니다.

| 파일 | 생성 위치 | 설명 |
|---|---|---|
| `df_merged.csv` | 별도 준비 필요 | 거래·고객·상품 결합 전처리본. `01`, `02`, `04`–`06`의 입력 |
| `clean_item.csv` | `03_item_eda.ipynb` | 상품 마스터 정제본 |
| `customer_rfm_pca.csv` | `04_rfm_analysis.ipynb` | RFM + PCA 가중치 기반 고객 등급 |
| `individual_cf_recommendations.csv` | `06_collaborative_filtering.ipynb` | 협업 필터링 기반 개인 추천 결과 |

## 인코딩
노트북의 입력 CSV는 `encoding='cp949'`로 읽습니다. `03_item_eda.ipynb`의 `clean_item.csv` 출력은 pandas 기본 UTF-8이며 파일별 인코딩을 확인합니다.
(예외: `individual_cf_recommendations.csv` 는 한국어 텍스트 출력 위해 `utf-8-sig` 로 저장)

## 재현 방법
1. `data/raw/` 에 `on_orders.csv`, `on_items.csv`, `on_users.csv` 배치
2. 당시 정제·병합한 `data/processed/df_merged.csv`를 별도로 준비합니다. 실제 입력 컬럼은 `idOrder`, `OrderDT`, `Price` 등을 사용하며 위 원본 구조 표만으로 병합 규칙을 확정하지 않습니다.
3. `notebooks/`를 작업 경로로 노트북을 실행합니다. 원본 3종만으로 전체 결과가 자동 재현되는 구성은 아닙니다.
4. 원본·고객별 추천을 공개하지 않으며 기존 노트북의 저장 출력도 비웠습니다.
