---
layout: post
category: etc 
---

# 문제

AWS EC2 서버에 접속하려 했을 때 아래와 같이 오류가 발생했다.

```bash
$ ssh -i my_key.pem ec2-user@11.22.33.44
ssh_exchange_identification: read: Connection reset by peer
```

# 해결

인터넷에 해당 문제를 검색했을 때 마땅한 해결 방법은 없었다. 

그래서 터미널 종료 후, 재시작한 후 다시 시도해니 정상적으로 접속되었다... ✌️

# 참고

[https://www.facebook.com/groups/awskrug/permalink/734671313301562](https://www.facebook.com/groups/awskrug/permalink/734671313301562/){:target="_blank"}