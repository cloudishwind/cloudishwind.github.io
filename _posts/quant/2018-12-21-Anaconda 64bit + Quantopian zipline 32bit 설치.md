---
layout: post
title: Anaconda 64bit + Quantopian zipline 32bit 설치
tags: ["anaconda", "python", "zipline"]
---

### 시스템 환경
* OS : Windows10 64bit


### 1) 아나콘다3 64bit 설치

Python 3.6버전으로 다운받기 위해 5.2버전을 다운받음

* [Downloads - Anaconda](ttps://www.anaconda.com/download/)
* [Anaconda installer archive](https://repo.anaconda.com/archive/)


### 2) Visual Studio Build Tools 설치(zipline 설치 필요조건)

아래 경로에서 "Visual Studio Build Tools 2015" 다운로드
(python 3.5가 아닌경우 설치에 필요한 Build Tools 버전이 다를 수 있음)

* [visualstudio](https://visualstudio.microsoft.com/ko/vs/older-downloads/)


### 3) 32bit Python conda 가상환경 생성 및 zipline 설치

관리자권한 Console 실행후 아래 명령어 실행

1. set CONDA_FORCE_32BIT=1
2. conda create --n {가상환경명} python=3.5
3. activate {가상환경명}
4. pip install zipline
5. pip uninstall bottleneck
6. pip install --upgrade numpy
7. deactivate
8. set CONDA_FORCE_32BIT=

- 32bit 환경에서 conda install zipline 시 python 버전이 2.7로 내려가게 되어, pip install 을 사용함
- (4)까지 진행하고 import zipline 하게되면 AttributeError: module 'bottleneck' has no attribute 'nanmean' 오류가 발생하는데 (5),(6)을 수행하면 오류가 사라짐
- (7),(8)은 설치와는 무관

### 참고사이트
* <http://www.zipline.io>
