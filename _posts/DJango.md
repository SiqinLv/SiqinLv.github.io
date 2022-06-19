- 虚拟环境
- sudo pip install django
- 搭建虚拟环境：
  - sudo pip install virtualenv
  - sudo pip install virtualenvwrapper
  - 配置环境变量：
    ```python
    # 1、创建目录用来存放虚拟环境
    $HOME/.virtualenvs
    
    # 2、打开~/.bashrc文件，并添加如下：
    export WORKON_HOME=$HOME/.virtualenvs
    source /usr/local/bin/virtualenvwrapper.sh
    
    # 3、运行
    source ~/.bashrc
    ```
- 创建虚拟环境
>- `mkvirtualenv -p python3 py3_django_11`， 若不加python3默认是python2，py3_django_11为虚拟环境的名字
>- 输入命令后，默认进入虚拟环境了。
>- 查看虚拟环境`workon`
>- 切换虚拟环境：workon 虚拟环境名称
>- 删除虚拟环境：rmvirtualenv 虚拟环境名称
>- 不能删除正在使用的虚拟环境，需要退出当前环境:deactivate
>- 在虚拟环境下，查看虚拟环境的路径：witch python
>- 创建Django项目
  - 通过指令创建工程：django-adimin startproject 项目name
  - manage.py为管理工具/脚本（例如：创建子应用的时候户用到它）
  - settings.py：设置相关的
  - url.py:路由相关
  - wsgu.py:程序的入口
  - 工程运行：python manage.py runserver,默认端口号为8000
  - 帮助指定：python manage.py --help
  - 修改运行的ip和端口：python manage.py runserver 127.0.0.1:8001
>- 创建子应用 
  - python manager.py startapp 项目name
  - 例：python manage.py startapp login,python manage.py startapp pay,python manage.py startapp book
    - migrations:和迁移相关
    - model.py:模型相关
    - test.py:测试相关
    - view.py:视图相关
    - admin.py:和后台相关
    - app.py:和当前子应用相关
>- json
  - json.dumps 将字典转换为 JSON形式的字符串
  - json.loads 将JSON形式的字符串转换成JSON
  - from django.http import JsonResponse
    - return JsonResponse(data)  JsonResponse返回JSON形式的字符串
>- 数据保存在客户端用cookie，保存在服务器用session
