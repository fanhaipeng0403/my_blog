---
title: Flask
date: 2017-02-10 13:25:39
tags:  Flask

---

flask快速启动


flask代码块
http://flask.pocoo.org/snippets/

flask的网站
http://flask.pocoo.org/community/poweredby/

flask中文学习网
http://flask123.sinaapp.com/article/63/
http://docs.pythontab.com/
http://python.usyiyi.cn/

flask最佳实践
https://spacewander.github.io/explore-flask-zh/1-introduction.html

flask大型项目目录
https://github.com/Robpol86/Flask-Large-Application-Example


插件
flask_themes: 皮肤，博客必不可少的
flask_sqlalchemy: flask对sqlalchemy的插件，定义了一些方法，使创建models和输出query更方便
flask_wtf: 对wtforms的插件，默认加入了csrf功能（防止表单重复提交）和Recaptcha（验证码）
flask_uploads: 上传文件的插件
flask_cache: 缓存插件（支持memcached,gaememcached,filesystem,simple等）
flask_principal: 权限插件 (众多插件中比较复杂的一个, 但也是作用很大的一个)，支持各种权限方式，较django admin的权限，我只能说，这个插件让你知道，权限其实很简单。
flask_mail: 发送邮件插件
flask_script: 项目管理插件，类似django的manager
flask_babel: 多语言支持，使用非常方便，（request.accept_languages.best_match判断语言有点怪，好象会根据系统语言判断，待深究）
singals: 其实信号不常用，因为sqlalchemy太强大了，不过也会有用它的地方的。
twitter: 这个非flask插件，是twitter的api，很有意思的功能，在线发推啦（国内主机不能支持这个功能）
pygments: 代码高亮
https://github.com/humiaozuzu/awesome-flask



## 项目快速启动脚本

每个团队都有自己的项目规范，分享平时的开发中经常用到的项目结构，仅供参考。


```
# !/bin/bash

dirname=$1

if [ ! -d "$dirname" ]
then
    mkdir ./$dirname && cd $dirname
    mkdir ./application
    mkdir -p ./application/{controllers,models,static,static/css,static/js,templates}
    touch {manage.py,requirements.txt}
    touch ./application/{__init__.py,app.py,configs.py,extensions.py}
    touch ./application/{controllers/__init__.py,models/__init__.py}
    touch ./application/{static/css/style.css,templates/404.html,templates/base.html}
    echo "File created"
else
    echo "File exists"
fi
```


