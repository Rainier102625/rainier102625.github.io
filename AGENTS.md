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

**Override 구조:**

- `_includes/sidebar.html` — 테마 기본 사이드바를 완전히 교체한 커스텀 사이드바
- `_layouts/home.html` — 홈페이지 레이아웃 커스터마이즈 (핀 포스트, 페이지네이션 로직 포함)
- `_sass/custom.scss` — 전체 레이아웃 중앙 정렬(max-width: 1200px), 사이드바 카테고리 스타일, 아바타 크기 등 스타일 오버라이드
- `_sass/layout/_sidebar.scss` — 사이드바 상세 스타일 (CSS 변수 `--sidebar-bg`, `--sidebar-active-color` 등 사용)

**사이드바 구성:**

1. 프로필 (아바타 + 사이트 제목 + tagline)
2. 탭 네비게이션 — `_tabs/` 폴더의 파일들이 `site.tabs` collection으로 자동 수집됨
3. 카테고리 목록 — `site.categories`에서 자동 생성, `/categories/:slug/` 링크
4. 하단 연락처 아이콘 — `_data/contact.yml`로 설정

**카테고리 시스템:**

- 포스트 front matter에 `categories: [주제]` 작성
- `jekyll-archives` 플러그인이 `/categories/:name/` 페이지 자동 생성 (`_config.yml`에 설정됨)
- 사이드바와 홈 카드에 자동 반영

**포스트 작성:**

- `_posts/YYYY-MM-DD-title.md` 형식으로 파일 생성
- front matter 필수 항목: `title`, `date`, `categories`
- `pin: true` — 홈 상단 고정
- `hidden: true` — 홈 목록에서 숨김
- `last_modified_at` — `_plugins/posts-lastmod-hook.rb`가 git 이력으로 자동 설정

**탭 추가:**

- `_tabs/` 에 md 파일 추가 후 front matter에 `layout`, `icon`(Font Awesome 클래스), `order` 지정

**소셜 링크 추가:**

- `_data/contact.yml`에 항목 추가 (현재 github, twitter, email, rss 활성화됨)
