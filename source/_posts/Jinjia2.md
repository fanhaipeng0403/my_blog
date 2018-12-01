---
title: Jinjia2
date: 2016-02-18 22:55:18
tags:
---



模板过滤器
http://stackoverflow.com/questions/12288454/how-to-import-custom-jinja2-filters-from-another-file-and-using-flask

```
app.jinja_env.filters['datetimeformat'] = utils.format_datetime
app.jinja_env.filters['dateformat'] = utils.format_date
app.jinja_env.filters['timedeltaformat'] = utils.format_timedelta
app.jinja_env.filters['displayopenid'] = utils.display_openid
```
