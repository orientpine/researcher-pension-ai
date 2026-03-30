# 펀드 포트폴리오 분석

**분석 기준일**: 2026-01-31  
**데이터 기준일**: 2026-01-01 (fund_data.json)  
**버전**: v4.5 (macro-outlook 반영 강화 + 펀드 선택 근거)

---

## 투자자 프로필
- 투자 성향: 중립형 (moderate)
- 위험자산 한도: 70% (DC형)
- 목표 위험자산: 50-60%

---

## macro-outlook 반영 검증 (MANDATORY)

> **참조**: `00-macro-outlook.md` (섹션 8. 자산배분 시사점)

| 항목 | macro-outlook 권고 | 실제 포트폴리오 | 편차 | 상태 | 근거 |
|------|-------------------|----------------|:----:|:----:|------|
| 위험자산 비중 | 50-60% | 53% | 0%p | ✅ | 목표 범위 내 |
| 환헤지 전략 | 50% 부분 헤지 | 48% (15%H/16%UH) | -2%p | ✅ | 목표 근접 |
| 미국 비중 | 35% (위험자산 대비) | 34% (18%/53%) | -1%p | ✅ | 목표 근접 |
| 한국 비중 | 12% | 22% | +10%p | ⚠️ | 에너지/테크 기회 활용 (아래 근거) |
| 신흥국 비중 | 23% | 13% (글로벌 배당 간접) | -10%p | ⚠️ | 직접 신흥국 펀드 부재 (아래 근거) |
| 주목 섹터 (에너지) | Overweight | 12% 편입 | - | ✅ | 원자력 ETF 편입 |
| 주목 섹터 (방어주) | Overweight | 13% 편입 | - | ✅ | 글로벌 배당 펀드 편입 |
| 회피 섹터 (원자재) | Underweight | 0% | - | ✅ | 미편입 확인 |

### 편차 근거

**한국 비중 +10%p 초과 근거**:
- macro-outlook 섹션 1: "KOSPI 5,224 사상 최고치 경신, 반도체 주도"
- macro-outlook 섹션 4: 기술/반도체 Neutral이지만, 원자력(에너지)은 Overweight
- `fund_data.json`: NH-AmundiHANARO원자력 return1y=178.03% (1위)
- 원자력은 에너지 섹터로 macro-outlook Overweight 권고에 부합

**신흥국 비중 -10%p 미달 근거**:
- 과기공제회 펀드 리스트에 순수 신흥국 ETF 부재
- 글로벌 배당/인컴 펀드(13%)로 간접 노출 대체
- macro-outlook 섹션 7: 인도, 인도네시아 통화정책 완화 → 글로벌 펀드 내 간접 노출

---

## 안전자산 비교 (예금 vs 채권)

| 구분 | 예금 (과기공제회) | 채권형 펀드 (bestBond) |
|------|:----------------:|:---------------------:|
| 상품명 | 과학기술인공제회 퇴직연금 운용방법 (1년) | 미래에셋브라질하이인컴채권증권자투자신탁[채권]종류Crp-e |
| 명목 수익률 | 4.9% | 22.67% |
| 총보수 | 0% | 0.88% |
| 실질 수익률 | **4.9%** | **21.79%** |
| 원금 보장 | O | X |
| 채권 선택 기준 | - | 5.4% (예금+0.5%p) |
| **결론** | 미선택 | **선택** |

**SAFE_ASSET_DECISION: 채권** [출처: `deposit_rates.json`, `fund_fees.json`]

> 채권 실질수익률 21.79% > 예금+0.5%p(5.4%) → 채권 선택

---

## 추천 포트폴리오

| # | 펀드명 | 비중 | 유형 | 위험자산 | 1Y 수익률 |
|:-:|--------|:----:|:----:|:--------:|:---------:|
| 1 | 신한미국S&P500인덱스증권자투자신탁(H)[주식-파생형](종류C-re) | 9% | 해외주식형 | O | 13.53% |
| 2 | 신한미국S&P500인덱스증권자투자신탁(UH)[주식-파생형](종류C-re) | 9% | 해외주식형 | O | 13.54% |
| 3 | 미래에셋TIGER코리아테크액티브증권상장지수투자신탁(주식) | 10% | 주식형 | O | 120.59% |
| 4 | NH-AmundiHANARO원자력iSelect증권상장지수투자신탁(주식) | 12% | 주식형 | O | 178.03% |
| 5 | 마이다스글로벌블루칩배당인컴혼합자산자투자신탁(H)C-Pe2 | 6% | 해외주식형 | O | 11.84% |
| 6 | 마이다스글로벌블루칩배당인컴혼합자산자투자신탁(UH)C-Pe2 | 7% | 해외주식형 | O | 13.28% |
| 7 | 미래에셋브라질하이인컴채권증권자투자신탁[채권]종류Crp-e | 25% | 채권형 | X | 22.67% |
| 8 | 우리PIMCO토탈리턴증권자투자신탁[채권_재간접형](H)ClassPe1 | 22% | 채권형 | X | 7.21% |
| **합계** | - | **100%** | - | **53%** | - |

