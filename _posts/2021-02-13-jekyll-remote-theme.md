---
layout: post
category: jekyll 
---

# 문제

현재 이 jekyll 블로그 코드를 수정하거나 포스트를 작성해 커밋을 하고, 푸쉬를 하면 아래와 같은 경고 메일이 날라왔다.

```text
The page build completed successfully, but returned the following warning for the `master` branch:

You are attempting to use a Jekyll theme, "no-style-please", which is not supported by GitHub Pages. Please visit https://pages.github.com/themes/ for a list of supported themes. If you are using the "theme" configuration variable for something other than a Jekyll theme, we recommend you rename this variable throughout your site. For more information, see https://docs.github.com/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll.

For information on troubleshooting Jekyll see:

 https://docs.github.com/articles/troubleshooting-jekyll-builds

If you have any questions you can submit a request at https://support.github.com/contact?repo_id=336736482&page_build_id=233332373
```

큰 문제까지는 아니지만 푸쉬했을 때마다 메일이 와서 스트레스였다. 

# 원인

현재 이 jekyll 블로그는 [no-style-please](https://github.com/riggraz/no-style-please) 테마를 사용하고 있는데 이 테마가 github에서 지원하는 정식 테마가 아니기 때문에 경고 메일이 날라온 것 같다. 

👉 [github에서 지원하는 테마보기](https://pages.github.com/themes/)

# 해결

`_config.yml` 파일에 `remote_theme`에 사용하고 있는 테마의 저장소를 추가하면 된다.

```yaml
remote_theme: riggraz/no-style-please
```

# 참고 사이트

[https://dreamgonfly.github.io/blog/jekyll-remote-theme](https://dreamgonfly.github.io/blog/jekyll-remote-theme)
