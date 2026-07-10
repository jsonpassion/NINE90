# 스크린샷 / GIF 자산

## 호버 재생 GIF (권장)

정지 화면(PNG) + GIF 한 쌍을 넣고 `docs/index.html`의 `.shot-ph` div를 교체하세요.
JS가 자동으로 **마우스 호버 시 GIF 재생, 벗어나면 정지 화면 복귀**를 처리합니다:

```html
<!-- 교체 전 -->
<div class="shot-ph">📱<br />대시보드<br />GIF 준비 중 ...</div>

<!-- 교체 후 -->
<img data-still="assets/still-dashboard.png"
     data-gif="assets/demo-dashboard.gif"
     src="assets/still-dashboard.png" alt="대시보드 — 책장 진도" />
```

권장 파일명:
- still-dashboard.png / demo-dashboard.gif
- still-cards.png / demo-cards.gif
- still-quiz.png / demo-quiz.gif

권장 사양: 시뮬레이터 화면 녹화 → GIF 변환(880px 폭, 12~15fps, 5초 내외, 3MB 이하).

## 정적 스크린샷만 쓸 경우

`data-*` 속성 없이 `<img src="assets/screen-dashboard.png">` 만 넣으면 됩니다.
