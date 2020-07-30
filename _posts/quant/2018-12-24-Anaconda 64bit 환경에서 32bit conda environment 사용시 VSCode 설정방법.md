---
layout: post
title: Anaconda 64bit 환경에서 32bit conda environment 사용시 VSCode 설정방법
tags: ["anaconda", "vscode"]
---

### 환경
* OS : Windows10 64bit
* Anaconda 5.2 64bit
* IDE : Visual Studio Code


### 문제점

* 증권사 API를 사용하려면 32bit python 환경을 사용해야 하므로 zipline도 32bit conda environment에 설치
* 디버깅을 위해 내부터미털 구동시 conda environment activation은 되는데 set CONDA_FORCE_32BIT=1 설정이 안됨


### 해결방법

1. bat파일 생성

  * {프로젝트디렉토리}/.vscode/vscode.bat 으로 생성함(위치, 파일명 제한없음)
    > set CONDA_FORCE_32BIT=1

2. User 또는 Workspace setting 추가

  * {프로젝트디렉토리}/.vscode/settings.json
  {tab}zipline을 쓰는 프로젝트에만 반영시킬 것이라 Workspace setting에 추가함
    > "terminal.integrated.shellArgs.windows": ["/K", "C:\\...\\vscode.bat"]

3. 결과확인
  * VS Code에서 디버깅 실행시 conda 가상환경이 activate되기 전에 set CONDA_FORCE_32BIT=1 명령어가 수행됨


### 참고사이트

* [How to setup custom terminal in Visual Studio Code – QJ Li – Medium](https://medium.com/@qjli/how-to-setup-custom-terminal-in-visual-studio-code-e0a4be28130e)
