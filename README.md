# DART BIG:IN

> **시장에서 산업으로, 산업에서 기업으로.** DART 공시·재무 데이터와 KRX 시장 데이터를 연결해 초보 투자자가 사업의 흐름을 근거와 함께 읽도록 돕는 Top-down 투자 리서치 서비스입니다.

단순한 데이터 시각화가 아니라, **금융 도메인 지식으로 산업별 재무 분석 체계를 설계**하고 **공시에서 실제 사업 변화를 나타내는 신호를 선별하는 산업·기업 워드클라우드 알고리즘을 구현**한 팀 프로젝트입니다. AI가 작성한 인사이트는 재무 데이터와 공시 원문을 역할에 맞게 분리해 사용하며, 화면에서 근거 공시까지 거슬러 올라갈 수 있습니다.

![DART BIG:IN 홈 화면](service/docs/screenshots/home.png)

## 프로젝트 개요

- **분석 범위:** 5개 산업, 25개 대표 기업
- **분석 기간:** 2023~2025년 정기보고서를 기본 범위로 사용하고, DB에 검증된 최신 분기가 있으면 같은 보고서 종류끼리 비교
- **사용자 흐름:** 시장 요약 → 산업 비교 → 대표 기업 상세 분석 → 공시 근거 확인
- **핵심 데이터:** DART 재무제표·공시 원문, KRX 산업 지수·구성종목, 기업 주가
- **핵심 분석:** 산업별 재무지표, 산업·기업 공시 신호, Gemini 인사이트, 문장별 원문 각주

| 산업 | 대표 기업 |
| --- | --- |
| 반도체 | SK하이닉스, 삼성전자, 한미반도체, 주성엔지니어링, 원익IPS |
| 자동차 | 기아, 현대자동차, 현대모비스, 한국타이어앤테크놀로지, HL만도 |
| 헬스케어 | 셀트리온, 알테오젠, 삼성바이오로직스, 유한양행, HLB |
| 철강 | 현대제철, 고려아연, POSCO홀딩스, 풍산, 에이치브이엠 |
| 은행·금융지주 | 하나금융지주, KB금융, 신한지주, 우리금융지주, 카카오뱅크 |

## 서비스 이용 흐름

```text
KRX 시장·산업 흐름
        ↓
5개 산업의 지수와 공시 신호 비교
        ↓
산업 대표기업의 재무지표와 공통 사업 변화 확인
        ↓
개별 기업의 재무 추이·고유 공시 신호·AI 인사이트 확인
        ↓
키워드 또는 각주 클릭 → 근거 공시 문단·표와 DART 원문 확인
```

산업과 기업 화면의 AI 문장은 페이지를 열 때마다 새로 생성하지 않습니다. 분석 명령이 DB와 공시 검색 결과로 보고서를 만들고 검증해 저장하면, 웹 서버가 저장 보고서와 최신 조회 데이터를 화면에 전달합니다.

## 주요 기능

| 화면·기능 | 제공 내용 |
| --- | --- |
| 홈 | 5개 산업의 KRX 지수 등락률과 산업 진입 동선 |
| 산업 분석 | 산업 지수, 공시 신호 워드클라우드, AI 산업 인사이트, 대표 5개 기업 재무 비교 |
| 기업 분석 | 주가, 기업 워드클라우드, AI 기업 인사이트, 분기별 재무 그래프 |
| 키워드 설명 | 선택한 공시 신호의 의미, 관련 공시, DART 원문 링크 |
| 공시 각주 | AI 문장을 뒷받침하는 원문 문단·표와 정확한 문서 위치 |
| 근거 검증 | 인용 ID, 원문 위치, 재무 수치, 데이터·임베딩 버전 계약 검사 |

| 산업 분석 | 기업 분석 |
| --- | --- |
| ![산업 분석 화면](service/docs/screenshots/industry.png) | ![기업 분석 화면](service/docs/screenshots/company.png) |

## 개인 기여 요약

이 저장소는 부트캠프 팀 프로젝트의 결과물입니다. 아래 항목은 제가 직접 설계·구현하거나 분석 원칙을 정립한 부분입니다.

