# assets/

스크린샷 섹션은 현재 **CSS 키프레임 기반 애니메이션 목업**(index.html `.shot-anim` + styles.css `sa-*`)으로
동작하므로 이미지 파일이 필요 없습니다.

실기기 캡처(GIF/스틸)로 교체하고 싶다면:
1. 이 폴더에 `still-*.png` / `demo-*.gif`를 넣고
2. index.html의 `.shot-anim` div를 `<img>`로 교체하세요.
   (기존 hover-play JS는 제거됨 — 필요 시 git 히스토리 참고)
