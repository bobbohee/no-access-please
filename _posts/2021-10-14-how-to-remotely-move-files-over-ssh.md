---
layout: post
category: terminal
---

# 문제

커스텀 모듈에 소수점을 없애는 기능을 추가해 다른 기업에서 체험용으로 사용 중인 서버에 커스텀 모듈을 설치해 확인해야 했다.
체험용 서버이기 때문에 기본만 세팅한 상태라 git도 연동되어 있지 않았다.

원래는 git을 사용해 로컬에서 개발한 코드를 서버에서 받았는데, git을 사용하고 있지 않아 다른 방법을 찾아보기로 했다.

# 해결

터미널에서 `scp` 명령어를 통해 서버로 파일을 전송할 수 있었다.

```bash
$ scp [옵션] [keypair 파일 path] [전송할 파일 path] [원격지 ID]@[원격지_IP]:[위치]
```

```bash
$ scp -i keypair_odoo_ssk.pem ~/Downloads/tilon.zip bitnami@ec2-3-37-40-91.ap-northeast-2.compute.amazonaws.com:~
tilon.zip                                                                                                      100% 6043     1.1MB/s   00:00
```

# 참고

[https://eehoeskrap.tistory.com/543](https://eehoeskrap.tistory.com/543){:target="_blank"}