1. **산업별 재무지표 선정과 4슬롯 그래프 설계** — 경제·금융적 의미와 실제 DB 커버리지를 함께 검토해 산업 간 비교 구조를 설계했습니다.
2. **산업 워드클라우드 알고리즘 설계·구현** — 단순 빈도가 아니라 현재성, 변화, 기업 간 확산을 평가하고 산업별 vocabulary와 노이즈 규칙을 적용했습니다.
3. **기업 워드클라우드 알고리즘 설계·구현** — 기업 내부의 현재성, 변화, 문맥 다양성을 평가하는 별도 점수 체계를 구현했습니다.
4. **데이터 품질 진단과 알고리즘 개선** — 표·회계 노이즈, 산업별 후보 편차, 구조적 결측, 누적값 차감 오류를 분석 로직에 반영했습니다.
5. **AI 인사이트 분석 원칙·프롬프트 설계** — 재무 수치와 공시 자연어의 역할을 분리하고, 근거 없는 인과 해석을 억제했습니다.
6. **UI 개선** — 산업 탐색 화면, 카드·차트·워드클라우드 표현과 Pretendard 기반 타이포그래피를 개선했습니다.

중앙 MySQL 인프라 구축, DART 원천 수집·적재 파이프라인, 서비스 백엔드의 전체 구현은 팀의 공동 결과이거나 다른 팀원의 담당 영역입니다. 저는 **읽기 전용 중앙 DB를 조회해 지표·워드클라우드·인사이트 분석 로직에 활용**했으며, DB 인프라 전체를 단독 구축한 것으로 표현하지 않습니다.

## 개인 기여 1 — 산업별 재무지표 선정과 그래프 설계

그래프는 백엔드가 주는 숫자를 그대로 그린 결과가 아닙니다. 먼저 산업의 성장성·수익성·투자 또는 건전성·재무 여력을 설명할 후보 지표를 정하고, 실제 DB에서 기업·기간별 값의 존재 여부와 재무제표 기준을 확인한 뒤 비교 가능한 지표만 채택했습니다.

### 최종 확정된 4슬롯 구성

| 산업 | 성장성 | 수익성 | 투자·건전성 | 재무 여력 |
| --- | --- | --- | --- | --- |
| 반도체 | 매출 지수 | 영업이익률 | CAPEX / 매출액 | FCF Margin |
| 자동차 | 매출 지수 | 영업이익률 | CAPEX / 매출액 | FCF Margin |
| 헬스케어 | 매출 지수 | 영업이익률 | R&D / 매출액 | FCF Margin |
| 철강 | 매출 지수 | 영업이익률 | CAPEX / 매출액 | FCF Margin |
| 은행·금융지주 | 순이자이익 지수 | ROE | 대손비용률 추정치 | 자기자본비율 |

### 일반 산업의 계산과 선정 이유

- **매출 지수** = 당기 분기 매출액 ÷ 각 기업의 가장 이른 기준 분기 매출액 × 100  
  각 기업의 기준 분기를 100으로 놓고 이후 매출이 기준점에서 얼마나 늘거나 줄었는지 보여줍니다. 기업마다 절대 매출 규모가 다르므로 지수화를 통해 규모 차이를 제거하고 각 기업의 성장 경로를 같은 출발점에서 비교합니다. 기준값이 없거나 0 이하이거나 비교 기간의 재무제표 기준이 다르면 임의의 지수를 만들지 않고 결측으로 둡니다.
- **영업이익률** = 분기 영업이익 ÷ 분기 매출액 × 100  
  외형 성장과 본업의 수익성을 분리합니다.
- **CAPEX/매출액** = 분기 유형자산 취득액 ÷ 분기 매출액 × 100  
  반도체·자동차·철강 기업이 생산설비와 유형자산에 투입한 투자 강도를 매출 규모에 맞춰 비교합니다.
- **R&D/매출액** = 분기 연구개발비 ÷ 분기 매출액 × 100  
  헬스케어 기업이 신약·바이오 제품의 연구개발에 투입한 비용을 매출 규모에 맞춰 비교합니다. 비율 변화가 연구개발비 증가뿐 아니라 매출 변화에서도 발생할 수 있으므로 실제 금액과 함께 해석합니다.
- **FCF** = 분기 영업활동현금흐름 − 분기 CAPEX  
  **FCF Margin** = FCF ÷ 분기 매출액 × 100. 본업 현금흐름에서 설비투자 후 남는 여력을 봅니다.

누적값만 있는 경우 `H1-Q1`, `Q3-H1`, `FY-Q3`으로 분기값을 복원합니다. 연간값을 단순히 4로 나누지 않으며, 필요한 선행 기간이 없거나 개별 분기의 합으로 검증할 수 없으면 값을 만들지 않습니다.

### 은행·금융지주를 별도로 설계한 이유

은행은 제조업의 매출·CAPEX 구조로 비교하기 어렵기 때문에 별도 지표 체계를 사용합니다.

