---
layout: post
category: django
---

# 문제

gunicorn 서비스를 실행시키니 `ModuleNotFoundError: No module named 'django'` 에러가 발생했다.

서비스로 실행하지 않고 명령으로 실행시킨 경우에는 정상적으로 실행되었는데, 서비스 파일을 생성해 실행시키니 에러가 발생해서 당황스러웠다.

```
$ sudo systemctl daemon-reload
$ sudo systemctl restart gunicorn
$ sudo systemctl status gunicorn
● gunicorn.service - gunicorn daemon
     Loaded: loaded (/etc/systemd/system/gunicorn.service; disabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Mon 2022-02-21 02:19:04 UTC; 5s ago
    Process: 34864 ExecStart=/usr/local/bin/gunicorn --bind 127.0.0.1:8000 config.wsgi:application (code=exited, status=3)
   Main PID: 34864 (code=exited, status=3)

Feb 21 02:19:04 hw-esg gunicorn[34866]:   File "<frozen importlib._bootstrap_external>", line 848, in exec_module
Feb 21 02:19:04 hw-esg gunicorn[34866]:   File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
Feb 21 02:19:04 hw-esg gunicorn[34866]:   File "/home/parkbohee0705/hw_esg/backend/config/wsgi.py", line 12, in <module>
Feb 21 02:19:04 hw-esg gunicorn[34866]:     from django.core.wsgi import get_wsgi_application
Feb 21 02:19:04 hw-esg gunicorn[34866]: ModuleNotFoundError: No module named 'django'
Feb 21 02:19:04 hw-esg gunicorn[34866]: [2022-02-21 02:19:04 +0000] [34866] [INFO] Worker exiting (pid: 34866)
Feb 21 02:19:04 hw-esg gunicorn[34864]: [2022-02-21 02:19:04 +0000] [34864] [INFO] Shutting down: Master
Feb 21 02:19:04 hw-esg gunicorn[34864]: [2022-02-21 02:19:04 +0000] [34864] [INFO] Reason: Worker failed to boot.
Feb 21 02:19:04 hw-esg systemd[1]: gunicorn.service: Main process exited, code=exited, status=3/NOTIMPLEMENTED
Feb 21 02:19:04 hw-esg systemd[1]: gunicorn.service: Failed with result 'exit-code'.
```

<br>

**gunicorn.service**

```
[Unit]
Description=gunicorn daemon
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/home/parkbohee0705/hw_esg/backend
ExecStart=/usr/local/bin/gunicorn --bind 127.0.0.1:8000 config.wsgi:application

[Install]
WantedBy=multi-user.target
```

# 해결

파이썬 패키지를 읽어오지 못하는 문제같아 `django` 패키지가 설치된 위치를 확인해 `django` 패키지의 소유자와 그룹을 확인해보니 `parkbohee0705`로 나타났다.

```
$ pip show django
Name: Django
Version: 3.2
Summary: A high-level Python Web framework that encourages rapid development and clean, pragmatic design.
Home-page: https://www.djangoproject.com/
Author: Django Software Foundation
Author-email: foundation@djangoproject.com
License: BSD-3-Clause
Location: /home/parkbohee0705/.local/lib/python3.8/site-packages
Requires: asgiref, pytz, sqlparse
Required-by: django-import-export, django-seed, djangorestframework, drf-yasg


$ ls -la ~/.local/lib/python3.8/site-packages/ | grep django
drwxrwxr-x 19 parkbohee0705 parkbohee0705    4096 Feb 16 06:20 django
drwxrwxr-x  2 parkbohee0705 parkbohee0705    4096 Feb 16 06:20 django_import_export-2.7.1.dist-info
drwxrwxr-x  4 parkbohee0705 parkbohee0705    4096 Feb 16 06:20 django_seed
drwxrwxr-x  2 parkbohee0705 parkbohee0705    4096 Feb 16 06:20 django_seed-0.3.1.dist-info
drwxrwxr-x  2 parkbohee0705 parkbohee0705    4096 Feb 16 06:20 djangorestframework-3.13.1.dist-info
```

<br>

`gunicorn.service` 파일에서 `User`, `Group`을 `root`에서 `parkbohee0705`로 변경하고 다시 서비스를 실행하니 정상적으로 동작했다! ☺️

```
# before
User=root
Group=root

# after
User=parkbohee0705
Group=parkbohee0705
```