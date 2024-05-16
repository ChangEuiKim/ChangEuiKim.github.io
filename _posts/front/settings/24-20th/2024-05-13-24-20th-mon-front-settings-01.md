---
title: '[Frontend] 개발환경 설정하기'
layout: single
categories:
  - Frontend
  - Settings
tags:
  - ASAC 5기
  - Frontend
  - Settings
  - WSL2
  - Zsh
  - Oh My Zsh
  - Git

date: 2024-05-13 23:44:00 +0900
last_modified_at: 2024-05-13 23:44:00 +0900
---

# 프론트엔드 개발환경 설정하기

## 1 WSL2 설치하기

WSL2는 Windows에서 Linux 커널을 실행할 수 있도록 하는 기능입니다. WSL2를 사용하면 Windows에서 Linux 환경을 사용할 수 있어서 Docker와 같은 Linux 환경에서만 동작하는 프로그램을 Windows에서도 사용할 수 있습니다.

> 참고: Microsoft 사에서 제공하는 [WSL을 사용하여 Windows에 Linux를 설치하는 방법](https://learn.microsoft.com/ko-kr/windows/wsl/install)을 참고하여 WSL2를 설치합니다.
>
> Windows 10 버전 2004 이상(빌드 19041 이상) 또는 Windows 11을 실행해야 합니다. 이전 버전을 사용 중인 경우 [수동 설치 페이지](https://learn.microsoft.com/ko-kr/windows/wsl/install-manual)를 참고합니다.

## 2 터미널 설정하기

Git, Node 등 CLI(Command Line Interface)를 사용하는 프로그램을 사용할 때 터미널을 주로 사용합니다. 터미널 설정에 따라 생산성을 향상시킬 수 있습니다.

### 2.1 Oy My Zsh 설치하기

Ubuntu에서 사용하는 기본 쉘인 bash보다 편리한 기능을 제공하는 zsh 쉘을 설치합니다. Oh My Zsh는 zsh 쉘을 사용할 때 테마와 플러그인을 쉽게 설치할 수 있도록 도와주는 프레임워크입니다.

> 참고: [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)의 깃허브 페이지에서 더 자세한 정보를 확인할 수 있습니다.

#### 2.1.1 패키지 관리자를 업데이트합니다.

```bash
sudo apt update -y && sudo apt upgrade -y
```

- sudo: 관리자 권한으로 명령을 실행합니다.
- apt: Advanced Packaging Tool의 약자로 Debian 계열 리눅스의 패키지 관리자입니다.
- apt upgrade: 설치된 패키지를 최신 버전으로 업그레이드합니다.
- apt update: 패키지 목록을 최신 상태로 업데이트합니다.
- -y: 패키지 설치 도중 물어보는 질문에 자동으로 yes로 응답합니다.

#### 2.1.2 zsh 쉘을 설치합니다.

```bash
sudo apt install zsh -y
```

- apt install 패키지명: 패키지를 설치합니다.
- zsh는 z shell의 약자로 bash보다 편리한 기능을 제공합니다.

#### 2.1.3 Oh My Zsh를 설치합니다.

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- curl: URL을 이용하여 데이터를 전송하는 명령입니다.
- sh: 쉘 스크립트를 실행하는 명령입니다.
- -c: command 옵션으로 스크립트를 실행합니다.
- "$(URL)": URL에서 스크립트를 다운로드하여 실행합니다.

### 2.2 Zsh 플러그인 설치하기

Oh My Zsh를 사용하면 플러그인을 쉽게 설치할 수 있습니다. 플러그인은 zsh 쉘에서 사용할 수 있는 기능을 확장해주는 역할을 합니다.

> 참고: 문법 강조 플러그인 [zsh-syntax-highlighting](zsh-syntax-highlighting)와 자동완성 플러그인[zsh-autosuggestions](zsh-autosuggestions)을 설치합니다.

플러그인의 깃허브 저장소를 클론하고 Zsh의 설정 파일에 플러그인을 추가합니다.

#### 2.2.1 문법 강조 플러그인을 설치합니다.

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- Syntax Highlighting: 명령어를 입력할 때 문법에 따라 색상을 입혀서 보여줍니다.

#### 2.2.2 자동완성 플러그인을 설치합니다.

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

- Autosuggestions: 명령어를 입력할 때 이전에 입력한 명령어를 기반으로 자동완성을 제공합니다.

#### 2.2.3 플러그인을 설정 파일에 추가합니다.

```bash
vim ~/.zshrc
```

- vim: 리눅스의 텍스트 편집기입니다.
- 쉘의 설정파일은 rc 파일로 끝납니다. zsh의 설정 파일은 ~/.zshrc에 저장됩니다.
- `:set nu`를 입력해 줄 번호를 표시합니다.
- 80번째 줄에 plugins 항목이 있습니다. plugins 항목에 플러그인을 추가합니다.

  ```bash
  plugins=(
    git
    zsh-syntax-highlighting
    zsh-autosuggestions
  )
  ```

#### 2.2.4 설정 파일을 적용합니다.

```bash
source ~/.zshrc
```

- source: 설정 파일을 적용합니다. 닷 (`.`) 명령어로도 설정 파일을 적용할 수 있습니다.
- 현재 셀 세션에서 스크립트를 실행하기 때문에 새로운 셸을 열지 않아도 설정 파일이 적용됩니다.

### 2.3 Zsh 테마 설정하기

Zsh 테마는 쉘 프롬프트의 디자인을 변경해주는 역할을 합니다. Oh My Zsh를 사용하면 테마를 쉽게 변경할 수 있습니다.

> 참고: Zsh의 테마는 [Themes](https://github.com/ohmyzsh/ohmyzsh/wiki/themes)에서 확인할 수 있습니다. Git 명령어를 사용하는 경우 [agnoster-zsh-theme](https://github.com/agnoster/agnoster-zsh-theme) 테마를 사용하면 편리합니다.

#### 2.3.1 Powerline Fonts를 설치합니다.

> 참고: 파이프 (`|`) 구분이 쉬운 [D2Coding](https://github.com/powerline/fonts/tree/master/D2Coding) 폰트를 사용하면 편리합니다.

```bash
sudo apt install fonts-powerline
```

- agnoster 테마를 사용하려면 [Powerline Fonts](https://github.com/powerline/fonts)를 설치해야 합니다.
- Powerline Fonts는 특수문자를 사용하여 테마를 꾸밀 수 있도록 해줍니다.

```bash
echo "\ue0b0 \u00b1 \ue0a0 \u27a6 \u2718 \u26a1 \u2699"
```

- 해당 명령어를 입력했을때 위와 같이 출력되면 Powerline Fonts가 설치되어 있는 것입니다.

#### 2.3.2 테마를 설정합니다.

```bash
vim ~/.zshrc
```

- 테마를 설정하기 위해 zsh의 설정 파일을 엽니다.
- `:set nu`를 입력해 줄 번호를 표시합니다.
- 10번째 줄에 ZSH_THEME 항목이 있습니다. ZSH_THEME 항목에 테마를 추가합니다.

  ```bash
  ZSH_THEME="agnoster"
  ```

#### 2.3.3 설정 파일을 적용합니다.

```bash
source ~/.zshrc
```

## 3 Git 설정하기

### 3.1 사용자 정보 설정하기

Git을 사용하기 위해서는 사용자 정보를 설정해야 합니다. 사용자 정보는 커밋할 때 작성자 정보로 사용됩니다.

```bash
git config --global user.name "깃허브 계정명"
git config --global user.email "깃허브 이메일"
git config --global user.initials "이니셜"
```

- config: Git의 설정을 변경하는 명령입니다.
- --global: 전역 설정을 변경합니다.
- 해당 명령어를 입력하면 ~/.gitconfig 파일에 사용자 정보가 저장됩니다.
- 프로젝트 파일에 .gitconfig 파일이 있을 경우 전역 설정보다 로컬 설정을 우선합니다.

### 3.2 커밋 컨벤션 설정하기

커밋 메시지를 작성할 때 컨벤션을 지키면 프로젝트의 커밋 히스토리를 관리하기 쉽습니다. 커밋 컨벤션은 [Conventional Commits](https://www.conventionalcommits.org/ko/v1.0.0/)을 따릅니다.

> 참고: 커밋 컨벤션을 지키면 [Semantic Versioning](https://semver.org/lang/ko/)을 적용할 수 있습니다.

#### 3.2.1 커밋 템플릿을 설정합니다.

```bash
git config --global commit.template ~/.gitmessage
```

- commit.template: 커밋 메시지를 작성할 때 사용할 템플릿을 설정합니다.
- ~/.gitmessage: 사용자 홈 디렉토리에 .gitmessage 파일을 생성합니다.
- 커밋 템플릿은 커밋 메시지를 작성할 때 사용할 템플릿을 설정합니다.

#### 3.2.2 커밋 템플릿을 작성합니다.

```bash
vim ~/.gitmessage
```

- 커밋 템플릿을 작성하기 위해 텍스트 편집기를 엽니다.

```bash
################<타입> : <제목>################

##################구분 공백줄##################

##################구분 공백줄##################
# 위의 공백은 제목 본문 구분줄입니다. 비워주세요
# 아래에 커밋 메시지를 작성해주세요
# 여러 줄의 메시지를 작성할 땐 "-"로 구분 (한 줄은 72자 이내)
###############################################

###############################################
# 제목은 50자 이내 / 변경사항이 "무엇"인지 명확히 작성 / 끝에 마침표 금지
# feat: 새로운 기능 추가
# fix: 버그 수정
# docs: 문서 수정
# style: 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
# refactor: 코드 리팩토링
# test: 테스트 코드, 리팩토링 테스트 코드 추가
# chore: 빌드 업무 수정, 패키지 매니저 수정 등
# comment: 주석 추가 및 변경
# remove: 파일, 폴더 삭제
# rename: 파일, 폴더명 수정
###############################################
```

- 커밋 템플릿을 작성합니다.

### 3.3 .gitconfig에 추가 설정하기

Git의 설정을 변경하면 Git을 더 편리하게 사용할 수 있습니다. .gitconfig 파일에 추가 설정을 합니다.

```bash
vim ~/.gitconfig
```

- Git의 설정 파일을 엽니다.

```bash
#------- Default User Set --------
[user]
        name = ChangEuiKim
        email = cekim.dev@gmail.com
        initials = cekim
[http]
        sslVerify = true
[core]
        autocrlf = false
        ;   if true, git considers that 'CR' is added,
        ;   when 'CRLF' in working directory --> 'LF' in Repo
        ; safecrlf = true
        ;   when [autocrlf = false] git reject commit
        ;   - Commit: CRLF -> LF
        ;   - Checkout: LF -> CRLF
        ;   Consume there is only 'LF' in repository
        whitespace= fix,-indent-with-non-tab,trailing-space,cr-at-eol
        ; preloadindex = true [default]
        fscache = true
        editor = code --wait
#------- Colors --------
[color]
        ; ui = true [default]
        ; interactive = true [default]
[color "diff"]
        ; meta = blue white bold
#------- Merge Tool --------
[merge]
        tool = vscode
[mergetool "vimdiff"]
        trustExitCode = false
#------- Alias --------
[alias]
        co = checkout
        ci = commit
        st = status
        br = branch
        ; ? = diff
        l = !git graph | less -FXRS
        r = !git graph -20 | less -FXRS
        h = !git graph -1 | less -FXRS
        graph = log --graph --date-order -C -M --pretty=format:\"%C(blue)%h%C(reset) (%ar) [%an] %C(yellow)%d%Creset %s\" --all --date=short
        ls = log --graph -C -M --pretty=format:"%C(yellow)%h%Cgreen%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --all --date=short
        ll = log --pretty=format:"%C(yellow)%h%Cgreen%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --all --numstat
        ; standup = log --since yesterday --oneline --author <who@you-want-to-know.com>
#------- Additional --------
[init]
        defaultBranch = main
[commit]
        template = /home/dev/.gitmessage
```

#### 3.4.1 User, Http, Core

- `[user]`: 사용자 정보를 설정합니다.
- `[http]`: http 프로토콜을 사용할 때 ssl 검증을 사용합니다.
- `[core]`: Git의 기본 설정을 변경합니다.
- `;`는 주석을 의미합니다.
- autocrlf: 개행문자의 자동 변환을 false로 설정합니다.
  - CR은 Carriage Return의 약자로 줄바꿈 문자입니다.
  - CRLF는 Carriage Return Line Feed의 약자로 Windows에서 줄바꿈을 표현하는 문자입니다.
  - LF는 Line Feed의 약자로 Unix 계열에서 줄바꿈을 표현하는 문자입니다.
- whitespace: 공백문자를 검사하는 옵션을 설정합니다.
- fscache: 파일 시스템 캐시를 사용합니다. Git의 성능을 향상시킵니다.
- editor: Git이 텍스트 편집기로 VS Code를 사용합니다. `--wait` 옵션은 VS Code가 열려있는 동안 Git이 대기합니다.

#### 3.4.2 Merge, Alias

- `[merge]`: 병합 도구를 설정합니다.
- `[alias]`: 명령어의 별칭을 설정합니다.
- tool: 병합 도구로 VS Code를 사용합니다.
- trustExitCode: 병합 도구로 `vimdiff`를 사용할 때 종료 코드를 무시합니다. Vimdiff는 Vim의 비교 도구입니다.
- alias: 명령어의 별칭을 설정합니다.
  - `co`: git checkout
  - `ci`: git commit
  - `st`: git status
  - `br`: git branch
  - `l`: 커밋 그래프를 less 명령어와 함께 출력
  - `r`: 최근 20개의 커밋 그래프를 less 명령어와 함께 출력
  - `h`: 최근 1개의 커밋 그래프를 less 명령어와 함께 출력
  - `graph`: 커밋 로그를 그래프로 보여주는 별칭. 커밋 해시, 시간, 작성자, 브랜치, 태그 등을 색상으로 구분하여 표시
  - `ls`: graph와 비슷하지만 더 간단한 형식으로 커밋 로그를 표시
  - `ll`: 커밋 로그를 커밋 해시, 브랜치, 태그, 파일 변경 내역 등을 포함하여 표시

#### 3.4.3 Init, Commit

- `[init]`: Git 저장소를 초기화할 때 기본 브랜치를 main으로 설정합니다.
- `[commit]`: 커밋 템플릿을 설정합니다.

## 4 Visual Studio Code 설치하기

Visual Studio Code는 Microsoft에서 제공하는 오픈소스 코드 편집기입니다. Visual Studio Code를 사용하면 코드 작성, 디버깅, 버전 관리 등을 편리하게 할 수 있습니다.

> 참고: [Visual Studio Code](https://code.visualstudio.com/)의 공식 홈페이지에서 다운로드 받아 설치합니다.

### 4.1 확장 Extensions 설치하기

Visual Studio Code에서는 확장을 설치하여 기능을 확장할 수 있습니다. 확장을 설치하면 코드 작성, 디버깅, 버전 관리 등을 더 편리하게 사용할 수 있습니다.

#### 4.1.1 WSL2 관련 확장 설치하기

- WSL
- Remote - SSH
- Remote - SSH: Editing Configuration Files
- Remote - Tunnels
- Remote Explorer
- Remote Development
- Docker
- Dev Containers

#### 4.1.2 편의성 확장 설치하기

- Auto Close Tag
- Auto Rename Tag
- Auto Import
- Code Spell Checker
- Color Highlight
- ESLint
- IntelliCode
- IntelliCode API Usage Examples
- JavaScript and TypeScript Nightly
- Korean Language Pack for Visual Studio Code
- Markdown All in One
- Prettier - Code formatter

#### 4.1.3 웹 서버 확장 설치하기

- open in browser
- Live Server
- REST Client
