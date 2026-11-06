# HJW 포트폴리오

자기소개, 관심 분야, 학습 계획, 기술 역량, 프로젝트를 정리한 개인 포트폴리오 사이트입니다.

- 사이트: https://jiwon051.github.io/JW-Profile/
- 테마: [Tella](https://github.com/opera7133/tella) (MIT, `LICENSE`)

## Requirements

| 도구 | 버전 | 설치 |
|---|---|---|
| Git | 2.x | https://git-scm.com |
| Hugo | 0.154.5 extended | Windows 기준: [릴리스 페이지](https://github.com/gohugoio/hugo/releases/tag/v0.154.5)에서 hugo_extended_0.154.5_windows-amd64.zip을 받아 압축을 풀고 폴더를 PATH에 추가 (macOS·Linux는 같은 페이지에서 운영체제에 맞는 hugo_extended_0.154.5_... 파일 사용) |
| Node.js | 24 (npm 포함) | https://nodejs.org |
| Python | 3.12 이상 | https://www.python.org |


```bash
git --version
hugo version
node -v
python --version
```

GitHub Actions도 같은 버전을 사용 (.github/workflows/hugo-pages.yml)

## Getting started

### 1. 저장소 받기와 패키지 설치

```bash
git clone https://github.com/jiwon051/JW-Profile.git
cd JW-Profile/site
npm install
```

### 2. 로컬에서 사이트 확인

site 폴더에서 실행한다.

> `npm install`을 하지 않으면 Tailwind CSS 단계에서 `"npx" is not whitelisted` 오류 발생

```bash
hugo server --config hugo.toml,pages.json
```

터미널에 표시된 주소(http://localhost:1313/JW-Profile/)로 접속한다. 파일을 저장하면 화면이 자동으로 새로고침된다.

### 3. 배포와 같은 방식으로 빌드

저장소 맨 위 폴더(`JW-Profile/`)에서 실행. GitHub Actions가 실행하는 명령과 같다.

```bash
python .github/pages_build.py --dependencies
python .github/pages_build.py --build
```

빌드 완료가 출력되고 public/index.html이 만들어지면 성공. public/과 .pages-tools/는 .gitignore에 포함되어 커밋되지 않는다.

## Editing

| 바꿀 것 | 파일 |
|---|---|
| 사이트 제목, 메뉴, 로고 | site/hugo.toml |
| 홈 슬라이드 문구·이미지·버튼 | site/data/slide.json |
| 소개 페이지 | site/content/about.md |
| 블로그 글 | site/content/blog/*.md |
| 프로젝트 | site/content/products/*.md |
| 이미지 | site/static/img/ (blog/, project/, slide/, logo/) |
| 디자인 (CSS) | site/static/css/custom.css |
| 레이아웃 | site/layouts/ |

테마 원본 site/themes/template/은 직접 고치지 않고 같은 경로로 site/layouts/에 복사해서 수정한다.
수정한 뒤에는 [Getting started](#getting-started)의 hugo server로 화면을 먼저 확인한다.

## Deploy

main 브랜치에 push하면 GitHub Actions가 자동으로 빌드하고 배포한다. 저장소 맨 위 폴더에서 실행한다.

```bash
git add .
git commit -m "변경 내용"
git push origin main
```

### Actions 확인

1. https://github.com/jiwon051/JW-Profile/actions 를 연다.
2. 방금 push한 커밋 메시지의 Deploy Hugo to GitHub Pages 실행을 누른다.
3. build와 deploy가 모두 초록색 체크(✓)이면 성공, 빨간색(✗)이면 해당 단계를 눌러 로그를 확인하고 수정 후 다시 push한다.

### 공개 화면 확인

  https://jiwon051.github.io/JW-Profile/ 에서 변경한 페이지를 연다.

Pages 설정은 Settings → Pages → Build and deployment → Source: GitHub Actions로 되어 있어야 한다.

## Credits

| 자료 / 사용 위치 | 구분 | 원본 URL 또는 도구 | 이용 조건 |
|---|---|---|---|
| Tella 테마 / `site/themes/template/` | 외부 | https://github.com/opera7133/tella | MIT, `LICENSE` 고지 유지 |
| Splide 슬라이더 / `site/themes/template/static/js/` | 외부 | https://splidejs.com | MIT |
| Bootstrap Icons / `site/themes/template/static/css/` | 외부 | https://icons.getbootstrap.com | MIT |
| Tailwind CSS / `site/package.json` | 외부 | https://tailwindcss.com | MIT |
| 글꼴 Montserrat, Open Sans | 외부 | Google Fonts | SIL Open Font License |
| 배포 스크립트 / `.github/` | 외부 | `prepare_github_pages.py` | 수업 자료 |
| 소개·블로그·프로젝트 글 / `site/content/` | 직접 | 직접 작성 | - |
| 로고 / `site/static/img/logo/logo.png` | 직접 | 직접 제작 | - |
| 파비콘 / `site/static/favicon*`, `site/static/apple-touch-icon.png`, `site/static/android-chrome-*.png` | 직접 | https://readdy.ai/ko/tools/favicon-generator | - |
| 블로그 표지 / `site/static/img/blog/data-analysis.jpg`, `it-service.jpg`, `plan.jpg`, `site/static/img/blog/skill.png` | AI | Claude | AI 생성 |
| 홈 슬라이드 이미지 / `site/static/img/slide/` | AI | Claude | AI 생성 |
| 페이지 CSS·HTML 일부 / `site/static/css/custom.css`, `site/content/` | AI | Claude | AI 초안을 직접 수정·검토 |
| 접근성·경로 수정 / `site/layouts/`, `.github/pages_build.py` | AI | Claude | AI와 수정 후 직접 동작 확인 |