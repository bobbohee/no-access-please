---
layout: post
category: mac 
---

# 문제

맥(Mac)은 기본적으로 스크린샷이 데스크탑 위치에 저장되는데, 스크린샷이 많아질 경우 바탕화면이 더러워지게 되고, 관리가 힘들어진다.

그래서 스크린샷을 저장할 다른 폴더를 지정하기로 했다.

# 해결

## 폴더 지정

스크린샷을 저장할 폴더를 지정한다.

```bash
defaults write com.apple.screencapture location {폴더 위치}
```

```bash
defaults write com.apple.screencapture location ~/Downloads/screenshot/
```

## 변경사항 반영

```bash
killall SystemUIServer
```