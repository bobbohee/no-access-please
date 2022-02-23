---
layout: post
category: python
---

# 문제

사용자가 메뉴를 클릭할 때마다, TIPA(중소기업기술정보진흥원) API에 모니터링을 위한 정보를 전송해야 했다.

메뉴 클릭 시, 아래와 같은 형식으로 로드할 페이지에 대한 정보를 넘기고 있었다. 그래서 해당 데이터에서 필요한 정보만 구분해 사용했다.

```python
{'action': 292, 'model': 'sale.order', 'view_type': 'list', 'cids': 1, 'menu_id': 176}
```

하지만, 예외적으로 홈 메뉴를 클릭했을 때 다른 형식으로 데이터가 넘어오는 경우가 있어, 예외 처리가 필요했다.

```python
{'cids': 1, 'home': ''}
```

객체(dict)에서 `home`이라는 key를 가지고 있는 경우와 `action`, `menu_id`, `view_type` 모두 key를 가지고 있는 경우로 예외 처리를 했는데,
키가 여러 개인 경우, 어떻게 검사를 해야 하나 고민했다.

# 해결

```python
def do_act_window(self, vals):
    if 'home' in vals:
        return self.monitor_menu({
            'upperMenuNm': '홈',
            'menuNm': '홈',
            'actionNm': 'module',
        })
    if all(k in vals for k in ('menu_id', 'action', 'view_type')):
        return self.monitor_menu({
            'upperMenuNm': self.env['ir.ui.menu'].browse(vals.get('menu_id')).name,
            'menuNm': self.name,
            'actionNm': vals.get('view_type'),
        })
```

# 참고

[https://stackoverflow.com/questions/1285911/how-do-i-check-that-multiple-keys-are-in-a-dict-in-a-single-pass](https://stackoverflow.com/questions/1285911/how-do-i-check-that-multiple-keys-are-in-a-dict-in-a-single-pass){:target="_blank"}