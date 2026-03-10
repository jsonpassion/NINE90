# NINE90 Content Repository

TOEIC 990 학습 앱 콘텐츠 저장소.

## Directory Structure

```
nine90-content/
├── manifest.json          ← App syncs this first
├── content/
│   ├── voca/              ← Vocabulary card sets
│   │   ├── band-000-399/  ← Beginner (입문)
│   │   ├── band-400-599/  ← Lower Intermediate (중급 기초)
│   │   ├── band-600-799/  ← Intermediate (중급)
│   │   └── band-800-990/  ← Advanced (고급)
│   └── rc/                ← Reading Comprehension passages
│       ├── band-000-399/
│       ├── band-400-599/
│       ├── band-600-799/
│       └── band-800-990/
```

## Adding Content

### 1. VOCA File Format

```markdown
---
id: voca-000-d03
type: voca
level: 1
difficulty: easy
tags: [office, basics]
source: nine90
version: 1
updated_at: 2026-03-15T00:00:00Z
score_band_id: score-000-399
score_min: 0
score_max: 399
---

- word | 뜻 | Example sentence. | 예문 한국어 번역.
- another | 또다른뜻 | Another example. | 또 다른 예문.
```

### 2. RC File Format

```markdown
---
id: rc-000-005
type: rc
level: 1
difficulty: easy
tags: [notice, office]
source: nine90
version: 1
updated_at: 2026-03-15T00:00:00Z
score_band_id: score-000-399
score_min: 0
score_max: 399
---

# Passage Title

Passage text goes here. Multiple sentences forming a coherent TOEIC-style passage.

## Q201. Question prompt here?
- A. Option A
- B. Option B
- C. Option C
- D. Option D
- Answer: B
- Explanation: Why B is the correct answer.

## Q202. Another question?
- A. Option A
- B. Option B
- C. Option C
- D. Option D
- Answer: C
- Explanation: Explanation text.
```

### 3. Update manifest.json

After adding files, add corresponding entries to `manifest.json`:

```json
{
  "id": "voca-000-d03",
  "type": "voca",
  "level": 1,
  "path": "content/voca/band-000-399/voca-000-d03.md",
  "checksum_sha256": "placeholder",
  "updated_at": "2026-03-15T00:00:00Z",
  "tags": ["office", "basics"],
  "score_band_id": "score-000-399",
  "score_min": 0,
  "score_max": 399,
  "sequence": 3
}
```

### 4. Bump version

Update `manifest.json` top-level `version` field (e.g., `"1.0.0"` → `"1.1.0"`).

## Naming Convention

| Type | Pattern | Example |
|------|---------|---------|
| VOCA | `voca-{band}-d{day}` | `voca-000-d01`, `voca-400-d03` |
| RC | `rc-{band}-{seq}` | `rc-000-001`, `rc-800-004` |

## Score Bands

| ID | Range | Level |
|----|-------|-------|
| `score-000-399` | 0-399 | 입문 (Beginner) |
| `score-400-599` | 400-599 | 중급 기초 (Lower Intermediate) |
| `score-600-799` | 600-799 | 중급 (Intermediate) |
| `score-800-990` | 800-990 | 고급 (Advanced) |
