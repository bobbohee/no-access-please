---
layout: post
category: terminal
---

# 문제

postgresql 12 버전을 사용하다 11 버전을 사용하게 되었다. 
postgresql을 homebrew로 관리하고 있었기 때문에 12 버전을 중지시키고, 11 버전을 시작시켰다.

```bash
$ brew services stop postgresql@12
$ brew services start postgresql@11
```

psql 버전을 확인해보니 11 버전이 아닌 12 버전이 나왔다. 당황스러웠다.

```bash
$ psql -V 
psql (PostgreSQL) 12.5
```

# 해결 

> 9.6 패키지의 실행 파일을 사용하기 위해서는 홈브류의 link, unlink 기능을 사용해 패키지의 연결을 다시 해줄 필요가 있습니다. 현재는 10.4 패키지가 링크되어있는 상태이므로, 10.4 패키지를 언링크하고 9.6 패키지를 링크해줍니다. - 44bits

<br>

위 글과 같이 `link`, `unlink` 기능을 사용해 패키지의 연결을 다시해주어야 한다. 현재는 12 버전이 링크되어있는 상태로, 11 버전을 언링크하고 12 버전을 링크한다.

```bash
$ brew unlink postgresql@12
Unlinking /usr/local/Cellar/postgresql@12/12.5... 376 symlinks removed

$ brew link --force postgresql@11
parkbohee@bobbohees-MacBook-Pro no-access-please % brew link --force postgresql@11
Linking /usr/local/Cellar/postgresql@11/11.10... 455 symlinks created

If you need to have this software first in your PATH instead consider running:
  echo 'export PATH="/usr/local/opt/postgresql@11/bin:$PATH"' >> ~/.zshrc
```

<br>

다시 버전을 확인해보면 정상적으로 11 버전을 사용하고 있음을 알 수 있다.

```bash
$ psql -V 
psql (PostgreSQL) 11.10
```

# 참고

[https://formulae.brew.sh/formula/postgresql](https://formulae.brew.sh/formula/postgresql){:target="_blank"}

[https://www.44bits.io/ko/post/install-specific-version-package-homebrew](https://www.44bits.io/ko/post/install-specific-version-package-homebrew){:target="_blank"}