# 퇴직연금 포트폴리오 분석 결과

**생성일**: 2026-01-21 23:05:00
**세션 ID**: dc7f2a
**워크플로우**: Multi-Agent Portfolio Analysis v3.0

---

## 검증 상태 요약

| 항목 | 상태 | 상세 | 보고서 |
|------|:----:|------|--------|
| 거시경제 분석 | PARTIAL | 웹검색 API 제한으로 참조값 사용 | [00-macro-outlook.md](./00-macro-outlook.md) |
| 펀드 분석 | DONE | 2,015개 펀드 기반 분석 완료 | [01-fund-analysis.md](./01-fund-analysis.md) |
| 규제 준수 (Compliance) | PASS | 위험자산 65% (한도 70% 이내) | [02-compliance-report.md](./02-compliance-report.md) |
| 데이터 검증 | PASS (조건부) | 신뢰도 72점 (C등급) | [03-output-verification.md](./03-output-verification.md) |
| 출처 검증 | PARTIAL | 로컬 데이터 검증됨, 거시경제 미검증 | [03-output-verification.md](./03-output-verification.md) |

---

## 투자자 프로필

| 항목 | 내용 |
|------|------|
| **투자 성향** | 중립형 (Moderate) |
| **투자 목표** | 장기 은퇴 자산 형성 |
| **계좌 유형** | DC형 퇴직연금 (과학기술인공제회) |
| **분석 기준일** | 2026-01-21 |
| **데이터 기준일** | 2026-01-01 (fund_data.json, 2,015개 펀드) |
| **데이터 경과일** | 20일 (FRESH) |

---

## 시장 전망 요약 (macro-outlook)

[출처: 00-macro-outlook.md - 참조값, 실시간 검증 권장]

| 권고 항목 | 권고 | 실제 반영 |
|----------|------|----------|
| 위험자산 비중 | 60-65% | 65% |
| 환헤지 전략 | 50:50 분산 | 환노출 중심 (국내채권 35%) |
| 주목 섹터 | 반도체/AI, 에너지/전력 | 반도체 15%, 전력 10% |
| 지역 배분 | 미국 50-55%, 한국 25-30% | 미국 35%, 한국 65% |

**주의**: 거시경제 데이터는 웹검색 API 제한으로 실시간 검증되지 않았습니다. 투자 결정 전 최신 시세를 확인하세요.

---

## 추천 포트폴리오

### 포트폴리오 구성

| # | 펀드명 | 비중 | 유형 | 역할 | 위험자산 |
|:-:|--------|:----:|------|------|:--------:|
| 1 | 미래에셋TIGER미국S&P500증권상장지수투자신탁(주식) | **20%** | 해외주식형 | Core (미국) | O |
| 2 | 미래에셋TIGER반도체TOP10증권상장지수투자신탁(주식) | **15%** | 주식형 | Satellite (반도체) | O |
| 3 | 삼성KODEXAI전력핵심설비증권상장지수투자신탁[주식] | **10%** | 주식형 | Satellite (에너지) | O |
| 4 | 삼성KODEX200증권상장지수투자신탁[주식] | **10%** | 주식형 | Core (한국) | O |
| 5 | 미래에셋퇴직연금배당커버드콜액티브증권자투자신탁1호(주식혼합) | **10%** | 주식혼합형 | Income | O |
| 6 | 키움더드림단기채증권투자신탁[채권]C-P2e(퇴직연금) | **20%** | 채권형 | 안전자산 | X |
| 7 | 한국투자크레딧포커스ESG증권자투자신탁 1(채권)(C-Re) | **15%** | 채권형 | 안전자산 | X |
| | **합계** | **100%** | | | |

### 위험자산 분포

| 구분 | 비중 | 한도 | 상태 |
|------|:----:|:----:|:----:|
| **위험자산** | 65% | 70% | PASS |
| **안전자산** | 35% | 30%+ | PASS |
| **한도 여유** | 5%p | - | - |

---

## 포트폴리오 특성

### 핵심-위성 전략

```
┌─────────────────────────────────────────────────────────────┐
│                     포트폴리오 구조 (100%)                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Core (핵심) 30%          │  Satellite (위성) 25%           │
│  ├─ S&P500 20%            │  ├─ 반도체TOP10 15%             │
│  └─ KODEX200 10%          │  └─ AI전력설비 10%              │
│                           │                                 │
│  Income (인컴) 10%        │  안전자산 35%                    │
│  └─ 배당커버드콜 10%       │  ├─ 단기채 20%                  │
│                           │  └─ 크레딧ESG 15%               │
└─────────────────────────────────────────────────────────────┘
```

