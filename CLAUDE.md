# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# 로컬 서버 실행
bundle exec jekyll s

# 의존성 설치
bundle install
```

## Architecture

**Theme:** `jekyll-theme-chirpy` (~> 7.5) — 테마 원본 파일은 gem에 있으며 `bundle info --path jekyll-theme-chirpy`로 위치 확인 가능. 이 repo의 파일들은 테마를 오버라이드한다.

**테마 원본 경로:** `C:\Ruby34-x64\lib\ruby\gems\3.4.0\gems\jekyll-theme-chirpy-7.5.0`

**Override 구조:**

- `_includes/sidebar.html` — 커스텀 사이드바 (프로필 + 카테고리 트리뷰 + 연락처)
- `_includes/topbar.html` — 커스텀 topbar (탭 네비게이션 + 검색, breadcrumb 제거됨)
- `_layouts/home.html` — 홈페이지 레이아웃 (ListTile 카드 형태, 이미지 옆에 텍스트)
- `_layouts/category.html` — 카테고리 아카이브 페이지 (홈과 동일한 카드 형태)
- `all-posts.html` — 전체 글 페이지 (`permalink: /categories/`, 모든 포스트 날짜순 카드 표시)
- `_sass/custom.scss` — 모든 커스텀 스타일 오버라이드 (아래 CSS 구조 참고)

**사이드바 구성:**

1. 프로필 (아바타 + 사이트 제목 + tagline)
2. 카테고리 트리뷰 — 부모/자식 계층 구조, `<details>` 태그로 접기/펼치기
   - "전체 글" 링크 → `/categories/` (all-posts.html)
   - 부모 카테고리: 포스트 `categories[0]`에서 자동 추출
   - 자식 카테고리: 포스트 `categories[1]`에서 자동 추출
3. 하단 연락처 아이콘 — `_data/contact.yml`로 설정

**Topbar 구성:**

- 검색바 (왼쪽 정렬)
- 탭 네비게이션: Tags, Archives, About — 오른쪽 끝 정렬 (`_tabs/` 폴더에서 자동 수집, categories 제외)
- breadcrumb 제거됨
- 모바일에서 탭은 숨김, 사이드바 트리거 + topbar-title 표시

**CSS 구조 (`_sass/custom.scss`):**

- 전체 레이아웃 중앙 정렬 (`max-width: 1200px`, 사이드바 위치 보정)
- 홈 카드 ListTile 이미지 (`#post-list .card .preview-img` — 130x130px, `object-fit: cover`)
- 사이드바 카테고리 트리뷰 (`#sidebar .category-tree`)
  - `.tree-total` — 전체 글 링크 스타일
  - `.tree-parent` / `.tree-children` — 부모/자식 카테고리 스타일
  - `.tree-leaf` — 자식 없는 단독 카테고리
  - `.tree-count` — 포스트 수 배지
- 검색바 (`#search` — `margin-right: auto`로 왼쪽 정렬)
- Topbar 탭 (`#topbar-tabs` — `margin-left: auto`로 오른쪽 끝 정렬)
- 아바타 크기 (`#sidebar #avatar` — 9.5rem)

**카테고리 시스템:**

- 포스트 front matter에 `categories: [부모, 자식]` 형태로 작성 (1단계만 쓰면 단독 카테고리)
- `jekyll-archives` 플러그인이 `/categories/:name/` 페이지 자동 생성 (`_config.yml`에 설정됨)
- 사이드바 트리뷰에 자동 반영 (부모-자식 계층 구조)
- 각 카테고리 아카이브 페이지는 `_layouts/category.html`로 홈과 동일한 카드 형태

**포스트 작성:**

- `_posts/YYYY-MM-DD-title.md` 형식으로 파일 생성
- front matter 필수 항목: `title`, `date`, `categories`
- `image:` — 홈 카드에 ListTile 형태로 썸네일 표시
- `pin: true` — 홈 상단 고정
- `hidden: true` — 홈 목록에서 숨김
- `last_modified_at` — `_plugins/posts-lastmod-hook.rb`가 git 이력으로 자동 설정

**탭 (Topbar):**

- `_tabs/` 에 md 파일 추가 후 front matter에 `layout`, `icon`(Font Awesome 클래스), `order` 지정
- 현재 활성: tags, archives, about (categories는 삭제됨 — 사이드바 트리뷰로 대체)

**소셜 링크 추가:**

- `_data/contact.yml`에 항목 추가 (현재 github, twitter, email, rss 활성화됨)

## CSS 참고사항

- 테마 CSS가 `!important` 없이도 높은 명시도를 가지므로, 오버라이드 시 `!important` 필요할 수 있음
- `.name` (class) vs `#name` (id): id가 명시도 더 높음 (100 vs 10)
- flexbox에서 `margin-left: auto`는 해당 요소를 오른쪽 끝으로 밀어줌
- `.부모 .자식` 선택자로 특정 컨텍스트의 요소만 스타일 변경 가능
