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
- 创建虚拟黄精
