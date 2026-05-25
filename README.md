# Interpretation KR

> 대한민국 법령해석례를 Git으로 관리합니다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![data](https://img.shields.io/badge/data-Markdown-blue)](kr/) [![source](https://img.shields.io/badge/source-법제처_DRF_OpenAPI-orange)](https://open.law.go.kr)

법제처가 발간하는 **법령해석례**를 Markdown + YAML frontmatter 로 변환하여 Git 저장소에서 관리합니다. 각 해석례는 회답일자를 Git commit date 로 갖고, 안건명·질의요지·회답내용·이유·관련법령을 메타·본문으로 보관합니다.

법령(`legalize-kr`)·행정규칙(`regulate-kr`)·판례(`precedent-kr`)에 이어, **법령해석례**까지 Git 으로 추적해 법령 적용 해석의 변화를 시각화합니다.

## 왜 필요한가?

법령은 문언이지만, **해석례는 그 문언이 실제 행정에서 어떻게 적용되는지의 공식 해석** 입니다. 민원인·지자체가 법제처에 질의한 사항에 대해 법제처가 회답한 공식 해석으로, 실무에서 직접 참조됩니다.

```
개인정보보호법 제15조 (개인정보의 수집·이용)
  └─ 법제처 해석례 2024-XXX (마케팅 동의 수집 범위)
       └─ 법제처 해석례 2025-XXX (AI 학습 데이터 활용 범위)
```

## 빠른 시작

```bash
git clone https://github.com/wellsa-ai/interpretation-kr.git
cd interpretation-kr

# 특정 해석례 보기 (예시 경로)
cat kr/2024/24-XXX.md

# 특정 법령 관련 해석례 검색
grep -rl "개인정보보호법" kr/
```

## 구조

```
kr/{회답연도}/
  {안건번호}.md            # 해석례 본문 (질의요지·회답·이유)
  ...
```

## 메타데이터 (YAML Frontmatter)

```yaml
---
안건명: "개인정보 수집 동의 범위에 관한 해석"
안건번호: "24-0123"
회답일자: "2024-06-15"
질의기관: "○○시"
회답기관: "법제처"
관련법령:
  - "개인정보보호법 제15조"
  - "개인정보보호법 시행령 제17조"
출처: "https://www.law.go.kr/법령해석례/(24-0123)"
---
```

## 자동 업데이트

매일 [국가법령정보센터 DRF API](https://open.law.go.kr) 의 `target=expc` 를 체크하여 신규·정정 해석례가 있으면 자동으로 커밋합니다.

- `pipeline/cron_update.sh` — 매일 06:00 KST (신규 체크)
- `pipeline/cron_full_sweep.sh` — 매일 23:30 KST (전체 풀 스윕)

## 관련 프로젝트

| 프로젝트 | 대상 | 설명 |
|---|---|---|
| [legalize-kr](https://github.com/legalize-kr/legalize-kr) | 법률·시행령 | 대한민국 법령 |
| [regulate-kr](https://github.com/wellsa-ai/regulate-kr) | 행정규칙·고시 | 전 부처 행정규칙 |
| [precedent-kr](https://github.com/wellsa-ai/precedent-kr) | 법원 판례 | 대한민국 법원 판례 |
| **interpretation-kr** (이 저장소) | 법령해석례 | 법제처 법령해석례 |
| [constitution-kr](https://github.com/wellsa-ai/constitution-kr) | 헌재결정례 | 헌법재판소 결정례 |
| [localrule-kr](https://github.com/wellsa-ai/localrule-kr) | 자치법규 | 지자체 자치법규 |
| [treaty-kr](https://github.com/wellsa-ai/treaty-kr) | 조약 | 대한민국 조약 |

## 활용 사례

- **법령 검색 보강**: 법령 검색 결과에 관련 해석례 동시 노출
- **법무 실무**: "이 조문이 우리 케이스에 어떻게 적용되나" 공식 해석 확인
- **민원 자동 응답**: 시민 질의 → 유사 해석례 추출 (예: [MiniLex](https://minilex.wellsa.ai))

## 데이터 출처

모든 해석례 데이터는 [국가법령정보센터 DRF API](https://open.law.go.kr) 에서 가져옵니다. 해석례 원문은 대한민국 정부 공공저작물로 자유롭게 이용 가능합니다.

## 라이선스

- 해석례 원문: 공공저작물 (대한민국 정부)
- 저장소 구조·파이프라인 코드: MIT

## 기여

이슈, PR 환영합니다.