- **순이자이익 지수** = 당기 분기 순이자이익 ÷ 각 기업의 가장 이른 기준 분기 순이자이익 × 100  
  기준 분기의 순이자이익을 100으로 놓아 절대 규모가 다른 은행들의 이익 성장 경로를 상대적으로 비교합니다. 기준값이 없거나 재무제표 기준이 달라 비교할 수 없으면 결측으로 둡니다.
- **ROE** = 연환산 분기 순이익 ÷ 평균 자기자본 × 100
- **대손비용률 추정치** = 연환산 신용손실비용 ÷ 평균 대출채권 × 100
- **자기자본비율** = 기말 자본총계 ÷ 기말 자산총계 × 100

금융지주 4개사는 연결 기준(CFS), 카카오뱅크는 별도 기준(OFS)을 사용하는 비교 정책을 적용합니다. 대손비용률은 공시 재무 DB로 계산한 **추정 지표**이지 은행이 발표한 공식 대손비용률이 아니며, 자기자본비율도 BIS·CET1과 다른 재무제표 기반 비율입니다. NIM·BIS·CET1·NPL은 25개 기업·전체 기간의 커버리지를 확인하지 않은 상태에서 화면 지표로 사용하지 않았습니다.

### 헬스케어 R&D 지표의 데이터 검증

헬스케어는 산업 특성상 설비투자보다 연구개발 활동을 직접 보여주는 지표가 중요하다고 판단해 **R&D/매출액**을 사용합니다. 현재 구현은 검토·승인된 문서 단위 `RND_EXPENSE`를 우선 조회하고, 같은 재무제표 범위에서 확인되는 손익계산서 연구개발비 계정을 제한적으로 보완합니다. 연결 기준에는 연결 범위, 별도 기준에는 별도 범위의 값만 사용해 서로 다른 보고 범위를 섞지 않습니다.

누적 연구개발비에서 분기값을 복원할 때 음수 차감값이 발생하면 보고 범위가 달라졌을 가능성이 있으므로 비율을 만들지 않습니다. 값이 없거나 하나로 확정할 수 없는 기간은 억지로 채우지 않고 결측으로 남깁니다. CAPEX도 원천 부호, 직접 계정과 세부 계정 합산의 중복, 누적값 차감에서 생기는 음수 파생값을 별도로 점검했습니다. 즉, 지표 선정과 계산은 다음을 함께 만족해야 했습니다.

- 산업의 경제적 의미를 설명하는가
- 대표 5개사를 같은 기준으로 비교할 수 있는가
- CFS/OFS, 기간, 단위와 원천 문서를 추적할 수 있는가
- 결측이나 음수 파생값을 억지로 정상값처럼 만들지 않는가

## 개인 기여 2 — 산업 워드클라우드 알고리즘

산업 워드클라우드는 공시에 자주 등장한 단어 목록이 아닙니다. **최근에 중요하고, 과거보다 증가했으며, 한 기업에만 몰리지 않고 여러 대표기업으로 확산된 사업 신호**를 찾습니다. 구현은 [`dart_signal_wordcloud.py`](service/dart_remote/dart_signal_wordcloud.py), 공통 규칙은 [`signal_keyword_rules.py`](service/dart_remote/signal_keyword_rules.py)에 있습니다.

### 후보 추출과 정제

1. 현재 검증 데이터 버전의 검색 가능한 DART 공시 청크에서 사업 관련 섹션만 읽습니다.
2. Kiwi 형태소 분석으로 일반명사·고유명사·영문 후보를 추출합니다.
3. 표 머리글, 측정 단위, 회계 계정명, 문서 필드, 계약 절차 문구, 홍보성·추상 표현을 제거합니다.
4. 반복 문구와 포함 관계를 정리하고 복합어·alias를 하나의 표기로 정규화합니다.
5. 의미가 약한 짧은 영문, 기업명·조직명, 최신 연도에서 지지가 부족한 후보를 억제합니다.
6. 공통 필터가 산업 핵심어까지 지우지 않도록 섹터별 vocabulary를 보호합니다.

실제 코드에 등록된 예시는 다음과 같습니다.

| 산업 | 보호·정규화하는 용어 예시 |
| --- | --- |
| 반도체 | HBM, SSD, GDDR, EUV, 파운드리 |
| 자동차 | EV, HEV, PHEV, 회생 제동, SDV, ADAS |
| 헬스케어 | FDA, CMC, 후보물질, 라이선스계약, 바이오시밀러 |
| 철강 | 합금, 후판, 전기로, 특수강, 제련 |
| 은행 | 기업금융, 담보대출, MMF, 자산관리, 신용위험 |

### 산업 점수

