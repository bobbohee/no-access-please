---
layout: post
category: react 
---


# 문제

`ubuntu 18.04` 서버에 리액트 프로젝트를 빌드하는데 아래와 같은 오류가 나면서 빌드가 중지되었다.

```bash
The build failed because the process exited too early. This probably means the system ran out of memory or someone called `kill -9` on the process.
```

# 원인

해당 에러는 서버 메모리가 부족해 발생하는 문제이다. 

# 해결

## sourcemap 제거

sourcemap은 빌드 시 생성되며, 디버깅을 위한 파일이다. 
잘못된 문제가 생겼을 때, 디버깅을 위해 필요한 파일이지만 해당 프로젝트는 이전 프로젝트로 리팩토링된 프로젝트와 비교를 하기 위해 잠시 배포되었기 떄문에 sourcemap이 크게 필요없다고 판단되어 sourcemap을 생성하지 않도록 했다. 

<br>

`GENERATE_SOURCEMAP=false` 설정을 통해 프로젝트 빌드 후, sourcemap을 삭제하도록 한다.

```json
"build": "GENERATE_SOURCEMAP=false react-scripts build"
```

<br>

`GENERATE_SOURCEMAP`은 `react-scripts 1.0.11` 버전부터 동작하기 때문에 1.0.11 버전 이하라면 아래처렁 사용하도록 한다.

```json
"build": "react-scripts build && rm build/static/**/*.map"
```

## 그 외

👉 [react-scripts 메모리 설정하기](https://lahuman.github.io/react_build_heap_momory/){:target="_blank"}

👉 [Code Splitting, Analyze](https://medium.com/@yerikim/%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%B6%80%EC%A1%B1%EC%9C%BC%EB%A1%9C-%EC%9D%B8%ED%95%9C-cra-build-fail-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0-acdfdb4f8c49){:target="_blank"}

# 참고한 사이트

[https://medium.com/@yerikim/메모리-부족으로-인한-cra-build-fail-해결하기-acdfdb4f8c49](https://medium.com/@yerikim/%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%B6%80%EC%A1%B1%EC%9C%BC%EB%A1%9C-%EC%9D%B8%ED%95%9C-cra-build-fail-%ED%95%B4%EA%B2%B0%ED%95%98%EA%B8%B0-acdfdb4f8c49){:target="_blank"}

[https://velog.io/@racoon/React-build-시-sourcemap-제거하기](https://velog.io/@racoon/React-build-%EC%8B%9C-sourcemap-%EC%A0%9C%EA%B1%B0%ED%95%98%EA%B8%B0){:target="_blank"}