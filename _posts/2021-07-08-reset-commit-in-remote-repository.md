---
layout: post
category: git 
---

시간이 없어서 해당 문제를 겪고 3일 뒤에 글을 쓰려니 기억이 나질 않는다... 이래서 시간이 없더라도 간단하게 작성해놔야하는데 😂

깃에 올라가면 안되는 파일이 올라갔는데 그걸 브랜치에 push 한 뒤, 알아채버렸다. 한가지 다행인 사실은 메인 브랜치는 아니고, 특정 기능 개발 브랜치였다.

# 방법

커밋을 취소하기 방법은 `revert`와 `reset`이 있다. 
간단히 설명해 `revert`는 커밋을 취소한 기록이 남고, `reset`은 커밋을 취소한 기록이 남지 않는다. 

그 중 나는 `reset`을 사용했다. 

## 돌아갈 이력 확인

`git reflog` 명령어를 통해 돌아갈 이력을 확인한다. 만약 내가 잘못한 커밋이 ID가 `d6cd12c`라면, 돌아갈 이력은 `18b4857`이다.

```bash
$ git reflog
ca0f23b (HEAD -> master, origin/master) HEAD@{0}: commit: [ADD] 조건을 사용해 tree 뷰에 column 숨기기
d6cd12c HEAD@{1}: commit: [ADD] 커스텀 모듈 설치 시, 기존 모듈 번역의 수정 사항 적용하기
18b4857 HEAD@{2}: commit: [ADD] 특정 그룹만 수정이 가능하도록 view 설정 (editable)
4e39129 HEAD@{3}: commit: [ADD] %()d 형식의 name을 가진 버튼 가져오기
b425342 HEAD@{4}: commit: [ADD] Odoo 카테고리 페이지 추가
6b4ffcf HEAD@{5}: commit: [ADD] 파이썬 list에 여러 값 append 하기
```

## reset으로 되돌리기

`git reset` 명령어를 이용해 되돌리고 싶은 커밋으로 되돌린다.

```bash
git reset --soft 18b4857
```

<br>

현재는 로컬에서만 되돌아간 상태이므로, 원격에 반영하고 싶다면 아래 명령어를 사용한다. 

⚠️ 원격에서까지 커밋 기록을 지우면, 복구할 수 없으므로 신중하게 사용해야한다.

```bash
git push --force origin master
```

<br>

push까지 했을 때는 지금처럼 `reset`을 사용하기 보다는 `revert`를 사용해야한다.
(개인 프로젝트가 아닌 팀프로젝트에서는 더더욱!)

다음부터는 꼭 `revert`를 사용해 기록을 남기도록 하자!

# 참고

[https://jupiny.com/2019/03/19/revert-commits-in-remote-repository](https://jupiny.com/2019/03/19/revert-commits-in-remote-repository){:target="_blank"}