- **Current**: 최신 비교 기간의 전체 청크 중 해당 키워드가 등장한 비율의 백분위 점수
- **Change**: 실제 데이터가 있는 연속 기간의 언급률 변화. 여러 변화 구간은 이전 40%, 최근 60%로 순차 결합
- **CompanyCoverage**: 최신 기간에 키워드를 언급한 기업 수 ÷ 분석 기업 수 × 100
- **EntropyScore**: 기업별 공시량을 보정한 언급률이 기업들 사이에 얼마나 고르게 분산됐는지 나타내는 0~100 정규화 엔트로피

```text
SpreadScore = 0.60 × CompanyCoverage + 0.40 × EntropyScore

SignalScore = 0.50 × CurrentScore
            + 0.30 × ChangeScore
            + 0.20 × SpreadScore

FinalScore  = SignalScore
            − concentration_penalty
            − generic_business_penalty
```

최신 언급의 50%를 넘게 한 기업이 차지하면 최대 15점의 집중도 패널티를 부여하고, 지나치게 일반적인 사업 용어에는 2점을 감점합니다. 최종 점수 상위 12개를 반환하며 후보가 부족하면 존재하는 만큼만 반환합니다.

**HOT**은 단순히 최종 점수가 높은 단어가 아닙니다. 최종 Top12 안에서 `ChangeScore ≥ 90`이고 실제 변화량이 양수인 후보를 변화량 순으로 정렬해 최대 3개만 표시합니다.

## 개인 기여 3 — 기업 워드클라우드 알고리즘

기업 워드클라우드는 같은 후보 추출·정제 엔진과 산업 vocabulary를 공유하지만 목적이 다릅니다. 산업 분석이 **기업 간 확산**을 본다면, 기업 분석은 **한 기업 안에서 서로 다른 공시 문맥에 반복해서 등장하는 고유 신호**를 봅니다. 구현은 [`dart_company_signal_wordcloud.py`](service/dart_remote/dart_company_signal_wordcloud.py)에 있습니다.

- **Current**: 해당 기업의 최신 공시에서의 언급 수준
- **Change**: 해당 기업 내부의 과거 대비 언급률 변화
- **Context Diversity**: 같은 키워드가 서로 다른 문장 문맥과 공기어 조합에서 나타나는 정도

```text
C2 = 고유 문맥 signature 수 ÷ 최신 키워드 청크 수
C3 = 고유 공기어 조합 수 ÷ 최신 키워드 청크 수

DiversityRaw = 0.40 × C2 + 0.60 × C3
support      = min(1, 최신 문맥 수 ÷ 10)
DiversityScore = percentile(DiversityRaw × support)

FinalScore = 0.50 × CurrentScore
           + 0.30 × ChangeScore
           + 0.20 × DiversityScore
           − generic_business_penalty
```

기업별 후보를 만든 뒤 포함 관계와 구체성, 최신 문맥 지지 여부를 다시 검사하고 최종 Top12를 선택합니다. 후보가 12개보다 적으면 억지로 채우지 않습니다. 기업 **HOT**은 Top12 안에서 `ChangeScore ≥ 97.5`, 실제 변화량이 양수인 후보 중 최대 3개입니다.

## 개인 기여 4 — 데이터 품질과 알고리즘 개선

### 빈도 중심 추출에서 사업 신호 중심 추출로

초기 빈도 방식은 표 머리글, 회계 상투어, 기업 고유 조직명처럼 자주 나오지만 해석 가치가 낮은 단어를 상위에 올렸습니다. 이를 해결하기 위해 생산 코드에 다음 계층을 더했습니다.

- 표·측정·문서 필드·회계 계정 표현의 범주별 노이즈 필터
- 복합어와 alias의 정규화, 더 구체적인 구가 있을 때 단일 구성어 억제
- 산업별 vocabulary 보호와 문맥이 필요한 단어의 단독 노출 제한
- 산업 결과의 기업 집중도 패널티와 엔트로피 기반 확산 점수
- 기업 결과의 문맥·공기어 다양성 및 최소 지지도 반영
- 최종 후보 안에서만 HOT을 선정해 불꽃 표시가 순위를 우회하지 못하도록 제한

### 구조적 결측을 0으로 만들지 않기

신규 상장·신규 편입 기업은 과거 보고서가 존재하지 않을 수 있습니다. 에이치브이엠은 상장 전인 2023년 전체와 2024년 1분기 데이터가 없는 사례입니다. 이때 없는 연도를 0회 언급으로 만들면 모든 최신 단어가 급증한 것처럼 보입니다.

