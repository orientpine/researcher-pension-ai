# Researcher Pension AI

과학기술인공제회 DC형 퇴직연금 포트폴리오를 AI 멀티에이전트 시스템으로 분석·추천합니다.

> **⚠️ 본 프로젝트의 모든 분석은 AI가 자동 생성한 것이며, 투자 권유가 아닙니다.** [DISCLAIMER.md](DISCLAIMER.md) 참고

---

## 빠른 시작

### 1. 플러그인 설치

[OpenCode](https://github.com/opencode-ai/opencode) 또는 Claude Code에서 `investments-portfolio` 플러그인을 설치합니다.

### 2. 포트폴리오 생성

투자자 프로필과 함께 명령을 실행합니다:

```
/investments-portfolio:portfolio-analyze 나를 위한 새로운 포트폴리오를 구성해줘.

| 항목 | 내용 |
|------|------|
| **연령대** | 30대 초반 |
| **직업** | 연구원 |
| **은퇴 예정** | 65세 (약 30년 후) |
| **투자 성향** | **공격형** (30년+ 장기투자) |
| **위험 수용도** | 높음 (단기 -30% 손실 감내 가능) |
```

### 3. 결과 확인

`portfolios/` 디렉토리에 보고서가 자동 생성됩니다:

```
portfolios/2026-03-30-aggressive-abc123/
├── 00-macro-outlook.md        # 거시경제 전망
├── 01-fund-analysis.md        # 펀드 분석 및 추천
├── 02-compliance-report.md    # DC형 규제 준수 검증
├── 03-output-verification.md  # 환각 방지 출력 검증
└── 04-portfolio-summary.md    # 최종 포트폴리오 요약
```

> 더 많은 예시는 [examples/usage.md](examples/usage.md) 참고

---

## 멀티에이전트 워크플로우

5개의 전문 에이전트가 순차적으로 협업합니다:

```
[사용자 요청 + 투자자 프로필]
     │
     ▼
[macro-outlook]         거시경제 동향, 시장 전망, 자산배분 권고
     │
     ▼
[fund-portfolio]        펀드 데이터 기반 포트폴리오 구성
     │
     ▼
[compliance-checker]    DC형 위험자산 70% 한도, 단일펀드 40% 한도 검증
     │
     ▼
[output-critic]         출처 검증, 환각(hallucination) 탐지, 신뢰도 점수
     │
     ▼
[portfolio-orchestrator] 최종 통합 보고서
```

| 에이전트 | 출력 | 역할 |
|----------|------|------|
| **macro-outlook** | `00-macro-outlook.md` | 거시경제·시장 전망 |
| **fund-portfolio** | `01-fund-analysis.md` | 펀드 선별·비중 배분 |
| **compliance-checker** | `02-compliance-report.md` | 규제 준수 검증 |
| **output-critic** | `03-output-verification.md` | 환각 방지·출처 검증 |
| **portfolio-orchestrator** | `04-portfolio-summary.md` | 최종 통합 |

---

## 프로젝트 구조

```
researcher-pension-ai/
├── funds/                  # 펀드 데이터 (제로인 기반)
│   ├── fund_data.json      #   펀드 기본정보·수익률 (206개)
│   ├── fund_fees.json      #   수수료 정보
│   ├── fund_classification.json  #   자산 분류 (6개 카테고리)
│   ├── deposit_rates.json  #   예금 금리
│   └── all/                #   전체 펀드 데이터 (2,015개)
├── consultations/          # AI 투자 컨설테이션 보고서
├── docs/                   # 기술 문서·개선 계획
├── examples/               # 사용 예제
├── resource/               # 원본 CSV/XLSX (과학기술공제회 상품제안서)
├── DISCLAIMER.md           # 투자 면책 조항
└── AGENTS.md               # 프로젝트 지식베이스
```

## 펀드 데이터

| 파일 | 설명 | 레코드 수 |
|------|------|-----------|
| `fund_data.json` | 투자가능 펀드 기본정보·수익률 | 206개 |
| `fund_fees.json` | 펀드 총보수·연간비용 | 206개 |
| `fund_classification.json` | 카테고리·위험자산 분류 | 206개 |
| `deposit_rates.json` | 원리금보장형 예금 금리 | - |
| `all/all_fund_data.json` | 전체 펀드 (투자불가 포함) | 2,015개 |

- **데이터 출처**: 과학기술인공제회 상품제안서 (제로인 평가 데이터)
- **기준일**: 2026-03-01

---

## 펀드 데이터 업데이트

매월 과학기술공제회에서 새 상품제안서(CSV)가 발행되면, `data-updater` 스킬로 펀드 데이터를 갱신합니다.

### resource/ 폴더

원본 CSV/XLSX 파일을 보관합니다:

```
resource/
├── 25년12월_상품제안서_퇴직연금(DCIRP).csv
├── 25년12월_상품제안서_퇴직연금(DCIRP).xlsx
├── 26년01월_상품제안서_퇴직연금(DCIRP).csv
├── 26년01월_상품제안서_퇴직연금(DCIRP).xlsx
├── 26년03월_상품제안서_퇴직연금(DCIRP).csv
└── 26년03월_상품제안서_퇴직연금(DCIRP).xlsx
```

> 새 CSV를 받으면 `resource/` 폴더에 추가한 뒤 아래 명령을 실행합니다.

### 업데이트 실행

```
/investments-portfolio:data-updater resource/26년03월_상품제안서_퇴직연금(DCIRP).csv
```

자동으로 수행되는 작업:

1. CSV 파싱 및 검증 (UTF-8, 헤더 확인)
2. `funds/fund_data.json` 생성 (펀드 기본정보·수익률)
3. `funds/fund_fees.json` 생성 (수수료 정보)
4. `funds/fund_classification.json` 생성 (자산 분류)
5. `funds/all/` 전체 펀드 데이터 저장 (2,015개)
6. 기존 파일 자동 백업 (`funds/archive/`)

### 예금금리 업데이트 (선택)

예금금리는 웹에서 조회할 수 없는 과학기술공제회 내부 금리이므로, 직접 입력해야 합니다:

```
/investments-portfolio:data-updater 예금금리 업데이트
과학기술인공제회 1년: 4.9%
우리은행 1년: 2.75%
```

---
## 라이선스

이 프로젝트의 코드와 분류 데이터는 자유롭게 사용할 수 있습니다.  
펀드 수익률·수수료 데이터는 과학기술인공제회/제로인의 공개 시장 데이터를 기반으로 합니다.
