---
layout: post
category: git 
---

# 문제

git에서 repository를 clone 받을 때, 전체가 아닌 특정 폴더만 받고 싶은 경우가 있었다. 


# 해결

```bash
$ git init
$ git config core.sparseCheckout true
$ git remote add origin <REMOTE_URL>
$ echo <FOLDER_PATH> >> .git/info/sparse-checkout
$ git pull origin <BRANCH_NAME>
```

<br>

`odoo-ent14-kr` 레포지토리에 `config/addons/odoo.kr/ssk` 폴더만 clone 받고 싶은 경우, 아래와 같이 입력한다.

```bash
$ git init
$ git config core.sparseCheckout true
$ git remote add origin https://github.com/korjan20/odoo-ent14-kr.git
$ echo config/addons/odoo.kr/ssk >> .git/info/sparse-checkout
$ git pull origin develop
```

# 참고

[https://velog.io/@byjihye/git-clone](https://velog.io/@byjihye/git-clone){:target="_blank"}

[https://www.lesstif.com/gitbook/git-clone-20776761.html](https://www.lesstif.com/gitbook/git-clone-20776761.html){:target="_blank"}