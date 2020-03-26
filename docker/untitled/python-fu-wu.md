# python服务

1.dockerfile文件

```text
from flask import FROM python:3. 7- stretch
# Copy requirements. txt and uwsgi.ini file 
COPY requirements. txt / tmp/
COPY uwsgi.ini /etc/uwsgi/
# Upgrade pip and install required python packages
RUN pip install -U pip 
RUN pip install -r /tmp/ requi rements . txt
# Which uWSGI .ini file should be used, to make it customizable
ENV UWSGI_ INI /app/uwsgi.ini
# By default, run 2 processes
ENV UWSGI_ CHEAPER 2
# By default, when on demand, run up to 16 processes
ENV UWSGI_ PROCESSES 16
# Add demo app
COPY ./app /app
WORKDIR /app
CMD ["/usr/local/bin/uwsgi", "--ini=/etc/uwsgi/uwsgi . ini", "--die-on-term" ，"--need-app", "-- stats-http"]
```

2.更新中.............

