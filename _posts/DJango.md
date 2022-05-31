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
