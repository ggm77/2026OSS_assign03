22300378 서하민

# Assignment 03 - Multi-Page CRUD Frontend (Note CRUD)

## Service Topic

**Note CRUD** — 개인용 노트(메모) 관리 서비스입니다. 사용자가 노트를 작성, 조회, 수정, 삭제할 수 있는 4개 페이지 기반의 Multi-Page CRUD 웹 애플리케이션입니다.

## Data Fields

노트 하나는 아래 7개의 Field로 구성됩니다.

| Field | 설명 |
|---|---|
| 번호 (id) | 노트를 식별하는 고유 번호 |
| 제목 (title) | 노트의 제목 (2~50자) |
| 카테고리 (category) | 업무 / 개인 / 아이디어 / 학습 / 여행 / 기타 중 선택 |
| 중요도 (priority) | 낮음 / 보통 / 높음 중 선택 |
| 내용 (content) | 노트 본문 (10자 이상) |
| 생성일 (createdAt) | 노트가 처음 작성된 날짜 |
| 수정일 (updatedAt) | 노트가 마지막으로 수정된 날짜 |

## List Page (index.html)

목록 테이블에 다음 4개 이상의 Field를 표시합니다: **번호, 제목, 카테고리, 생성일, 수정일**

- `[+ Add]` 버튼 → `add.html`로 이동
- 각 행의 제목/보기 버튼 클릭 → `view.html?id=번호`로 이동
- Bootstrap `table-responsive`, `table-hover`를 이용해 반응형 테이블 구성

## Validation

`add.html`, `edit.html`에 공통으로 적용한 JavaScript Validation (6개):

1. **제목 길이 검증** — 2자 이상 50자 이하 (`title.trim().length`)
2. **카테고리 선택 여부** — Select 미선택 시 오류 표시
3. **중요도 선택 여부** — Select 미선택 시 오류 표시
4. **내용 길이 검증** — 10자 이상 입력 필수
5. **생성일 필수 입력 여부** — 날짜 미입력 시 오류 표시
6. **수정일 유효성 검증** — 필수 입력이며, 생성일보다 이전 날짜일 수 없음 (날짜 범위 비교)

Bootstrap의 `is-invalid` / `invalid-feedback` 클래스를 이용해 오류 메시지를 필드 아래에 표시합니다.

- `add.html`: 유효성 통과 시 `alert("게시물이 추가됩니다.")` 표시 후 `index.html`로 이동
- `edit.html`: 유효성 통과 시 `confirm("게시물을 수정할까요?")` 표시 후 확인 시 `view.html`로 이동

## RWD (Responsive Web Design)

- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` 적용
- Bootstrap Grid(`container`, `row`, `col-md-6`)를 이용해 Desktop에서는 2열, Mobile에서는 1열로 폼 필드 배치
- `my.css`에 `@media (max-width: 768px)`, `@media (max-width: 576px)` Media Query를 추가하여
  - 제목 폰트 크기 축소
  - 테이블 글자 크기/padding 축소
  - 버튼을 세로 100% 너비로 전환
  - 목록 상단 버튼 영역을 세로 정렬로 전환
- 모든 테이블은 `table-responsive`로 감싸 Mobile에서 가로 스크롤 가능하도록 처리

## Bootstrap

사용한 주요 Bootstrap 5.3 컴포넌트 / 클래스:

- `navbar`, `navbar-expand-lg`, `navbar-toggler` (반응형 네비게이션)
- `container`, `row`, `col-md-6`
- `table`, `table-hover`, `table-responsive`, `table-dark`
- `form-control`, `form-select`, `form-label`, `is-invalid`, `invalid-feedback`
- `btn`, `btn-primary`, `btn-outline-secondary`, `btn-danger`, `btn-sm`
- `card`, `badge`
- `example.html`은 Bootstrap 공식 예제 중 **Jumbotron** 템플릿을 참고하여 제작

## Problem & Solution

- **문제**: 여러 페이지(`view.html`, `edit.html`)에서 동일한 Sample Data 배열을 각각 선언해야 해서 중복이 발생했습니다.
  **해결**: 과제 범위상 별도 백엔드/스토리지 없이 각 페이지에 필요한 최소한의 Sample Data만 두고, URL Query String(`?id=`)으로 페이지 간 선택한 데이터를 전달하는 방식으로 구현했습니다.
- **문제**: Bootstrap 기본 유효성 스타일(`novalidate` + `:invalid`)만으로는 커스텀 조건(길이, 날짜 비교 등)을 표현하기 어려웠습니다.
  **해결**: `novalidate` 속성으로 브라우저 기본 검증을 끄고, JavaScript로 직접 각 필드를 검사한 뒤 `is-invalid` 클래스를 토글하는 방식으로 구현했습니다.

## Reflection

Bootstrap Grid와 Media Query를 함께 사용하면서, Bootstrap이 제공하는 반응형 유틸리티만으로 해결되지 않는 세부적인 레이아웃(버튼 전체 너비화, 폰트 크기 조정 등)은 직접 Media Query를 작성해야 한다는 점을 배웠습니다. 또한 여러 페이지에 걸쳐 하나의 리소스(노트)를 CRUD 하는 흐름을 설계하면서, Query String을 이용한 페이지 간 데이터 전달 방식에 익숙해질 수 있었습니다.