```yaml
2023: 없음        # 0으로 생성하지 않음
2024: 실제 자료 있음
2025: 실제 자료 있음
Change: 2024 → 2025만 계산
```

변화율은 실제 데이터가 있고 보고서 종류가 비교 가능한 연속 기간만 사용합니다. 최신 연도가 반기까지만 있다면 전년의 같은 Q1·H1과 비교합니다. 이는 특정 기업명을 하드코딩한 예외가 아니라 모든 구조적 결측에 적용하는 공통 규칙입니다.

### 재무 품질 방어

- 분기값은 직접 분기값을 우선하고, 누적값 차감이 검증될 때만 파생합니다.
- 연구개발비 누적값 차감에서 음수 파생값이 나오면 보고 범위 변경 가능성이 있으므로 화면 비율에 사용하지 않습니다.
- CAPEX 누적값 차감에서 음수 파생값이 나오면 원천 부호, 보고 범위 변경과 계정 구성을 다시 확인하고 자동으로 정상 투자액처럼 사용하지 않습니다.
- CAPEX의 직접 계정과 세부 취득 계정을 중복 합산하지 않고, 원천 부호와 서비스용 지출 규모를 구분합니다.
- 필요한 값, 재무 기준, 단위 또는 근거가 맞지 않으면 추정값을 만들지 않고 결측으로 둡니다.

## 개인 기여 5 — AI 인사이트 설계

산업·기업·키워드 인사이트의 프롬프트는 “그럴듯한 설명”보다 **근거의 역할과 해석의 경계**를 먼저 정의합니다.

- 재무 변화 자체의 근거는 정규화된 재무 데이터가 담당합니다.
- 사업 활동, 제품, 투자 계획과 전략은 공시 자연어로 설명합니다.
- 함께 나타났다는 이유만으로 재무 변화와 사업 활동을 인과관계로 단정하지 않습니다.
- 산업 공통 흐름과 개별 기업의 차이를 분리합니다.
- 일반적인 기업 소개보다 최근 실적과 사업 변화에 집중합니다.
- 중요도에 따라 핵심 신호를 선택해 1~3문장으로 압축하고, 적격 근거가 없으면 빈 결과와 사유를 반환합니다.

검색은 BGE-M3가 담당하고 문장 생성은 Gemini가 담당합니다. Gemini가 DB 전체를 직접 탐색하지 않습니다. 서비스 코드가 분석 범위와 재무 근거를 정하고 관련 공시 청크를 검색한 뒤, 생성 결과의 인용 ID·원문 위치·수치 연결을 다시 검사합니다.

## 전체 시스템 구조

```text
데이터 계층(팀)                                            사용자 서비스

OpenDART ─▶ 수집·원본 보존 ─▶ 기간·계정 표준화 ─┐
                                                   ├─▶ 중앙 MySQL(검증 버전)
공시 XML ─▶ 섹션 청킹 ─▶ BGE-M3 임베딩 ──────────┘          │ SELECT only
                                                            ▼
KRX OpenAPI ───────────────────────────────────────▶ Python API·분석 로직
                                                            │
                              ┌─────────────────────────────┼─────────────────────┐
                              ▼                             ▼                     ▼
                       재무 4슬롯 계산             워드클라우드 점수       BGE 검색 → Gemini
                              └─────────────────────────────┼─────────────────────┘
                                                            ▼
                                                HTML / CSS / JavaScript UI
```

서비스 DB 모듈은 읽기 전용 트랜잭션과 `SELECT`만 허용합니다. 검증을 통과한 현재 데이터 버전과 임베딩 계약을 확인한 뒤 조회하며, 서비스 결과·캐시는 원천 DB를 수정하지 않습니다.

## 기술 스택

| 영역 | 기술 |
| --- | --- |
| Language·Data | Python, pandas, NumPy |
| Database | SQL, MySQL 8, SQLAlchemy, PyMySQL |
| Source | OpenDART API·공시 XML, KRX OpenAPI, FinanceDataReader |
| NLP·Signal | Kiwi(`kiwipiepy`), 정규식·규칙 기반 정제, 섹터 vocabulary |
| Embedding·Search | `BAAI/bge-m3`, 1,024차원 정규화 dense vector, NumPy/FAISS cosine search |
| AI | RAG, Google Gemini, 구조화 응답·인용 검증 |
| Frontend | HTML, CSS, Vanilla JavaScript, SVG 차트·워드클라우드 |
| Quality | `unittest`, Node 기반 UI 테스트, 데이터·벡터 무결성 검사 |

## 프로젝트 구조

