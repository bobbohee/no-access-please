---
layout: post
category: odoo
---

# 문제

`odoo 14` 버전을 `python 3.8.5` 버전을 사용해 개발한 프로젝트를 `ubuntu 18.04` 환경에 배포하려고 했더니, 서버에 설치된 파이썬 버전과 맞지 않았다.

odoo는 파이썬 버전에 민감하기 때문에, 서버에 `python 3.8.5` 버전을 설치하고자 했다.

# 해결

## dependencies 설치

```bash
sudo apt install build-essential checkinstall libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev openssl libffi-dev
sudo ldconfig
```

## 3.8.5 다운로드

```bash
mkdir -p $HOME/opt
cd $HOME/opt
curl -O https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tar.xz
tar -xf Python-3.8.5.tar.xz
```

## 3.8.5 설치

```bash
cd Python-3.8.5/
./configure --enable-shared --prefix=/usr/local LDFLAGS="-Wl,--rpath=/usr/local/lib" --enable-optimizations
sudo make altinstall
```

## 버전 확인

```bash
python3.8 -V
```

# 참고

[https://gist.github.com/dbinoj/7556daac1d214c98d1d84359045d5a49](https://gist.github.com/dbinoj/7556daac1d214c98d1d84359045d5a49){:target="_blank"}