---

## 펀드 선택 근거 (MANDATORY - v4.5)

| # | 펀드명 | 비중 | 선택 근거 | 참조 출처 |
|:-:|--------|:----:|----------|----------|
| 1 | 신한미국S&P500인덱스(H) | 9% | macro-outlook 미국 35% 권고 + 환헤지 50% 권고 반영 | `00-macro-outlook.md` 섹션 3, 8 |
| 2 | 신한미국S&P500인덱스(UH) | 9% | 미국 비중 확보 + 환노출로 원화 강세 수혜 가능성 | `00-macro-outlook.md` 섹션 3: USD/KRW -2.46% |
| 3 | 미래에셋TIGER코리아테크 | 10% | return1y=120.59% (상위 3%) + 반도체 사이클 회복 기대 | `fund_data.json` return1y, `00-macro-outlook.md` 섹션 4 |
| 4 | NH-AmundiHANARO원자력 | 12% | **macro-outlook 에너지 Overweight** + return1y=178.03% (1위) + return3y=70.34% | `fund_data.json`, `00-macro-outlook.md` 섹션 4: 에너지 Overweight |
| 5 | 마이다스글로벌블루칩배당(H) | 6% | **macro-outlook 방어주 Overweight** + 배당/인컴 안정성 + 환헤지 | `00-macro-outlook.md` 섹션 8: 방어적 자산 30% 이상 |
| 6 | 마이다스글로벌블루칩배당(UH) | 7% | 방어주 + 환노출 (50% 환헤지 목표 달성용) | `00-macro-outlook.md` 섹션 3, 8 |
| 7 | 미래에셋브라질하이인컴채권 | 25% | **bestBond** (실질수익률 21.79% > 예금+0.5%p) + 신흥국 간접 노출 | `fund_data.json` return1y=22.67%, `fund_fees.json` totalFee=0.88% |
| 8 | 우리PIMCO토탈리턴채권(H) | 22% | 글로벌 채권 분산 + 환헤지 + PIMCO 운용 전문성 | `fund_data.json` return1y=7.21%, `00-macro-outlook.md` 섹션 5: 변동성 대비 |

---

## 수익률 스냅샷 (6M/1Y/3Y)

| 펀드명 | 6M | 1Y | 3Y | 출처 |
|--------|:--:|:--:|:--:|------|
| 신한미국S&P500인덱스(H) | 11.51% | 13.53% | - | `fund_data.json` |
| 신한미국S&P500인덱스(UH) | 18.89% | 13.54% | - | `fund_data.json` |
| 미래에셋TIGER코리아테크 | 76.88% | 120.59% | - | `fund_data.json` |
| NH-AmundiHANARO원자력 | 30.03% | 178.03% | 70.34% | `fund_data.json` |
| 마이다스글로벌블루칩배당(H) | 5.32% | 11.84% | 18.89% | `fund_data.json` |
| 마이다스글로벌블루칩배당(UH) | 12.11% | 13.28% | 25.24% | `fund_data.json` |
| 미래에셋브라질하이인컴채권 | 8.86% | 22.67% | 7.70% | `fund_data.json` |
| 우리PIMCO토탈리턴채권(H) | 3.49% | 7.21% | 3.49% | `fund_data.json` |

---

## 섹터 집중 리스크 분석

| 섹터 그룹 | 포함 펀드 | 합계 비중 | 상관관계 | 판정 |
|:----------|:----------|:--------:|:--------:|:----:|
| Tech/AI | 미래에셋TIGER코리아테크(10%) | **10%** | High | ✅ 정상 |
| 에너지/인프라 | NH-AmundiHANARO원자력(12%) | **12%** | Medium | ✅ 정상 |
| 금융/배당 | 마이다스글로벌블루칩배당(13%) | **13%** | Low | ✅ 정상 |
| 채권/안전 | 브라질하이인컴(25%), PIMCO(22%) | **47%** | Low | ✅ 정상 |
| 미국 인덱스 | 신한S&P500(18%) | **18%** | Medium | ✅ 정상 |

> Tech/AI 그룹 10% < 40% 한도 → **PASS**

---

## 최종 검증 체크리스트

- [x] SAFE_ASSET_DECISION="채권" → 채권형 펀드 포함됨 (bestBond 25%)
- [x] 예금 vs 채권 비교 테이블 포함됨
- [x] **macro-outlook 반영 검증 테이블** 포함됨 (Step 2.5)
- [x] **주목 섹터** 최소 1개 이상 포함됨 (에너지 12%, 방어주 13%)
- [x] **회피 섹터(원자재)** 0% 편입됨
- [x] 편차 발생 시 **근거 명시**됨 (한국 +10%p, 신흥국 -10%p)
- [x] **펀드 선택 근거 테이블** 포함됨 (섹션 5.4)
- [x] **모든 펀드/예금에 selectionRationale + 참조 출처** 있음