```text
.
├─ pipeline/                         # 팀 데이터 계층
│  ├─ src/collect, preprocess        # DART 수집·정제·청킹
│  ├─ src/db, mapping, retrieval     # 표준화 DB·임베딩·검색 자산
│  ├─ src/quality                    # 데이터·검색 품질 검사
│  ├─ infra/mysql                    # MySQL 스키마·migration·동기화
│  └─ README.md                      # 파이프라인 상세 실행법
├─ service/
│  ├─ app.py                         # 로컬 HTTP 서버와 API
│  ├─ snapdart/                      # 분석 실행·보고서·화면 데이터 조립
│  ├─ dart_remote/
│  │  ├─ graph_metrics.py            # 산업별 4슬롯 재무지표
│  │  ├─ dart_signal_wordcloud.py    # 산업 워드클라우드
│  │  ├─ dart_company_signal_wordcloud.py # 기업 워드클라우드
│  │  ├─ signal_keyword_rules.py     # 공통·산업별 후보 규칙
│  │  └─ mysql_vectors.py            # BGE-M3 벡터 검색
│  ├─ web/                           # HTML/CSS/JavaScript UI
│  ├─ tests/                         # 서비스·UI 회귀 테스트
│  └─ docs/4차구상/                  # 서비스 상세 설명서
└─ README.md
```

## 설치 및 환경설정

Python 3.12와 MySQL 접속 권한이 필요합니다. 공개 저장소에는 `.env`, 인증서, API 키를 포함하지 않습니다.

### Windows PowerShell

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip

# 사용자 서비스만 실행
python -m pip install -r service\requirements.txt

# 파이프라인 도구까지 함께 사용할 경우(서비스 의존성 포함)
# python -m pip install -r pipeline\requirements.txt
```

### Linux / macOS

```bash
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip

# 사용자 서비스만 실행
python -m pip install -r service/requirements.txt

# Linux에서 FAISS 검색을 사용할 경우
python -m pip install faiss-cpu
```

`service/.env`를 직접 만들고 아래처럼 값을 채웁니다. 저장소에는 실제 주소·계정·비밀번호·키를 커밋하지 않습니다.

```dotenv
# 중앙 MySQL: 서비스용 읽기 전용 계정 사용
MYSQL_HOST=<db-host>
MYSQL_PORT=3306
MYSQL_DATABASE=<database>
MYSQL_USER=<read-only-user>
MYSQL_PASSWORD=<password>

# 선택: TLS 또는 Cloud SQL Connector
# MYSQL_SSL_CA=<absolute-path-to-ca.pem>
# CLOUD_SQL_INSTANCE=<project:region:instance>
# CLOUD_SQL_IP_TYPE=PUBLIC

# 외부 서비스
GEMINI_API_KEY=<gemini-api-key>
KRX_API=<krx-open-api-key>
OPENDART_API_KEY=<opendart-api-key>

# Windows 기본값은 numpy, Linux 기본값은 faiss
SEARCH_BACKEND=numpy

# 선택 설정
# BGE_M3_DEVICE=cpu
# BGE_M3_CACHE_DIR=<model-cache-directory>
# DART_CACHE_DIR=<vector-cache-directory>
# HF_TOKEN=<hugging-face-token>
# REPORT_PROMPT_VERSION=new
# INSIGHT_VALIDATION_MODE=mvp
# UI_VERSION=new
```

기존 배포 환경의 `SQL_HOST_NAME`, `SQL_PORT`, `SQL_USER_NAME`, `SQL_DEFAULT_SCHEMA`, `SQL_PSWD`도 호환되지만 새 로컬 설정에는 `MYSQL_*` 이름을 권장합니다. `SERVICE_DATA_VERSION`은 특별히 검증된 과거 버전을 선택할 때만 사용하며, 보통 비워 두어 현재 검증 버전을 선택합니다.

## DB 접속과 데이터 조회

### 연결 원칙

- 서비스는 `service/.env` 또는 프로세스 환경변수를 읽습니다.
- `MYSQL_USER`, `MYSQL_DATABASE`는 필수이며 호스트·비밀번호는 배포 방식에 맞게 제공합니다.
- 모든 쿼리는 읽기 전용 트랜잭션에서 실행되고, 코드 수준에서도 `SELECT` 이외 문장을 거부합니다.
- `data_versions.is_current`와 임베딩 메타데이터 계약을 확인해 검증된 버전만 사용합니다.
- 원격 DB 주소나 자격 증명은 README·소스·명령행 인수에 직접 적지 않습니다.

### 서비스 API로 조회

서버 실행 후 재무 데이터와 공시 검색을 같은 읽기 전용 경로로 확인할 수 있습니다.

```text
# 삼성전자 2025년 사업보고서 연결 재무 데이터
GET /api/financial?sector=반도체&code=005930&year=2025&report_type=FY&basis=CFS

