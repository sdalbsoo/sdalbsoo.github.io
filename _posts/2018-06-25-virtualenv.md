---
layout: post
title:  "Virtualenv 사용하기 "
date:   2018-06-25 10:00:00 +0900
categories: python
---

- 가상환경을 쓰는 이유?
	- 프로젝트별로 파이썬 환경을 독립 운영하기 위해서 사용

## 관련 명령어

1. 가상환경을 만들어야 한다.
	- `$ mkvirtualenv —python=python3.6 <name>`
2. 가상환경 이름 목록을 보고 싶다.
	- `$ lsvirtualenv`
3. 가상환경 위에서 파이썬을 쓰고 싶다.
	- `$ ipython (Read Eval Print Loop) or $ python (ipython같은 경우 자동완성 시스템이 구축되어있음)`
4. REPL을 나가고 싶다.
	- `<CTRL> + D`
5. 가상환경을 끈다.
	- `$ deactivate`
6. 가상환경을 지우고 싶다.
	- `$ rmvirtualenv <name>`
7. 가상환경을 만든 뒤 ipython을 사용하고 싶다.
	- `$ pip install ipython 사용하여 ipython을 다운받는다.`

[virutalenvwrapper 공식문서](http://virtualenvwrapper.readthedocs.io/en/latest/)
