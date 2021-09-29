---
layout: post
category: odoo
---

# 문제

서버를 실행하기 전에 업데이트를 실행할 모듈을 `-u` 또는 `--update` 옵션을 사용해 지정할 수 있다.

```bash
python odoo-bin --config=./config/.odoorc_local -u module_name
```

<br>

업데이트를 실행할 모듈이 여러 개일 경우, 아래와 같이 사용했었다.

아래와 같이 작성한 건 틀린 방법인데, 약 1년 동안 아무 문제없이 잘 사용해왔다. 🤔?

```bash
python odoo-bin --config=./config/.odoorc_local -u module_A -u module_B -u module_C
```

# 해결

압데이트를 실행할 모듈이 여러 개일 경우 `,`(콤마)로 구분해 작성한다. 

⚠️ 띄어쓰기 없이 작성해야 한다.

<br>

**올바른 방법 (O)**

```bash
python odoo-bin --config=./config/.odoorc_local -u module_A,module_B,module_C
```

옵션이 잘 지정되었을 경우, 아래 log처럼 update_list에 모듈 이름이 나타나야 한다.

```text
2021-09-16 07:34:35,358 64889 INFO ent14_ssk_0818 odoo.addons.base.models.ir_module: ALLOW access to module.button_upgrade on ['module_A', 'module_B', 'module_C'] to user __system__ #1 via n/a 
2021-09-16 07:34:35,358 64889 INFO ent14_ssk_0818 odoo.addons.base.models.ir_module: ALLOW access to module.update_list on ['module_A', 'module_B', 'module_C'] to user __system__ #1 via n/a 
```

<br>

**잘못된 방법 (X)**

```bash
python odoo-bin --config=./config/.odoorc_local -u module_A, module_B, module_C
```

잘못된 파라미터라는 오류가 나타난다.

```text
Usage: odoo-bin [options]

odoo-bin: error: unrecognized parameters: 'module_A, module_B, module_C'
```

## TMI

모듈 업데이트가 안됐을 경우, db_name을 지정했는지 확인해본다.

# 참고

[https://www.odoo.com/documentation/14.0/developer/misc/other/cmdline.html?highlight=command%20line#cmdoption-odoo-bin-u](https://www.odoo.com/documentation/14.0/developer/misc/other/cmdline.html?highlight=command%20line#cmdoption-odoo-bin-u){:target="_blank"}

[https://www.odoo.com/ko_KR/forum/doummal-1/how-to-upgrade-multiple-modules-from-command-line-with-a-single-run-179742](https://www.odoo.com/ko_KR/forum/doummal-1/how-to-upgrade-multiple-modules-from-command-line-with-a-single-run-179742){:target="_blank"}
