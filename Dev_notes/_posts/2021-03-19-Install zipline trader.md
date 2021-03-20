---
layout: post
title: Zipline trader 설치하기
tags: ["zipline", "python"]
---

설치환경
> Windows 10 64 bits   
> Anaconda

설치순서

* set CONDA_FORCE_32BIT=1
* conda create -n py36_32 python=3.6
* activate py36_32
* conda info
* pip install --upgrade pip
* pip install --upgrade setuptools
* deactivate

* git clone https://github.com/shlomikushchi/zipline-trader.git
* activate py36_32
* pip install -e .

* pip uninstall jedi