# 반도체 공시에서 HBM 수요 관련 상위 5개 청크
GET /api/search?sector=반도체&q=HBM%20수요&year=2025&top_k=5
```

재무 응답은 기업·연도·보고서·CFS/OFS·값 유형을 구분합니다. 공시 검색 결과는 `chunk_id`, 기업·연도·보고서, 섹션, 원문 위치와 검색 점수를 유지해 각주가 원본 XML로 이어지게 합니다. 세부 스키마와 조회 계약은 [DB 스키마](pipeline/docs/handoff/DB_SCHEMA_20261011.md), [백엔드 인터페이스](pipeline/docs/handoff/BACKEND_INTERFACE_SPEC.md), [서비스 데이터 조회 설명](service/docs/4차구상/01_서비스구조와데이터조회.md)을 참고하세요.

## 임베딩 및 벡터 검색 환경

현재 검색 모델 계약은 다음과 같습니다.

- **Model:** `BAAI/bge-m3`
- **Revision:** `5617a9f61b028005a4858fdac845db406aefb181`
- **Dimension:** 1,024
- **Normalization:** L2 정규화
- **Similarity:** inner product로 계산하는 cosine similarity
- **Backend:** Windows 기본 NumPy, Linux 기본 FAISS `IndexFlatIP`
- **검색 범위:** 먼저 기업·연도·보고서·현재 데이터 버전으로 후보를 제한한 뒤 dense exact search

질문과 저장 청크는 같은 모델·리비전·차원·정규화 계약을 사용해야 합니다. 서비스 시작 후 첫 검색에서는 벡터 스냅샷을 내려받아 무결성을 확인하고 로컬 캐시에 보관할 수 있으므로 시간이 걸릴 수 있습니다.

```powershell
cd service

# 검색 CLI
python -X utf8 -m dart_remote.mysql_vectors "HBM 수요와 설비투자 확대 계획" --sector 반도체 --top-k 5

# 산업·기업 워드클라우드 진단
python -X utf8 -m dart_remote.dart_signal_wordcloud KRX_SEMI --top-n 12 --keyword HBM
python -X utf8 -m dart_remote.dart_company_signal_wordcloud 00126380 --sector-index KRX_SEMI
```

세부 점수·출력 계약은 [워드클라우드 README](service/dart_remote/README_WORDCLOUD.md), 모델 선정과 검증은 [BGE-M3/FAISS 설계](pipeline/docs/vector/BGE_M3_FAISS_DESIGN.md)와 [검색 벤치마크](pipeline/docs/vector/VECTOR_RETRIEVAL_BENCHMARK_V2.md)를 참고하세요.

## 실행 방법

### 1. 시장 데이터 갱신(선택)

```powershell
cd service
python -X utf8 -m snapdart.market
```

`KRX_API`가 없거나 외부 호출 없이 기존 저장값을 사용하려면 이 단계를 생략하고 웹 서버에 `--no-market-refresh`를 지정합니다.

### 2. 분석 보고서 생성

```powershell
# 전체 섹터 Gemini 분석
python -X utf8 -m snapdart.analyze --llm --prompt-version new

# 한 섹터만 생성
python -X utf8 -m snapdart.analyze --llm --sector 반도체 --prompt-version new2

# 외부 LLM 호출 없는 규칙 기반 점검
python -X utf8 -m snapdart.analyze --offline --sector 반도체
```

지원 프롬프트 버전은 `new`, `new2`, `old`입니다. 새 프롬프트 버전은 기존 생성 캐시와 분리됩니다.

### 3. 웹 서버 실행

```powershell
python -X utf8 app.py --ui-version new --prompt-version new --no-market-refresh
# http://127.0.0.1:8501
```

저장 시세를 쓰지 않으려면 `--no-market-refresh`를 빼고 `KRX_API`를 설정합니다. 한 산업만 띄우려면 `--sector 반도체`, 포트를 바꾸려면 `--port 8502`를 추가합니다.

### 4. 테스트

```powershell
# service 디렉터리에서
python -B -X utf8 -m unittest discover -s tests -p "test_*.py"
python -B -X utf8 -m unittest discover -s dart_remote -t . -p "test_*.py"

