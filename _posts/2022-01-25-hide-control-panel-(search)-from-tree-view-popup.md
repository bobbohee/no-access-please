---
layout: post
category: odoo
---

# 문제

tree 뷰 팝업에서  Control Panel(1)과 Action Button(2)을 제거하고 싶었다.

![tree 뷰 팝업](/no-access-please/assets/image/2022-01-25-hide-control-panel-(search)-from-tree-view-popup/1.png)

# 해결

팝업을 띄우는 코드에서 flags에 `withControlPanel`과 `action_buttons`를 False로 설정하면 된다.

```python
'flags': {
    'withControlPanel': False,  # 1
    'action_buttons': False,     # 2
}
```

<br>

없어졌다!

![tree 뷰 팝업에 Control Panel 제거](/no-access-please/assets/image/2022-01-25-hide-control-panel-(search)-from-tree-view-popup/2.png)
