---
layout: post
title: "pyenv와 pipenv"
date: 2016-02-19
categories:
  - Python
description:
image: https://picsum.photos/2000/1200?image=1003
image-sm: https://picsum.photos/500/300?image=1003
---
### pyenv
***
여러 버전의 python을 쉽게 바꿔서 쓸 수 있게 하는 도구
<br />
<br />

### pipenv
***
pip와 virtualenv가 합쳐진 개념으로 python install package를 가상환경화 해주는 도구

Python.org에서 공식적으로 권장하는 패키지 설치 툴이다
<br />
<br />

### 왜 pyenv + pipenv 인가?
***
![enter image description here](/image/python_environment.png)

pyenv는 python 버전 관리를, pipenv는 프로젝트 의존성 관리를 도와준다.

<br />
<br />

### pyenv 설치

***


####brew로 pyenv 설치


`$ brew install pyenv`

####설치 할 수 있는 python 버전을 확인할 수 있다

`$ pyenv install --list`

####python 3.7.1을 설치

`$ pyenv install 3.7.1`

####pyenv는 global 인터프리터를 바꾸지 않는다

```
$ python --version 
Python 2.7.14

$ pyenv global 3.7.1
Python 3.7.1
```

####local 설정도 가능

```
$ pyenv install 3.7.0
$ mkdir my_project && cd my_project
$ python --version
Python 3.7.1

$ pyenv local 3.7.0
$ python --version
Python 3.7.0
```
<br />
<br />

### pipenv 설치
***

####brew로 pipenv 설치

`$ brew install pipenv`

####프로젝트에 pipenv 적용

```
$ cd my_project
$ pipenv install
Creating a virtualenv for this project…
Pipfile: /Users/dvf/my_project/Pipfile
Using /Users/dvf/.pyenv/versions/3.7.1/bin/python3.7 (3.7.1) to create virtualenv…

$ ls
Pipfile Pipfile.lock

```
> requirements.txt을 헤당 dir나 parent dir에서 찾을 수 있으면 그 내용이 Pipfile에 저장된다


####pip install 하는 것 처럼 pipenv install로 진행하면 된다

```
$ pipenv install django
Installing django
...

$ vim Pipfile

  1 [[source]]
  2 name = "pypi"
  3 url = "https://pypi.org/simple"
  4 verify_ssl = true
  5
  6 [dev-packages]
  7
  8 [packages]
  9 django = "*"
 10
 11 [requires]
 12 python_version = "3.7"
```

####Pipfile.lock 이란?
> 의존성 패키지의 version을 pin

```
 1 {
  2     "_meta": {
  3         "hash": {
  4             "sha256": ""
  5         },
  6         "pipfile-spec": 6,
  7         "requires": {
  8             "python_version": "3.7"
  9         },
 10         "sources": [
 11             {
 12                 "name": "pypi",
 13                 "url": "https://pypi.org/simple",
 14                 "verify_ssl": true
 15             }
 16         ]
 17     },
 18     "default": {
 19         "django": {
 20             "hashes": [
 21                 "sha256:",
 22                 "sha256:"
 23             ],
 24             "index": "pypi",
 25             "version": "==2.2.1"
 26         },
 27         "pytz": {
 28             "hashes": [
 29                 "sha256:",
 30                 "sha256:"
 31             ],
 32             "version": "==2019.1"
 33         },
 34         "sqlparse": {
 35             "hashes": [
 36                 "sha256:",
 37                 "sha256:"
 38             ],
 39             "version": "==0.3.0"
 40         }
 41     },
 42     "develop": {}
 43 }
```

####그 외

`$ pipenv check`  --> 의존성 미스 체크

`$ pipenv grapth` --> sub-의존성 조회