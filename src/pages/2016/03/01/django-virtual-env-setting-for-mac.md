---
title: '[django] 장고(django) 개발을 위한 파이썬(python) 가상환경 설정(Mac 환경)'
date: 2016-03-01 23:49:35
category: python
tags:
  - django
  - python
  - pyenv
  - virtualenv
---

가장 먼저 써야할 글을 이제서야 작성하네요.
여러 개발자들과 함께 장고(django)를 개발하기 위해서는 환경이 일치해야 합니다.
특히 python2 와 python3 는 서로 문법이 다르기 때문에(이에 대해서도 포스팅해야 겠네요) 개발 환경을 맞추는 것은 반드시 해야하는 작업입니다.

```
brew install pyenv
```

우선, pyenv 를 설치합니다. pyenv 는 로컬 환경에 여러 버전의 파이썬 버전을 설치 할 수 있도록 해줍니다.
기본적으로 설치되어 있는 파이썬 버전이 서로 다른 경우 개발에 제약이 생길 수 있기 때문에 파이썬 버전 의존성을 제거해주기 위해 반드시 pyenv 를 설치해 줍니다.

이제 실제 개발에 사용할 파이썬 버전을 설치해줍니다.

```
pyenv install 3.4.3  (python 3.4.3 버전 설치)
pyenv install --list  (설치 가능한 python 버전 list 보기)
```

파이썬 버전을 설치하고 나면 versions 명령어로 새 버전의 파이썬에 제대로 설치 되었나 확인해봅니다.

```
pyenv versions
   * system
     3.4.3    (새로 설치한 python)

pyenv shell 3.4.3    (3.4.3 버전 설정)
pyenv versions
     system
   * 3.4.3
```

위 화면처럼 나오면 정상입니다.
system 이란 현재 시스템에(Mac OS 에는 파이썬 2.7 버전이 기본적으로 설치되어 있습니다) 설치된 파이썬을 뜻합니다.
그리고 3.4.3 이 새롭게 설치된 파이썬 버전이겠지요.
별표는 현재 설정된 파이썬 버전을 뜻합니다. (현재는 system 버전이 설정되어 있네요)
그리고 아래 shell 명령어를 입력한다음 다시 versions 명령어를 입력하면 설정된 버전이 바뀐 것을 볼 수 있습니다.

좀 더 편한 작업을 위해 한가지 패키지를 더 설치해 줍니다.

```
brew install pyenv-virtualenv
```

pyenv-virtualenv 는 하나의 파이썬 버전에 여러개의 가상환경을 설정할 수 있도록 해주는 패키지입니다.
예를들어 파이썬 3.4.3 을 사용하는 django 프로젝트를 진행하는 동시에 다른 python 프로젝트를 진행하게 되었습니다.
이때 파이썬 버전을 동일하게 3.4.3 을 사용하게되면, django 에서만 사용하는 모듈을 다른 프로젝트에서도 불필요하게 설치되어 있게 됩니다.
이렇듯 잠재적인 문제를 야기하는 파이썬 모듈 의존성을 제거하기 위해 pyenv-virtualenv 패키지를 설치해줍니다.
아래와 같은 명령어를 통해서 하나의 파이썬 버전에 여러개의 가상환경을 설정할 수 있게 됩니다.

```
pyenv virtualenv <버전> <가상환경 이름>
pyenv virtualenv 3.4.3 py343
pyenv versions
     system
   * 3.4.3
     py343
```

virtualenv 라는 명령어가 추가되었습니다(그 외 activate 등 몇가지 추가).
첫번째 파라미터는 사용하는 버전을 뜻하고 두번째 파라미터는 가상환경의 이름을 뜻합니다.
다시 versions 명령어를 실행해보면, py343 이라는 새로운 가상환경이 만들어진것을 확인할 수 있습니다.

만들어진 가상환경을 사용할때 pyenv 의 명령어인 shell 을 사용해도 무방합니다만, 좀더 명시적으로 가상환경을 알 수 있도록 하기 위해서는 pyenv-virtualenv 패키지에서 제공하는 activate 명령어를 사용합니다.

```
pyenv activate py343
(py343) User-Macbook-Pro:~ user$

pyenv versions
     system
     3.4.3
   * py343
```

activate 명령어를 수행하게 되면, 쉘 커서 앞에 (py343)이라는 파이썬 가상환경 이름이 붙었네요.
versions 명령어를 수행해보면, py343 환경에 별표가 되어 있는걸 확인할 수 있습니다.
이제부터는 마음껏 모듈을 설치한 후에 다른 프로젝트를 진행할 일이 생기면, 다른 가상환경을 만들어서(예를들면 django343 등) 사용하시면 되겠습니다.

가상환경에서 빠져나올때는 deactivate 명령어를 사용하면 됩니다.

```
pyenv deactivate
```
