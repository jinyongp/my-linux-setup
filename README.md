# My Linux Setup <!-- omit in toc -->

제가 리눅스를 설치하는 과정을 정리해보았습니다. 저의 취향이 변함에 따라 내용은 계속 수정될 수 있습니다.

과정만 참고하시고 자신의 리눅스를 마음껏 커스터마이징해보세요.

주의하세요. 한번 시작하면 도중에 그만두기 힘듭니다!

>잘못된 내용 혹은 추가할 내용이 있다면 Issue 혹은 Pull Request를 올려주세요.

## Introduce My Linux <!-- omit in toc -->

- OS: Ubuntu 20.04.01 LTS Focal Fossa
- Shell: Zsh
- Terminal: HyperTerm

## Table of Contents <!-- omit in toc -->

- [Ubuntu 설치 - 멀티부팅: Windows 10 & Ubuntu](#ubuntu-설치---멀티부팅-windows-10--ubuntu)
  - [Disk 볼륨 분할](#disk-볼륨-분할)
  - [Windows 10에서 빠른 시작 끄기](#windows-10에서-빠른-시작-끄기)
  - [Ubuntu 설치용 USB 만들기](#ubuntu-설치용-usb-만들기)
  - [Bios 설정](#bios-설정)
  - [Ubuntu 설치](#ubuntu-설치)
- [우분투 세팅](#우분투-세팅)
  - [한국어 입력](#한국어-입력)
  - [apt 미러 서버 변경](#apt-미러-서버-변경)
  - [설치 프로그램](#설치-프로그램)
  - [테마](#테마)
- [터미널](#터미널)
  - [HyperTerm](#hyperterm)
  - [zsh, Oh My Zsh](#zsh-oh-my-zsh)
  - [vim, VundleVim](#vim-vundlevim)
- [개발환경](#개발환경)
  - [Editor: vscode](#editor-vscode)
    - [Extensions](#extensions)
  - [Node.js](#nodejs)
  - [Deno](#deno)
  - [Python](#python)
    - [Anaconda](#anaconda)

---

## Ubuntu 설치 - 멀티부팅: Windows 10 & Ubuntu

현재 Windows 10과 Ubuntu 20.04를 멀티부팅으로 같이 사용 중이다.

### Disk 볼륨 분할

현재, Windows에서 SSD를 C 드라이브로, HDD를 D 드라이브로 사용하고 있다.

D 드라이브를 분할하여, 우분투 설치 공간을 만들었다.

1. Windows에서 `Win + R` 단축키로 `실행`을 연 뒤, `diskmgmt.msc`를 입력하여 `디스크 관리`를 연다.
2. D 드라이브 볼륨을 우클릭하여 연 뒤, 볼륨 축소를 클릭한다.
3. `축소할 공간 입력`란에 우분투를 설치할 공간을 `MB` 단위로 입력하고 `축소` 버튼을 클릭한다.
4. `할당되지 않음` 공간이 만들어진다면 디스크가 성공적으로 분할된 것이다.

### Windows 10에서 빠른 시작 끄기

UEFI 펌웨어라면 windows의 `빠른 시작 옵션`을 해제해야 한다.

1. 제어판에서 전원 옵션에 진입한다.
2. 좌측의 `절전 모드 해제 시 암호 사용` 혹은 `전원 단추 작동 설정`을 클릭한다.
3. `현재 사용할 수 없는 설정 변경`을 클릭하여 추가 설정을 연 뒤, `빠른 시작 켜기(권장)` 체크를 해제한다.

### Ubuntu 설치용 USB 만들기

아래 페이지에 접속하여 Ubuntu desktop image 파일과 rufus를 설치한다.

>[Download Ubuntu 20.04.1 LTS (Focal Fossa)](https://releases.ubuntu.com/20.04/)
>[Download Rufus](https://rufus.ie/)

1. 용량이 4GB 이상인 USB를 연결한다. 포맷해야 하므로 필요할 경우, 내용물은 백업해야 한다.
2. 설치한 rufus를 실행한다.
   1. 장치로 방금 연결한 USB를 선택한다.
   2. `선택`을 클릭해서 위에서 설치한 desktop image 파일(.iso)을 선택한다.
   3. UEFI 시스템이므로 `GPT` 파티션 방식을 선택한다.
   4. 아래 설정은 건드리지 않고 `시작`을 클릭한다.
   5. 추가로 나오는 창은 `확인` 버튼을 클릭하여 계속한다.
   6. `상태`가 완료가 되면 설치가 완료된 것이다.
3. Rufus를 종료한다.

### Bios 설정

1. Ubuntu 설치용 USB를 연결한 상태로 windows를 `다시 시작`한다.
2. 처음 로딩 화면이 나오면, `F2`를 눌러 bios에 진입한다.(제조사마다 다르다.)
3. Boot 우선 순서를 USB가 1순위가 되도록 변경한다.(없다면 UEFI 시스템이 아닐 수 있다.)
4. UEFI 펌웨어일 경우, 설정에서 `Secure Boot` 옵션을 찾고 이를 비활성화해야 한다.
5. 세팅을 저장하고 다시 시작하면 USB 메모리로 부팅된다.
6. GRUB 창에서 `Install Ubuntu (Safe Graphics)`를 선택한다.
7. Ubuntu 설치 창이 뜰 때까지 대기한다.

### Ubuntu 설치

1. `한국어`를 선택하고 `Ubuntu 설치` 버튼을 클릭한다.
2. 한글 키보드 레이아웃을 선택하고 계속한다.
3. 무선 wi-fi일 경우 인터넷이 필요하므로 연결해야 한다.
4. 일반 설치에서 추가 소프트웨어를 설치하는 옵션을 활성화하고 계속한다.
5. 설치 형식에서 파티션을 나누기 위해 `기타` 옵션을 선택하고 계속한다.
6. D 드라이브에서 분할된 파티션에 보일 것이다. 남은 공간을 클릭하고 `+` 버튼을 클릭하여 파티션을 생성한다.
7. UEFI에서의 부트로더 설치를 위해, 크기에 500 MB를 할당하고 용도를 `EFI 시스템 파티션`으로 설정한다. 주 파티션으로 한다.
8. 남은 공간을 전부 선택하여, 논리 파티션으로 `EXT4 저널링 파일 시스템` 용도의 `/` 위치로 하여 파티션을 생성한다.
9. 원할 경우, `/home`을 위한 별도의 파티션을 분리해도 된다.
10. `부트로더를 설치할 장치`는 위에서 할당한 `EFI 시스템 파티션`을 선택한다.
11. 지금 설치를 클릭하여 설치를 계속한다.
12. Seoul을 선택하고 나머지 정보를 입력하여 설치를 계속한다. `자동으로 로그인` 옵션을 활성화했다.
13. 설치가 완료되면 `지금 다시 시작` 버튼을 클릭하고, 안내에 따라 USB를 제거한다.

---

## 우분투 세팅

### 한국어 입력

### apt 미러 서버 변경

### 설치 프로그램

### 테마

---

## 터미널

### HyperTerm

### zsh, Oh My Zsh

### vim, VundleVim

---

## 개발환경

### Editor: vscode

#### Extensions

### Node.js

### Deno

### Python

#### Anaconda

---
