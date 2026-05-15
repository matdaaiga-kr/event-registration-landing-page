---
name: event-registration-landing-page
description: 'A comprehensive guide for GitHub Copilot to generate a static web page for event registration with immersive, high-performance web experiences, advanced motion, typography, and architectural craftsmanship.'
---

# 이벤트 등록 랜딩페이지 생성 템플릿

## 목적

이 문서는 이벤트 폴더의 `index.md`, `images/`, (선택) `speakers.csv`를 입력으로 받아, Global Azure Bootcamp 예시와 유사한 레이아웃/스타일의 정적 등록 랜딩페이지 `index.html`을 생성하기 위한 표준 가이드입니다.
이 문서를 포함한 폴더 전체를 AI에 제공하고 "가이드대로 이 폴더에 `index.html`을 생성하라"라고 요청하면, 같은 폴더에 `index.html` 단일 파일을 출력하도록 설계되었습니다.
생성된 HTML은 `index.md`를 단일 소스로 삼아 텍스트/일정/장소 불일치가 없고, `speakers.csv`가 있으면 세션/연사 정보를 우선 반영합니다.

## AI 실행 지침 (가장 중요)

당신은 "정적 이벤트 등록 랜딩페이지 생성기"다. 현재 폴더 안의 파일들을 읽고, 같은 폴더에 `index.html` 단일 파일을 생성하라.

### 입력

- 필수: `index.md`
- 필수: `images/` 폴더(최소 1개 이미지)
- 선택: `speakers.csv`

### 출력

- 같은 폴더에 `index.html` 단일 파일 1개만 생성한다.
- 외부 빌드 도구 없이 동작해야 한다(정적 HTML).
- CSS/JS 외부 파일을 만들지 말고, `index.html` 안에서 인라인 스타일로 완결한다(예시 스타일 유지).

### 절대 규칙(금지/고정)

- 텍스트, 날짜, 시간, 장소, 안내 문구는 `index.md`가 "단일 소스"다. `index.md`와 불일치하는 문구를 임의로 만들지 말 것.
- 섹션 순서/레이아웃/스타일은 "Global Azure Bootcamp 형식"을 그대로 유지한다. 임의로 섹션을 추가/삭제/재배치하지 말 것.
- 이미지 경로는 상대경로만 사용한다: `images/...`
- CTA(참가 신청)는 반드시 실제 링크(`<a href>`)로 만든다.
- 불일치/누락이 발견되면, 생성 전에 질문은 최대 3개까지만 한다. (질문 없이 합리적으로 채울 수 있으면 채우되, 채운 부분은 HTML 안에 TODO로 표시)

### 우선순위(데이터 충돌 해결)

1. 날짜/시간/장소/행사 안내/문구: `index.md` 우선
2. 세션/연사(있을 때): `speakers.csv` 우선
3. sponsors(후원): `images/`에 `sponsor-`로 시작하는 이미지가 있으면 모두 노출, 없으면 후원 섹션 생략

## 폴더 구조(표준)

- `{YYYY}/{MM}/{event-slug}/`
  - `index.md` (필수, 콘텐츠 원본)
  - `index.html` (출력)
  - `images/` (필수, 이미지 자산)
  - `speakers.csv` (선택, 연사/세션 확정 데이터)

## index.md 작성 규칙(콘텐츠 계약)

`index.md`에는 다음 정보가 반드시 있어야 한다.

### 1) 상단 기본 정보

- 제목: 최상단 H1 1개
- 한 줄 소개(부제): 제목 아래에 1줄(굵게 권장)
- 일정/시간/장소: 날짜, 시간 범위, 장소 3줄(불릿 또는 문장)

### 2) "이런 분들을 위한 행사입니다" 섹션

- 정확히 3개 항목(각각 소제목 + 본문 1~3문단)

### 3) 키노트 섹션(선택)

- 키노트가 확정이면: 이름, 직함/소속, (선택) 이미지
- 미정이면: "추후 공지" 텍스트만 유지

### 4) 시간표 섹션

- 표 형태(시간 | 내용)를 우선 사용
- `speakers.csv`가 있는 경우, 시간표의 "세션 구간"은 CSV를 기반으로 채운다(등록/네트워킹 등 비세션 항목은 `index.md`에서 가져온다).

### 5) 행사 안내 섹션(필수)

- 장소(주소), 대상, 주차, 문의 이메일

### 6) 후원 섹션(선택)

- `images/`에 `sponsor-`로 시작하는 이미지가 있으면 모두 나열, 없으면 섹션 자체를 생략한다.

### 7) CTA 링크(필수, 고정 키워드 1줄)

AI가 안정적으로 링크를 찾기 위해, 아래 키워드 1줄을 반드시 포함한다.

