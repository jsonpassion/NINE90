# nine90-content

NINE90 앱이 동기화하는 학습 콘텐츠 저장소. 앱 코드와 분리되어 있어,
이 저장소만 갈아끼우면 같은 앱 구조로 다른 시험(TOEFL, TEPS, HSK 등)
전용 앱을 배포할 수 있다.

## 구조

```
manifest.json                 # 앱이 처음 읽는 파일 — 버전, 밴드 정책, 파일 목록
privacy.md                    # 앱 설정에서 링크되는 개인정보 처리방침
content/
└── voca/                     # 콘텐츠 타입 (현재 voca만)
    ├── score-000-399/        # 레벨(점수 밴드)별 디렉토리
    │   └── unit-001.md       # 1권 = 단어 100개 = 앱의 챕터 10개
    ├── score-400-599/
    ├── score-600-799/
    └── score-800-990/
tools/
├── build_manifest.py         # content/ 스캔 → 체크섬 계산 → manifest.json 생성
└── validate_content.py       # 형식·중복·개수 검증
```

## 단어 파일 형식

파일 하나 = 1권(unit). 파일명 `unit-NNN.md`의 번호가 manifest의 `sequence`가 된다.
앱은 밴드의 모든 unit을 sequence 순으로 이어붙인 뒤 10개씩 챕터로 나눈다.

```markdown
---
id: voca-000-399-u001        # voca-{band}-u{NNN} — 절대 바꾸지 말 것 (학습 진도 키)
type: voca
level: 1                     # 밴드 순서 (1-4)
difficulty: beginner
tags: [toeic, vocabulary, unit-1]
source: nine90
version: 1
updated_at: 2026-07-09T00:00:00Z
score_band_id: score-000-399 # 디렉토리명과 일치해야 함
score_min: 0
score_max: 399
---

- word | 뜻 | /발음(IPA)/ | 암기 힌트 | Example sentence. | 예문 번역.
```

단어 줄은 파이프(`|`) 구분 6필드. 본문에 파이프 문자를 쓰면 안 된다.
(구버전 4필드 `word | 뜻 | 예문 | 번역`도 앱이 읽을 수 있지만 새 콘텐츠는 6필드로.)

## 콘텐츠 수정 워크플로

1. `content/` 아래 md 파일 수정 또는 추가 (새 권은 `unit-002.md`처럼 다음 번호로)
2. `python3 tools/validate_content.py` — 에러 0 확인
3. `python3 tools/build_manifest.py` — 체크섬·버전 자동 갱신
4. 커밋 & 푸시 → 앱이 다음 실행 때 변경된 파일만 다시 받는다

**주의**: 파일의 `id`와 단어 줄 순서는 학습 진도(카드 ID = `{id}-{줄번호}`)의
키가 된다. 출시 후에는 줄 삭제·순서 변경 대신 새 unit 추가를 우선할 것.

## 새 시험 트랙 만들기 (TOEFL, HSK 등)

1. 이 저장소를 새 저장소로 복제
2. `tools/build_manifest.py`의 `TRACK`, `SCORE_BANDS`, `PROFILE` 수정
   (앱의 `ScoreBandInfo.allBands`와 밴드 id·범위가 일치해야 함)
3. `content/voca/{새 밴드 id}/` 아래 콘텐츠 작성
4. 앱 쪽은 manifest URL과 밴드 정의만 바꾸면 동일 구조로 동작

## 홍보 사이트 (GitHub Pages)

`docs/`가 GitHub Pages로 배포된다 — https://jsonpassion.github.io/NINE90/
- `index.html` 랜딩 (스크린샷 플레이스홀더는 docs/assets/README.md 참고)
- `privacy.html` / `terms.html` — 한/영 토글 정책 페이지 (원본: 루트 privacy.md / terms.md, 앱이 raw URL로 링크)
- 스타일: 앱 NB 디자인 시스템 미러 (`docs/styles.css` 상단 토큰 = NBTheme.swift)