# Node.js가 설치된 경우 UI 회귀 테스트
node tests/test_ui.cjs
```

파이프라인 재구축과 MySQL 동기화는 서비스 실행과 별도입니다. 필요한 경우 [pipeline/README.md](pipeline/README.md)와 [MySQL 구축 문서](pipeline/infra/mysql/README.md)를 따르세요.

## 자주 발생하는 문제

| 증상 | 확인 및 해결 |
| --- | --- |
| `MySQL 접속 환경변수를 설정하세요.` | `service/.env`의 `MYSQL_USER`, `MYSQL_DATABASE`와 호스트·비밀번호를 확인합니다. `.env`는 `service/` 또는 저장소 루트에서 읽습니다. |
| DB 연결 시간 초과 | DB 방화벽·VPN·SSH 터널·Cloud SQL 접근 권한과 `MYSQL_HOST`, `MYSQL_PORT`를 확인합니다. 서비스는 연결 15초, 읽기 90초 제한을 사용합니다. |
| Linux에서 `faiss` import 오류 | `faiss-cpu`를 설치하거나 `SEARCH_BACKEND=numpy`로 실행합니다. Windows는 기본적으로 NumPy를 사용합니다. |
| BGE-M3 모델/벡터 불일치 | 모델 리비전·1,024차원·정규화 설정과 현재 DB의 `embedding_metadata`가 일치하는지 확인하고 손상된 로컬 벡터 캐시를 재생성합니다. |
| `DB 청크 개수와 검증된 벡터 개수가 다릅니다.` | 청크·임베딩 동기화가 끝난 검증 버전을 사용해야 합니다. 임의로 검사를 우회하지 말고 DB 버전 담당자에게 동기화 상태를 확인합니다. |
| Gemini 분석 실패 | `GEMINI_API_KEY`, 할당량, 네트워크를 확인합니다. UI·DB 점검만 필요하면 `--offline`을 사용합니다. |
| KRX 갱신 실패 | `KRX_API` 승인 상태를 확인하거나 `--no-market-refresh`로 기존 저장 시세를 사용합니다. 실패 시 기존 자료를 덮어쓰지 않습니다. |
| 첫 화면이 계속 로딩됨 | 브라우저 Console의 JavaScript 오류와 Network의 `/api/project` 요청 여부를 먼저 확인합니다. 요청 전 실패는 UI, 요청 후 지연은 DB·서버 조회 문제로 나누어 진단합니다. |
| 보고서가 없다는 503 응답 | 먼저 `python -X utf8 -m snapdart.analyze ...`로 해당 프롬프트 버전의 보고서를 생성합니다. |
| 2026년처럼 최신 연도가 일부 분기만 존재 | 같은 보고서 종류끼리 비교하며 없는 기간을 0으로 만들지 않습니다. 결측은 데이터 오류와 구분해 화면에서 비워 둡니다. |

상세 실행·배포·진단 순서는 [실행·배포·점검 문서](service/docs/4차구상/07_실행배포와점검.md)를 참고하세요.

## 팀 협업과 역할 구분

| 구분 | 범위 |
| --- | --- |
| **개인 기여** | 산업별 재무지표 선정과 그래프 구조, 산업·기업 워드클라우드 점수·후보 규칙, 결측·노이즈 품질 개선, AI 분석 원칙과 프롬프트, UI 개선 |
| **팀 공동 결과** | 5개 산업·25개 기업 서비스 기획, 데이터·서비스 인터페이스 정의, 통합 테스트와 결과 검토 |
| **팀 데이터/백엔드 영역** | OpenDART 원천 수집·표준화·중앙 MySQL 인프라, 공시 원문·임베딩 적재, 서비스 API·원문 뷰어 등 전체 백엔드 기반 |

개인 기여는 중앙 DB를 **읽고 검증해 분석 로직에 반영한 역할**과, DB 수집·인프라 자체를 구축한 역할을 구분해 기술했습니다.

## 더 자세한 문서

- [서비스 구현 설명서](service/docs/4차구상/README.md): 데이터 조회부터 인사이트·화면까지 전체 흐름
- [워드클라우드 production README](service/dart_remote/README_WORDCLOUD.md): 점수, CLI, JSON 출력 계약
- [재무지표와 원문 출처](service/docs/4차구상/05_재무지표와원문출처.md): 분기값·산업별 지표·각주 계산
- [인사이트 생성과 프롬프트](service/docs/4차구상/03_인사이트생성과프롬프트.md): Gemini 입력·출력·검증 원칙
- [DB 스키마](pipeline/docs/handoff/DB_SCHEMA_20261011.md): 테이블과 버전 구조
- [데이터 파이프라인 README](pipeline/README.md): 수집·정제·임베딩·품질검사 상세

