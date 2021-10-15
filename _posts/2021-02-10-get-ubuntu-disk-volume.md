---
layout: post
category: terminal
---

# 문제

잘 작동하던 Odoo 테스트 서버가 죽어서 서버를 다시 start 하기 위해 서버 환경에 접속했다. 

아래와 같은 메시지가 나타났다. 대수롭게 생각하지 않고 넘어갔다. 

```shell
E297: Write error in swap file
```

서버를 restart 했다. 하지만 restart 했음에도 불구하고, 서버가 바로 죽어버렸다. 

# 원인

postgresql 설정을 잘못했는데 그로 인해 오류 로그 파일과 기타 알 수 없는 문제로 디스크 용량이 100%가 되었다. 

잘못된 postgresql 설정을 수정한 뒤에도 사용 가능한 디스크 용량이 없어 서버가 계속해서 죽었다.

👉 [postgresql 5432 에러 해결 방법](https://stackoverflow.com/questions/42653690/psql-could-not-connect-to-server-no-such-file-or-directory-5432-error){:target="_blank"}

# 해결

## 디스크 용량 확보

### 커널 로그 삭제

`/var/log`에 각종 log 파일들이 저장되는데 필요하지 않는 로그 파일들은 파일만 남기고 내용은 삭제한다.

```shell
cat /dev/null > /var/log/{log 파일명}
```

실수로 log 파일을 전부 삭제했는데 디스크 용량이 `100% → 91%`로 감소했다. 

### 커널 파일 삭제

오래된 커널 파일은 삭제해도 되기 때문에 삭제한다. 

커널 파일을 삭제하니 

- `apt autoremove` 사용하지 않는 패키지 삭제
- `--purge` 사용하지 않는 패키지의 설정 파일 삭제

```shell
sudo apt autoremove --purge
```

커널 파일을 삭제하니 `91% → 77%`로 감소했다. 

### 캐쉬 삭제

```shell
sudo apt-get clean
```

## Odoo log 기준 설정

packt을 참고해 `.odoorc` 파일에서 log 파일 작성 기준을 설정했다.

```text
logrotate = True
log_level = warn
log_handler = :WARNING,werkzeug:CRITICAL,odoo.service.server:INFO
```

👉 [Odoo log 옵션](https://gist.github.com/Guidoom/d5db0a76ce669b139271a528a8a2a27f){:target="_blank"}

# 참고 사이트

[https://falsy.me/ubuntu-용량이-부족할때-큰-용량의-파일-찾기와-오래된-커/](https://falsy.me/ubuntu-%EC%9A%A9%EB%9F%89%EC%9D%B4-%EB%B6%80%EC%A1%B1%ED%95%A0%EB%95%8C-%ED%81%B0-%EC%9A%A9%EB%9F%89%EC%9D%98-%ED%8C%8C%EC%9D%BC-%EC%B0%BE%EA%B8%B0%EC%99%80-%EC%98%A4%EB%9E%98%EB%90%9C-%EC%BB%A4/){:target="_blank"}

[https://m.blog.naver.com/PostView.nhn?blogId=and_lamyland&logNo=221278669952&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=and_lamyland&logNo=221278669952&proxyReferer=https:%2F%2Fwww.google.com%2F){:target="_blank"}

[https://jjudrgn.tistory.com/28](https://jjudrgn.tistory.com/28){:target="_blank"}
