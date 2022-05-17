Linux:
查看所有环境：conda env list
退出虚拟环境：conda deactivate
创建虚拟环境：conda create -n 虚拟环境名字 python=版本号 （2.7 / 3.6 / 3.7/ 3.8等可用的版本）
删除虚拟环境：conda remove -n 虚拟环境的名字 --all
切换环境：source activate 名字
Window：
切换环境：conda activate 名字
GPU测试：
查看显卡： lspci | grep -i nvidia