- `참가신청링크: https://example.com/registration`

만약 이 줄이 없다면, CTA의 `href`는 `#`로 두고 버튼 근처에 "TODO: 참가신청링크를 index.md에 추가하세요" 문구를 노출한다.

## speakers.csv 규격(있을 경우)

### 파일 의미

- `speakers.csv`는 "세션/연사 확정 데이터"다. 존재한다면 세션 카드와 시간표의 세션 항목은 CSV를 우선으로 반영한다.

### 헤더(필수)

`time,profile,name,organisation,session-title,session-description,linkedin,github` (순서 고정)

### 필드 규칙

- `time`: 예) `13:10 - 13:40`
- `profile`: 반드시 상대경로. 예) `images/mina-jin.png`
- `name`: 발표자 이름
- `organisation`: 소속/직함(짧게)
- `session-title`: 세션 제목
- `session-description`: 세션 설명(비어있으면 세션 카드에서 설명 영역을 생략)
- `linkedin`: 발표자 LinkedIn URL (선택)
- `github`: 발표자 GitHub URL (선택)

### 정렬

- CSV 행 순서대로 시간표와 세션 카드를 생성한다.

## images/ 규칙

- 히어로(배너) 이미지는 `images/` 안에서 다음 우선순위로 선택한다.
  1. 파일명에 `hero-`로 시작하는 이미지
  2. 파일명에 `landscape`를 포함하는 이미지
  3. 그 외 가장 "배너에 적합한" 가로형 이미지(합리적 추정)
- 연사 프로필 이미지는 `speakers.csv`의 `profile` 값을 그대로 사용한다.
- 후원 로고는 `images/sponsor-*.png` 형태가 있으면 모두 후원 섹션에 나열한다(없으면 섹션 생략).

## index.html 구성(섹션 순서 고정)

아래 섹션 순서를 반드시 지킨다.

1. 상단 배너 이미지(히어로 이미지 전체 폭)
2. 히어로 섹션(그라데이션 배경, 행사명/부제, 날짜/시간/장소 카드)
3. 주요 특징("이런 분들을 위한 행사입니다" 3개 카드)
4. 키노트 섹션(키노트 카드)
5. 시간표 섹션(타임라인/테이블)
6. 세션 소개 섹션
   - `speakers.csv`가 있으면: CSV 기반 세션 카드 반복
   - 없으면: "연사/세션 준비 중" 안내 문구 표시
7. 행사 안내 섹션(2x2 그리드: 장소/대상/주차/문의)
8. 후원 섹션(선택: `sponsor-*` 이미지가 있을 때만)
9. CTA 섹션(참가 신청 링크 버튼 + 안내사항)
10. 푸터(행사 요약 + 관련 링크)

## 디자인/스타일 규칙

- 폰트 스택: `Pretendard`, `Noto Sans KR`, 시스템 폰트 계열
- 주요 색상 톤: Azure 블루 계열 중심 + 보조 포인트(보라) + 밝은 회색 배경
- 레이아웃
  - 섹션 패딩은 넉넉하게(예: `60px 40px` 수준), 히어로/CTA는 더 큼(예: `80px 40px` 수준)
  - 콘텐츠 최대 폭은 `900px` 중심, 후원은 `1000px` 수준까지 허용
- 컴포넌트 룩앤필
  - 라운드(예: `12~15px`), 단정한 그림자/테두리
  - 세션 카드는 "테두리 + 상단 그라데이션 헤더 + 본문" 구조 유지
- 반응형
  - 최소 `320px` 폭에서 읽을 수 있어야 한다.
  - 2x2 그리드는 작은 화면에서 자연스럽게 줄바꿈되도록 한다.

## 생성 후 자체 검증 체크리스트

- `index.md`의 날짜/시간/장소/주소/문의 문구가 `index.html`과 1:1로 일치하는가?
- `images/` 경로가 모두 상대경로(`images/...`)인가?
- `참가신청링크`가 있으면 CTA가 `<a href>`로 실제 링크인가? 없으면 TODO 문구가 노출되는가?
- `speakers.csv`가 있으면 세션 카드/시간표 세션 항목이 CSV와 일치하는가?
- `speakers.csv`의 `session-description`이 빈 행은 "설명 영역"을 생략했는가?
- `sponsor-*` 이미지가 있으면 후원 섹션이 생성되고 모두 노출되는가?

## (선택) AI에게 요청하는 한 줄 예시
이 폴더에는 이 템플릿 문서와 `index.md`, `images/`, (선택) `speakers.csv`가 있다. 템플릿 문서의 AI 실행 지침을 그대로 따라 같은 폴더에 `index.html` 단일 파일을 생성하라.
