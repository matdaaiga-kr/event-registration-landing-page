# event-registration-landing-page
이벤트 등록 페이지용 바이브코딩 리포

이 레포는 각 이벤트 폴더에 `index.md`(콘텐츠) + `images/`(이미지) + (선택) `speakers.csv`(연사/세션)를 넣고,
`TEMPLATE.md`의 가이드대로 정적 랜딩페이지(`index.html`)를 빠르게 생성하는 용도입니다.

## 사용 방법(요약)
1) 이벤트 폴더를 만들고(예: `2026/06/localhost-build/`) 아래 파일을 준비합니다.
	- `index.md`
	- `images/` (최소 1개 이미지)
	- `speakers.csv` (있으면)
2) AI에게 `TEMPLATE.md`와 해당 이벤트 폴더 전체를 함께 주고,
	“`TEMPLATE.md`의 AI 실행 지침을 그대로 따라 같은 폴더에 `index.html` 단일 파일을 생성하라”라고 요청합니다.

자세한 규칙(섹션 구성/디자인/CSV 스키마/필수 키워드 등)은 `TEMPLATE.md`를 참고하세요.
