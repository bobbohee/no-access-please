---
layout: post
category: odoo
---

# 문제

작업지시서에서 투입하려는 또는 투입된 부품에 대한 공정 정보를 확인할 수 있는 버튼을 만들었다.

버튼 클릭 시, 팝업으로 부품에 대한 공정 정보가 나타났는데 문제는 새로 생성이 되거나, 수정, 삭제가 가능하다는 것이었다.
조회만 가능하게 readonly로 설정하고자 했다.

```python
return {
    'type': 'ir.actions.act_window',
    'res_model': 'lotsheet.lotsheet',
    'res_id': prev_routing.id_lotsheet.id,
    'views': [[self.env.ref('mrp_ssk.%s' % lotsheet['view']).id, 'form']],
    'name': _('%s Lot Sheet', lotsheet['title']),
    'target': 'new',
}
```

# 해결

아래와 같이 `flags`를 추가하면, form 뷰 팝업이 readonly로 설정되어 새로 생성이 되거나, 수정, 삭제되지 않는다.

```python
'flags': {'mode': 'readonly'}
```

# 참고

[https://www.odoo.com/forum/help-1/open-form-view-in-popup-in-readonly-mode-v10-177910](https://www.odoo.com/forum/help-1/open-form-view-in-popup-in-readonly-mode-v10-177910){:target="_blank"}