### 주요 펀드 수익률 (fund_data.json 기준)

| 펀드 | 1년 수익률 | 출처 |
|------|:---------:|------|
| 미래에셋TIGER반도체TOP10 | **121.14%** | fund_data.json |
| 삼성KODEXAI전력핵심설비 | **151.44%** | fund_data.json |

*주: 과거 수익률은 미래 수익률을 보장하지 않습니다.*

---

## Compliance 검증 결과 (원본)

[출처: 02-compliance-report.md]

```json
{
  "compliance": true,
  "violations": [],
  "warnings": [
    {
      "rule": "RISK_NEAR_LIMIT",
      "message": "위험자산 65% (한도 70%의 93% 사용)",
      "severity": "warning"
    }
  ],
  "summary": {
    "totalWeight": 100,
    "riskAssetWeight": 65,
    "safeAssetWeight": 35,
    "fundCount": 7,
    "maxSingleFundWeight": 20
  }
}
```

---

## Output-Critic 검증 결과 (원본)

[출처: 03-output-verification.md]

```json
{
  "verified": true,
  "confidence_score": 72,
  "grade": "C",
  "issues": [
    {
      "type": "SOURCE_INCOMPLETE",
      "description": "거시경제 지수 데이터 실시간 검증 불가 (웹검색 API 제한)",
      "severity": "medium"
    }
  ],
  "recommendations": [
    "과학기술인공제회 포털에서 최신 시세 확인",
    "한국은행/Fed 공식 사이트에서 금리 확인"
  ]
}
```

---

## 발견된 이슈

| # | 유형 | 설명 | 심각도 |
|:-:|------|------|:------:|
| 1 | SOURCE_INCOMPLETE | 거시경제 데이터 실시간 검증 불가 | MEDIUM |
| 2 | FEE_DATA_PARTIAL | 일부 펀드 총보수 추정치 사용 | LOW |

---

## 권고사항

### 투자 실행 전 확인 사항

1. **최신 시세 확인**: 과학기술인공제회 포털에서 현재 펀드 기준가 확인
2. **금리 확인**: 한국은행, Federal Reserve 공식 사이트에서 최신 기준금리 확인
3. **펀드 가용성**: 선택한 펀드가 퇴직연금 상품으로 제공되는지 확인

### 리밸런싱 가이드

| 주기 | 조건 |
|------|------|
| 반기 1회 | 비중 편차 ±5%p 초과 시 목표 비중으로 조정 |
| 수시 | 위험자산 70% 초과 시 즉시 조정 |

### 모니터링 포인트

- Fed/한국은행 금리 결정
- 반도체 업황 (AI 수요, 재고 수준)
- USD/KRW 환율 변동
- 미중 기술 갈등 동향

---

## 관련 보고서

| 보고서 | 파일 | 설명 |
|--------|------|------|
| 거시경제 분석 | [00-macro-outlook.md](./00-macro-outlook.md) | 시장 전망 및 자산배분 근거 |
| 펀드 분석 | [01-fund-analysis.md](./01-fund-analysis.md) | 상세 분석 및 추천 근거 |
| 규제 검증 | [02-compliance-report.md](./02-compliance-report.md) | DC형 규제 준수 검증 |
| 출력 검증 | [03-output-verification.md](./03-output-verification.md) | 환각 방지 및 데이터 정합성 |

### 분석 데이터 파일

| 파일 | 용도 |
|------|------|
| [index-data.json](./index-data.json) | 지수 데이터 (참조값) |
| [rate-analysis.json](./rate-analysis.json) | 금리/환율 분석 |
| [sector-analysis.json](./sector-analysis.json) | 섹터별 전망 |
| [risk-analysis.json](./risk-analysis.json) | 리스크 분석 |

---

## 면책조항

본 분석은 **투자 권유가 아닌 정보 제공 목적**입니다.

- 과거 수익률이 미래 수익률을 보장하지 않습니다.
- 웹검색 API 제한으로 거시경제 데이터가 실시간 검증되지 않았습니다.
- 실제 투자 전 과학기술인공제회 포털에서 최신 정보를 확인하세요.
- 펀드 선택 및 투자 결정의 책임은 투자자에게 있습니다.

---

*Multi-Agent Portfolio Analysis System v3.0*
*Agents: index-fetcher, rate-analyst, sector-analyst, risk-analyst, macro-synthesizer, fund-portfolio, compliance-checker, output-critic*
*Coordinated by: portfolio-coordinator*

**데이터 기준일**: 2026-01-01 (fund_data.json)
**분석 실행일**: 2026-01-21 23:05:00
**데이터 경과일**: 20일 (FRESH)
