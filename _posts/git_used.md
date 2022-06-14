## 安装git
> CentOS:
  `
    sudo yum install git-all
    git --version
  `
> Ubuntu:
`
  sudo apt-get install git
`
> Windows:
`
  https://git-scm.com/downloads
`
## 本地 Git 关联 GitHub 远程仓库
1. 生成秘钥

  `ssh-keygen -t rsa -C "XXXX@XXX.com"`
  第一步确定秘钥生成目录，直接回车
  
  第二三步输入密码
  
  秘钥生成后，进入秘钥目录，比如我的为/c/Users/baimo/.ssh/id_rsa，复制备用
2. 进入 GitHub https://www.github.com，打开设置
3. 新建一个 SSH key
4. 填写 SSH key,key为id_rsa.pub内容
5. 新建 GitHub 仓库
6. 将 GitHub 仓库与我们本地的 Git 仓库进行关联
  `
    git init
    git remote add origin https://github.com/qqdb/example01.git
  `
7. 提交
  - 第一次提交：`git push -u origin master` 也可用强制提交`git push -f origin master`
  - 之后提交：`git push origin master`
8. 使用pycharm连接github
  > File->settings->GitHub 点击add account登录github账号
  > 若无法登录，在github中的添加令牌
  > 个人令牌设置：
  >> 设置->开发者设置->个人访问令牌，勾选所有选项并添加令牌
  >> 添加成功后会显示token，复制token在pycharm中使用token登录
9. 配置git
  > 在setting的面板中选择git,在面板内容处的path to Git executable：填入git可执行文件路径，如`D:\lvsiqin\APPlist\Git\bin\git.exe`
10. 在pycharm工具栏选择VCS->Import into Version Control->Share Project GitHub后，上传本地代码到github上
  > 也可将github上的代码克隆到本地VCS->Get from Version Control
  >> 克隆自己的选择GitHub
  >> 克隆别人的选择repository URL,并写入ul地址，和本地路径
  >> 完成后会有读条
11. 从pycharm中查看github: file->Open on GitHub
12. 一般的Git操作：VCS->Git->...
13. 参与一个GitHub项目：
  > fork一个项目 Fork是GitHub存储库的副本，可在不影响原始项目的情况下更改代码。比如，https://github.com/scikit-learn/scikit-learn
  > 进入 Pycharm 的版本控制界面VCS->Get from Version Control->GitHub-> ... clone后，等进度跑完我们会得到项目的仓库
14. 查看项目参与者的操作日志 控制台下的log
15. 项目参与者创建pull请求
  > VCS->git->View Pull Resquests，在description填入pull请求
16. 项目的维护者管理pull请求
  > VCS->git->View Pull Requests
  > 查看pull请求信息:`stateopen ...`
  
参考来自[git和gitHub使用](https://zhuanlan.zhihu.com/p/145649307)
