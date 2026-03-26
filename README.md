# NINE90 — TOEIC 990 Content Repository

TOEIC 990 만점을 위한 학습 콘텐츠 저장소. iOS 앱 [NINE90](https://github.com/jsonpassion/NINE90)에서 동기화하여 사용합니다.

## 콘텐츠 현황 (v3.0.0)

| 밴드 | 레벨 | VOCA 파일 | 단어 수 | RC 파일 | 문제 수 |
|------|------|----------|--------|---------|--------|
| 0-399 | 입문 | 100 | 1,000 | 100 | ~300 |
| 400-599 | 중급 | 100 | 1,000 | 100 | ~300 |
| 600-799 | 중상급 | 100 | 1,000 | 100 | ~400 |
| 800-990 | 고급 | 100 | 1,000 | 100 | ~400 |
| **합계** | | **400** | **4,000** | **400** | **~1,400** |

## 디렉토리 구조

```
nine90-content/
├── manifest.json           ← 앱이 먼저 동기화하는 매니페스트
├── privacy.md              ← 개인정보 처리방침 (한/영)
├── content/
│   ├── voca/               ← 단어 카드 (10개/파일)
│   │   ├── band-000-399/   ← voca-000-d01.md ~ d100.md
│   │   ├── band-400-599/   ← voca-400-d01.md ~ d100.md
│   │   ├── band-600-799/   ← voca-600-d01.md ~ d100.md
│   │   └── band-800-990/   ← voca-800-d01.md ~ d100.md
│   └── rc/                 ← 독해 지문 + 문제
│       ├── band-000-399/   ← rc-000-001.md ~ 100.md (3문제/파일)
│       ├── band-400-599/   ← rc-400-001.md ~ 100.md (3문제/파일)
│       ├── band-600-799/   ← rc-600-001.md ~ 100.md (4문제/파일)
│       └── band-800-990/   ← rc-800-001.md ~ 100.md (4문제/파일)
```

## 콘텐츠 포맷

### VOCA (단어 카드)

```markdown
---
id: voca-000-d01
type: voca
level: 1
difficulty: easy
tags: [office, basics]
source: nine90
version: 1
updated_at: 2026-03-23T00:00:00Z
score_band_id: score-000-399
score_min: 0
score_max: 399
---

- word | 한국어 뜻 | Example sentence. | 예문 한국어 번역.
- another | 또다른뜻 | Another example. | 또 다른 예문.
```

- 파일당 10개 단어 카드
- 파이프(`|`) 구분: 단어 | 뜻 | 예문 | 예문 번역

### RC (독해 지문)

```markdown
---
id: rc-000-001
type: rc
level: 1
difficulty: easy
tags: [notice, office]
source: nine90
version: 1
updated_at: 2026-03-23T00:00:00Z
score_band_id: score-000-399
score_min: 0
score_max: 399
---

# Passage Title

Passage text here.

## Q1. Question prompt?
- A. Option A
- B. Option B
- C. Option C
- D. Option D
- Answer: B
- Explanation: Why B is correct.
```

- 밴드 000-599: 3문제/파일
- 밴드 600-990: 4문제/파일

## 점수대 (Score Bands)

| ID | 범위 | 레벨 | VOCA 난이도 | RC 지문 길이 |
|----|------|------|-----------|-------------|
| `score-000-399` | 0-399 | 입문 | 기초 일상 어휘 | 80-120 단어 |
| `score-400-599` | 400-599 | 중급 | 비즈니스 기초 | 150-200 단어 |
| `score-600-799` | 600-799 | 중상급 | 전문 비즈니스 | 200-280 단어 |
| `score-800-990` | 800-990 | 고급 | 법률/금융/기업 | 280-350 단어 |

## 동기화 방식

1. 앱이 `manifest.json`을 다운로드
2. 로컬 버전과 비교 → 변경 시 콘텐츠 다운로드
3. 마크다운 파싱 → 앱 모델로 변환
4. 오프라인 캐시 저장 (Application Support)

## 콘텐츠 추가 방법

1. 해당 밴드 디렉토리에 마크다운 파일 추가
2. `manifest.json`의 `entries` 배열에 엔트리 추가
3. `manifest.json`의 `version` 번호 증가
4. 커밋 & 푸시 → 앱이 자동 동기화

## 라이선스

모든 콘텐츠는 100% 오리지널로 제작되었으며 상업적 사용이 가능합니다.
개별 영어 단어는 저작권의 대상이 아니며, 모든 예문과 지문은 독자적으로 작성되었습니다.
