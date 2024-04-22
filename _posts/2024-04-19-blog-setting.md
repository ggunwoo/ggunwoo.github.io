---
title: Jekyll, Chirpy theme로 Github Pages 블로그 시작하기
date: 2024-04-19 18:16:00 +0900
categories: [Blog, Jekyll]
tags: [blog, setting, jekyll, chirpy, github pages]
---

<br />

## 서론

> &nbsp;해당 글은 재가 [Jekyll Theme](https://github.com/topics/jekyll-theme) 중에서 [Chirpy 테마](https://github.com/cotes2020/jekyll-theme-chirpy)를 사용하여 Github Pages 블로그를 개설하는 과정을 설명하고 있습니다. 다른 분들의 과정이 다를 수 있습니다. 다른 테마를 사용하시는 경우에도 과정이 다를 수 있습니다.
>
> [Chirpy 공식문서 시작 가이드](https://chirpy.cotes.page/posts/getting-started/)
>
> Windows, wsl2, Ubuntu를 사용했습니다.  
> macOS 경우 과정을 직접 경험하지 못했습니다.
>
> wsl2와 Ubuntu를 설치하려면?  
> [(WSL) Windows에서 Ubuntu bash 사용하는 방법 - Ju-ing님의 블로그](https://blog.ju-ing.com/posts/WSL-ubuntu-bash-install/)

<!-- > [[Windows] WSL2로 리눅스 설치 및 기본 사용법 - LainyZine님의 블로그](https://www.lainyzine.com/ko/article/how-to-install-wsl2-and-use-linux-on-windows-10/) -->

<br />

> 게시물에 링크가 많습니다. **Ctrl + left click** / **&#8984; + click** 을 이용하시면 새 탭에서 열 수 있습니다.

<br />

## Chirpy Theme 설치

Chirpy의 시작옵션은 3가지가있습니다.

1. [Chirpy Starter](https://github.com/new?template_name=chirpy-starter&template_owner=cotes2020)를 사용하여 직접 설치
1. [소스코드(.zip)](https://github.com/cotes2020/jekyll-theme-chirpy/releases)를 직접 다운받아 설치
1. [Chirpy Github](https://github.com/cotes2020/jekyll-theme-chirpy) 저장소를 [fork](https://github.com/cotes2020/jekyll-theme-chirpy/fork)받아서 설치

초기설정 작업이 복잡하지만 UI 커스터마이징에 이점이 있어서 3번, Fork 방식으로 설치를 진행했습니다.

<!-- 저는 초기설정 작업이 필요로 하지만 UI 커스터마이징에 이점이있는 3번 fork 방식으로 설치했습니다. -->

<br />

### 1. Repository(저장소) Fork

<img width="80%" src="/assets/img/posts-img/240419/fork_01.png" alt="fork" />

Chirpy저장소에서 fork한 후 <span style="color:yellowgreen">Create fork</span>를 클릭하시면 내 저장소에 jekyll-theme-chirpy가 복제되어 자동으로 생성됩니다..

<br />

### 2. Fork한 저장소 이름 바꾸기

<img width="90%" src="/assets/img/posts-img/240419/change_name_01.png" alt="changeName" />

fork한 내 원격저장소에서 Settings 탭 -> General -> Repository name을 [GtiHub ID].github.io로 작성하신 후 Rename을 눌러 바꿔주시면됩니다.

> jekyll-theme-chirpy -> [GitHub ID].github.io

<br />

### 3. 원격저장소에서 로컬로 가져오기

```shell
git clone https://github.com/[GitHub_ID]/[GitHub_ID].github.io.git
```

로컬환경에서 Shell을 열어 설치를 원하시는 위치로 이동한 뒤 Fork한 저장소를 Clone해서 로컬폴더를 만들어줍니다.

<br />

### 4. 로컬 **Chirpy 초기화** 하기

```shell
bash tools/init # 또는 bash tools/init.sh
```

저는 여기서 많이 헤맸는데요.  
Chirpy 사용하기 위해선 `tools/init`초기화 작업을 꼭 진행해야합니다.  
로컬폴더에 /tools/init 파일을 bash로 실행시키는 명령어이며, Unix계열 운영체제에서 사용이 가능하다고 합니다.  
macOS나 Linux에선 바로 실행이 가능하지만 Windows에서 사용하기위해 Linux환경을 구축해야하며 WSL(Windows Subsystem for Linux)가 필요합니다.

> _WSL2 설치하려면?_  
> [(WSL) Windows 에서 Ubuntu bash 사용하는 방법 - Ju-ing님의 블로그](https://blog.ju-ing.com/posts/WSL-ubuntu-bash-install/){:target="\_blank"}

macOS를 사용하신다면 초기화해주시고 다음으로 넘어가시면 되겠습니다.

<br />

#### 4-1. (windows) Linux 환경에서 최신 버전의 node.js를 설치

wsl2와 Ubuntu 설치하셨다면 Linux환경에 최신 버전의 node.js를 설치해야합니다.

바로 Ubuntu에서 `sudo apt install node` 명령으로 node를 설치하시면 `tools/init` 명령어가 정상적으로 실행되지 않습니다. 왜냐하면 Ubuntu에 포함된 node.js는 v12.22.9 버전이기 때문입니다. 그렇기에 node.js를 최신버전 설치는 필수로 진행해야합니다.

24년 4월 19일 기준으로 node.js의 최신버전은 21.7.1버전이고 LTS버전은 20.12.0 입니다. 최신 버전은 불안정하고 일부 모듈이 작동하지 않을 수 있으니 20.x 버전을 curl로 다운받는 방법을 설명하겠습니다.

> [공식사이트](https://nodejs.org){:target="\_blank"}_에서 node.js 최신버전을 확인할 수 있습니다._

<br />

Ubuntu을 실행하여 다음 명령을 순서대로 실행해주세요.

```shell
sude apt update
```

```shell
sudo apt-get install curl
```

```shell
curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
```

```shell
sudo apt-get install nodejs npm
```

설치가 완료되셨으면 `node -v`, `npm -v`명령으로 최신버전인지 확인합니다.

<br />

#### 4-2. (windows) npm 설치 후 초기화

다시 로컬환경에서 Shell을 열어주시고 Chirpy폴더로 이동합니다.

Shell 명령으로 `bash` 혹은 `wsl`을 입력하시면 Linux환경으로 로컬폴더를 열 수 있습니다.  
다시 `bash tools/init`명령을 실행하시면 초기화가 진행 됩니다.

<br />

여기서 저 같은 경우 초기화가 진행되지않으면서 다양한 문제를 경험하게 되었는데요.

- _error 1_ : tools/init: line : $'\r': command not found

  > Windows와 Linux는 개행방식(줄바꿈 등)이 달라서 생긴 문제입니다.
  >
  > 저는 /tools/init 파일을 에디터로 열어 LF로 바꿔서 해결했습니다.
  > <img width="70%" src="/assets/img/posts-img/240419/crlf_error.png" alt="crlf_error" />
  >
  > 개행방식을 _LF_ 바꿨다면 `init` 파일을 `git add --all` 해주세요.  
  > git add를 진행하지않으면 `init`파일 `line:45`에 의해서 파일이 staging 상태가 아니라는 Error 코드가 뜨게됩니다.
  >
  > `Error: Commit unstaged files first, and then run this tool again.`

<br />

- _error 2_ : mv: cannot stat '.github/workflows/starter/pages-deploy.yml': No such file or directory

  > `init` 파일 `line:93`
  >
  > github action, workflow를 실행시킬 pages-deploy.yml파일 또는 경로에 문제가 있다는대요.
  >
  > 로컬폴더에서 Linux환경으로 `npm install`을 실행해서 해결했습니다.

<br />

- _error 3_ : 초기화를 진행해도 /assets/js/dist 폴더에 `.js` 생성되지않은 문제 (NODE_ENV 환경 변수 에러)

  > 최상위 폴더에 `rollup.config.js`와 `package.json`에 script섹션 build스크립트에서 확인이 가능합니다.  
  > `"build": "NODE_ENV=production npx rollup -c --bundleConfigAsCjs",`
  >
  > \_javsciprt에 .js 파일을 dist에 .min.js로 번들링 해주는 `rollup.config.js`가 무슨 이유에서인지 run build로 실행되지않아서 생긴 문제로 보여집니다.
  >
  > `NODE_ENV=production`: 프로젝트를 배포환경으로 설정  
  > `npx rollup -c`: Rollup으로 `rollup.config.js`을 실행
  >
  > 터미널에서 직접 `npm run build`하거나 저는 직접 build 스크립크를 터미널에서 실행해서 해결했습니다.
  >
  > ```terminal
  > NODE_ENV=production npx rollup -c --bundleConfigAsCjs
  > ```

<img width="80%" src="/assets/img/posts-img/240419/reset_success.png" alt="reset_success">

모든 error를 해결 후 다시 `bash tools/init`을 실행하여 초기화를 진행했습니다.🥳🥳

<br />

## **로컬**에서 Jekyll 실행

Github Pages에 업로드하기전 로컬서버에서 작업할 수 있는 환경을 jekyll로 구축합니다.  
`ruby`로 `bundle` 을 설치한 후 `jekyll serve` 서버를 실행 시킬 수 있습니다.

<br />

### 1. ruby 설치

[Jekyll Installation](https://jekyllrb.com/docs/installation/){:target="\_blank"}

Jekyll을 사용하기 위해서 먼저 ruby를 설치해 주시면 됩니다. 운영체제마다 설치 방법이 상이합니다.

- macOS - Bomebrew

```shell
brew install ruby
```

- Windows - [Ruby Installer](https://rubyinstaller.org/downloads/){:target="\_blank"}

wsl로 설치 하는 방법이 있지만 저는 설치가 진행 되지않아서 홈페이지에서 직접 설치했습니다.

1. WITH DEVKIT - 가장 위에있는 => Ruby+Devkit 3.2.3-1 (x64) 다운로드 _- 2024.04.19_
1. `.exe` 파일을 실행하여 ruby 설치
1. 설치가 완료되면 `Start Command Prompt with Ruby` 실행
1. 아래 명령을 실행

```ruby
gem install jekyll minima bundler jekyll-feed tzinfo-data
```

`5 gems installed`을 확인한 뒤 `jekyll -v` 및 `bundler -v`로 설치 확인

<br />

### 2. 의존성 모듈 설치하기

로컬폴더로 돌아와 아래 명령을 실행하여 모듈을 설치합니다.

```shell
bundle
```

> 저는 Linux환경말고 Windows shell(터미널)에서 실행해야 설치가 진행 되었습니다.

<br />

### 3. Jekyll 실행하기

의존성 모듈까지 설치해서 Chirpy폴더에 `Gemfile.lock`이 생성되었다면 아래 명령으로 로컬서버를 실행합니다!

```shell
jekyll serve
```

실행되지 않을 경우 `bundle exec jekyll s`명령을 실행합니다.

<img src="/assets/img/posts-img/240419/jekyll.png" alt="jekyll실행" />

🤔 음.. 서버 주소가 [4000포트](http://localhost:4000/) 라고 적혀있네요.

<br />

<img src="/assets/img/posts-img/240419/jekyll-run.png" alt="jekyll" />

정상적으로 실행되었다면 `tools/init`을 실행하여 초기화된 상태에 Chirpy UI가 보입니다!

> 만약 초기화를 진행하지않게되면 서버에 `.js` 파일이 없다는 문구가 계속 뜨게되며 많은 요소들이 재기능하지 못하게 됩니다.

<br />

## GitHub Pages로 배포하기

이제 마지막으로 Github Pages로 push하여 블로그를 배포하겠습니다.
저는 초기화가 진행되면서 원격저장소와 로컬저장소의 차이때문에 push가 진행 되지않았습니다.
여기서 GitHub 파일들을 Pull 또는 fetch 해버리면 다시 초기화를 진행해야합니다.

~~_저는 두번 했습니다...._~~

<br />

### 1. 초기 설정 (\_config.yml)

로컬 최상위 폴더에 있는 `_config.yml`은 블로그 환경을 설정할 수 있습니다.  
해당 글에서는 배포하기전 기본 설정만 다루고 자세한 설정은 다음 글에서 다루겠습니다!

- `lang` : `ko-KR`, 언어를 한글로 설정하고 기본값은 en `/_data/locales/ko-KR`
- `timezone` : `Asia/Seoul` 한국 표준시(UTC +0900)로 설정
- `title` : 블로그 왼쪽 사이드바 제목
- `tagline` : 제목 아래 슬로건
- `url` : `https://[GitHub ID].github.io` 로 설정

<br />

### 2. 첫번째 포스팅 해보기

블로그 게시물은 `/_posts`에 `.md`, `.markdown` 확장자 파일들로 구성됩니다.  
글을 작성 요령은 아래와 같습니다.

1. 파일명 : **YYYY-MM-DD-URL_NAME.md**
1. 확장자는 `.md ` 또는 `.markdown`를 사용해야합니다.
1. 파일명에서 공백을 사용할 수 없습니다. `-`로 대체해야합니다.
1. 게시물은 꼭 `/_posts` 폴더에 작성해야합니다.
1. Front Metter를 사용해 글의 레이아웃을 구성합니다.
   [Front Metter 공식문서](https://chirpy.cotes.page/posts/write-a-new-post/#front-matter)

```markdown
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG] # TAG names should always be lowercase
---
```

Front Metter는 기본적으로 게시물 최상단에 위치해야하며 아래와 같이 작성해야합니다.

```markdown
---
title: Jekyll, Chirpy theme로 Github Pages 블로그 시작하기
date: 2024-04-19 18:16:00 +0900
categories: [Blog, GitHub Pages]
tags: [blog, setting]
---
```

> 설정을 마치셨으면 push하기 전에 `.gitignore` 파일에서 `Gemfile.lock`을 추가해서 staged에 올라갈 파일에서 제외시켜주세요.

<br />

### 3. Add Commit Push

이제 수정한 파일들을 원격저장소에 commit하면 자동으로 배포까지 진행하게 됩니다.

저같은 경우 원격저장소에 변경이력이 떠서 강제로 push하는 방법을 선택했습니다.

#### `git add` 전에 확인사항

1. .gitignore 목록에 `Gemfile.lock`이 적혀있는지 확인

> 모든 파일을 Staging 상태로 만든 뒤 commit해줍니다.
>
> ```shell
> git add .
> ```
>
> ```shell
> git commit -m 'initial commit'
> ```
>
> 만약 개행방식 경고가 뜬다면?  
> `git config --global core.autocrlf true` 명령을 실행해주세요.  
> 파일을 staging 상태로 만들 때 자동으로 LF를 CRLF로 변경해줍니다.  
> 이후 commit시 다시 CRLF에서 LF로 변경한 후 commit합니다.

#### push전 확인 및 설정사항

1. Github Free 요금제를 사용중이라면 저장소는 항상 Public 상태여야합니다.
1. Github 원격저장소 -> setting -> pages -> Build and deployment -> Source를 Deploy from ad branch 에서 GitHub Actions로 변경해주기

> 원격저장소 따위 무시하고 강제 push
>
> ```shell
> git push -u origin master --force
> ```

<br />

### 4. Github action 확인하기

방금 원격저장소로 push한 "initial commit" commit이 `.github/workflows/pages-deploy.yml`에 의해서 자동으로 Build -> Deployment를 진행하게됩니다.  
Github 저장소의 Actions탭에서 진행상황을 확인할 수 있습니다.

<img width="70%" src="/assets/img/posts-img/240419/action_01.png" alt="action01" />

<img width="70%" src="/assets/img/posts-img/240419/action_02.png" alt="action02" />

commit이 workflow에서 오류가 없다면 초록불이 들어온 뒤 자동으로 배포하게되며,  
`[Github ID].github.io`을 주소창에 입력하면 Github Pages에 배포된 Chirpy UI를 확인하실 수 있습니다. 🥳🥳🥳

<br />

## 마무리

블로그 개설하면서 많은 사람들의 도움을 받은만큼 이 글도 누군가에 도움이 되었으면 좋습니다. 재가 진행해온 과정에서 생략없이 작성되었지만 모두가 같은 환경이 아니기때문에 이대로 진행한다해도 오류가 있을 수 있겠지만 꼭 해결되시길 바랄게요!

다음 글에선 Chirpy 테마 커스터마이징하는 글을 작성해볼까합니다. 읽어주셔서 감사합니다!

<br />
<br />
<br />

> 블로그 개설에 도움을 받은 자료
>
> - [Jekyll Chirpy 테마 사용하여 블로그 만들기 - 하얀눈길님의 블로그](https://www.irgroup.org/posts/jekyll-chirpy){:target="\_blank"}
> - [[개발자 블로그] Jekyll의 Chirpy테마로 깃허브 블로그 만들기 - J1mmyson님의 블로그](https://j1mmyson.github.io/posts/StartingBlog){:target="\_blank"}
> - [Github blog 만들기 (chirpy theme) - Ju-ing님의 블로그](https://blog.ju-ing.com/posts/Github-blog-chirpy-theme){:target="\_blank"}
> - [jekyll/Chripy로 GitHub Pages 만들기 - NUGA님의 블로그](https://nugabox.github.io/posts/jekyll-Chirpy%EB%A1%9C-GitHub-Pages-%EB%A7%8C%EB%93%A4%EA%B8%B0){:target="\_blank"}
> - [Chirpy 테마 적용 시 \*.min.js 문제 - 김세훈님의 블로그](https://syehoonkim.github.io/posts/applying_chirpy_theme){:target="\_blank"}