---

## 출력 JSON (기계 가독용)

```json
{
  "portfolio": [
    { 
      "name": "신한미국S&P500인덱스증권자투자신탁(H)[주식-파생형](종류C-re)", 
      "weight": 9, 
      "category": "해외주식형", 
      "role": "core",
      "selectionRationale": {
        "reason": "macro-outlook 미국 35% 권고 + 환헤지 50% 권고 반영",
        "references": ["00-macro-outlook.md:섹션3,8"]
      }
    },
    { 
      "name": "신한미국S&P500인덱스증권자투자신탁(UH)[주식-파생형](종류C-re)", 
      "weight": 9, 
      "category": "해외주식형", 
      "role": "core",
      "selectionRationale": {
        "reason": "미국 비중 확보 + 환노출로 원화 강세 수혜",
        "references": ["00-macro-outlook.md:섹션3"]
      }
    },
    { 
      "name": "미래에셋TIGER코리아테크액티브증권상장지수투자신탁(주식)", 
      "weight": 10, 
      "category": "주식형", 
      "role": "satellite",
      "selectionRationale": {
        "reason": "return1y=120.59% (상위 3%) + 반도체 사이클 회복",
        "references": ["fund_data.json:return1y=120.59%", "00-macro-outlook.md:섹션4"]
      }
    },
    { 
      "name": "NH-AmundiHANARO원자력iSelect증권상장지수투자신탁(주식)", 
      "weight": 12, 
      "category": "주식형", 
      "role": "satellite",
      "selectionRationale": {
        "reason": "macro-outlook 에너지 Overweight + return1y=178.03% (1위)",
        "references": ["fund_data.json:return1y=178.03%,return3y=70.34%", "00-macro-outlook.md:섹션4"]
      }
    },
    { 
      "name": "마이다스글로벌블루칩배당인컴혼합자산자투자신탁(H)C-Pe2", 
      "weight": 6, 
      "category": "해외주식형", 
      "role": "satellite",
      "selectionRationale": {
        "reason": "macro-outlook 방어주 Overweight + 배당/인컴 안정성",
        "references": ["00-macro-outlook.md:섹션8"]
      }
    },
    { 
      "name": "마이다스글로벌블루칩배당인컴혼합자산자투자신탁(UH)C-Pe2", 
      "weight": 7, 
      "category": "해외주식형", 
      "role": "satellite",
      "selectionRationale": {
        "reason": "방어주 + 환노출 (50% 환헤지 목표 달성용)",
        "references": ["00-macro-outlook.md:섹션3,8"]
      }
    },
    { 
      "name": "미래에셋브라질하이인컴채권증권자투자신탁[채권]종류Crp-e", 
      "weight": 25, 
      "category": "채권형", 
      "role": "safe",
      "selectionRationale": {
        "reason": "bestBond (실질수익률 21.79% > 예금+0.5%p) + 신흥국 간접 노출",
        "references": ["fund_data.json:return1y=22.67%", "fund_fees.json:totalFee=0.88%", "deposit_rates.json:4.9%"]
      }
    },
    { 
      "name": "우리PIMCO토탈리턴증권자투자신탁[채권_재간접형](H)ClassPe1", 
      "weight": 22, 
      "category": "채권형", 
      "role": "safe",
      "selectionRationale": {
        "reason": "글로벌 채권 분산 + 환헤지 + 변동성 대비",
        "references": ["fund_data.json:return1y=7.21%", "00-macro-outlook.md:섹션5"]
      }
    }
  ],
  "analysis": { 
    "riskProfile": "중립형", 
    "totalRiskWeight": 53, 
    "totalSafeWeight": 47, 
    "SAFE_ASSET_DECISION": "채권",
    "bestBond": { "name": "미래에셋브라질하이인컴채권증권자투자신탁[채권]종류Crp-e", "netReturn": 21.79 },
    "depositRate": 4.9,
    "threshold": 5.4,
    "macroOutlookCompliance": {
      "riskWeight": { "target": "50-60%", "actual": "53%", "status": "PASS" },
      "hedgeRatio": { "target": "50%", "actual": "48%", "status": "PASS" },
      "topSectors": ["에너지(12%)", "방어주(13%)"],
      "avoidSectors": ["원자재(0%)"]
    }
  },
  "sources": [
    { "type": "local", "file": "fund_data.json", "version": "2026-01-01" }, 
    { "type": "local", "file": "fund_fees.json" },
    { "type": "local", "file": "deposit_rates.json" },
    { "type": "local", "file": "00-macro-outlook.md" }
  ]
}
```

---

**면책조항**: 본 분석은 투자 참고 자료이며, 투자 결정에 대한 책임은 투자자 본인에게 있습니다. 과거 수익률이 미래 수익률을 보장하지 않습니다.

---
*Multi-Agent Portfolio Analysis System v4.5*  
*Agent: fund-portfolio*  
*Analysis Date: 2026-01-31*
