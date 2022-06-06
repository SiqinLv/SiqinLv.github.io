## Linux环境下:
>- 查看当前Cuda的版本，即实际安装的Cuda版本：nvidia-smi
>- 查看所有环境：conda env list
>- 退出虚拟环境：conda deactivate
>- 创建虚拟环境：conda create -n 虚拟环境名字 python=版本号 （2.7 / 3.6 / 3.7/ 3.8等可用的版本）
>- 删除虚拟环境：conda remove -n 虚拟环境的名字 --all
>- 切换环境：source activate 名字
### linux下环境安装：
> 安装Anaconda3:
 1. wget https://repo.anaconda.com/archive/Anaconda3-2019.07-Linux-x86_64.sh
 2. bash Anaconda3-5.0.1-Linux-x86_64.sh
 3. 查看是否安装成功：
  `conda`
 4. 镜像源</br>
  - 恢复莫人源：`conda config --remove-key channels`
  - 修改镜像源
   `
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  `
# 设置搜索时显示通道地址
conda config --set show_channel_urls yes

   `
> 升级pip
  `python -m pip install --upgrade pip`
> pytorch环境
 1. conda install pytorch torchvision torchaudio cudatoolkit=11.6 -c pytorch
> tensorflow环境
 1. wget http://mirrors.aliyun.com/pypi/simple/tensorflow-gpu/tensorflow_gpu-2.9.0rc2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl
 2. conda install tensorflow-gpu
#### pytorch环境
>+ conda install pytorch torchvision torchaudio cudatoolkit=11.6 -c pytorch
#### GPU测试：
 --- 
> 判断可行性:


```python
import torch
print("torch version:",torch.__version__)
print("torch if cuda is available:",torch.cuda.is_available())
print('GPU name:'+ str(torch.cuda.get_device_name()))
print('Number of cuda:'+ str(torch.cuda.device_count()))
print("-------------------------------------------------------------")

import tensorflow as tf
version=tf.__version__  #输出tensorflow版本
gpu_ok=tf.test.is_gpu_available()  #输出gpu可否使用（True/False）
print("tensorflow版本",version)
print("GPU是否可用",gpu_ok)
print("tensorflow中cuda是否可用",tf.test.is_built_with_cuda())  # 判断CUDA是否可用（True/False）

```
<hr/>

#### pytorch测试:

```python
import torch
import torch.nn as nn
from torch.autograd import Variable
import torch.utils.data as Data
import torchvision
import time

# import matplotlib.pyplot as plt

torch.manual_seed(1)

EPOCH = 1
BATCH_SIZE = 50
LR = 0.001
DOWNLOAD_MNIST = True
if_use_gpu = 1

# 获取训练集dataset
training_data = torchvision.datasets.MNIST(
    root='./mnist/',  # dataset存储路径
    train=True,  # True表示是train训练集，False表示test测试集
    transform=torchvision.transforms.ToTensor(),  # 将原数据规范化到（0,1）区间
    download=DOWNLOAD_MNIST,
)

# 打印MNIST数据集的训练集及测试集的尺寸
print(training_data.train_data.size())
print(training_data.train_labels.size())
# torch.Size([60000, 28, 28])
# torch.Size([60000])

# plt.imshow(training_data.train_data[0].numpy(), cmap='gray')
# plt.title('%i' % training_data.train_labels[0])
# plt.show()

# 通过torchvision.datasets获取的dataset格式可直接可置于DataLoader
train_loader = Data.DataLoader(dataset=training_data, batch_size=BATCH_SIZE,
                               shuffle=True)

# 获取测试集dataset
test_data = torchvision.datasets.MNIST(
    root='./mnist/',  # dataset存储路径
    train=False,  # True表示是train训练集，False表示test测试集
    transform=torchvision.transforms.ToTensor(),  # 将原数据规范化到（0,1）区间
    download=DOWNLOAD_MNIST,
)
# 取前全部10000个测试集样本
test_x = Variable(torch.unsqueeze(test_data.test_data, dim=1).float(), requires_grad=False)
# test_x = test_x.cuda()
## (~, 28, 28) to (~, 1, 28, 28), in range(0,1)
test_y = test_data.test_labels


# test_y = test_y.cuda()
class CNN(nn.Module):
    def __init__(self):
        super(CNN, self).__init__()
        self.conv1 = nn.Sequential(  # (1,28,28)
            nn.Conv2d(in_channels=1, out_channels=16, kernel_size=5,
                      stride=1, padding=2),  # (16,28,28)
            # 想要con2d卷积出来的图片尺寸没有变化, padding=(kernel_size-1)/2
            nn.ReLU(),
            nn.MaxPool2d(kernel_size=2)  # (16,14,14)
        )
        self.conv2 = nn.Sequential(  # (16,14,14)
            nn.Conv2d(16, 32, 5, 1, 2),  # (32,14,14)
            nn.ReLU(),
            nn.MaxPool2d(2)  # (32,7,7)
        )
        self.out = nn.Linear(32 * 7 * 7, 10)

    def forward(self, x):
        x = self.conv1(x)
        x = self.conv2(x)
        x = x.view(x.size(0), -1)  # 将（batch，32,7,7）展平为（batch，32*7*7）
        output = self.out(x)
        return output


cnn = CNN()
if if_use_gpu:
    cnn = cnn.cuda()

optimizer = torch.optim.Adam(cnn.parameters(), lr=LR)
loss_function = nn.CrossEntropyLoss()

for epoch in range(EPOCH):
    start = time.time()
    for step, (x, y) in enumerate(train_loader):
        b_x = Variable(x, requires_grad=False)
        b_y = Variable(y, requires_grad=False)
        if if_use_gpu:
            b_x = b_x.cuda()
            b_y = b_y.cuda()

        output = cnn(b_x)
        loss = loss_function(output, b_y)
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()

        if step % 100 == 0:
            print('Epoch:', epoch, '|Step:', step,
                  '|train loss:%.4f' % loss.item())
    duration = time.time() - start
    print('Training duation: %.4f' % duration)

cnn = cnn.cpu()
test_output = cnn(test_x)
pred_y = torch.max(test_output, 1)[1].data.squeeze()
accuracy = sum(pred_y == test_y) / test_y.size(0)
print('Test Acc: %.4f' % accuracy)
```

<hr/>

### tensorflow测试:
```python
# import tensorflow as tf
# if tf.test.gpu_device_name():
#     print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
# else:
#     print("Please install GPU version of TF")
import tensorflow as tf

# tensorflow_version = tf.__version__
# gpu_available = tf.test.is_gpu_available()
#
# print('tensorflow version:',tensorflow_version, '\tGPU available:', gpu_available)
#
# a = tf.constant([1.0, 2.0], name='a')
# b = tf.constant([1.0, 2.0], name='b')
# result = tf.add(a,b, name='add')
import tensorflow as tf
print('Tensorflow Version: {}'.format(tf.__version__))

tf.debugging.set_log_device_placement(True)
# import os
# os.environ["CUDA_DEVICE_ORDER"] = "PCI_BUS_ID"
# os.environ["CUDA_VISIBLE_DEVICES"] = "0" # 选择ID为0的GPU
# import os
# os.environ["CUDA_VISIBLE_DEVICES"] = "2"
# gpus = tf.config.experimental.list_physical_devices('GPU')


(train_image, train_lable), (test_image, test_label) = tf.keras.datasets.fashion_mnist.load_data()
train_image = train_image/255
test_image = test_image/255
model = tf.keras.Sequential()
model.add(tf.keras.layers.Flatten(input_shape=(28,28)))  # 28*28
model.add(tf.keras.layers.Dense(128, activation='relu'))
model.add(tf.keras.layers.Dense(10, activation='softmax'))
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['acc']
)
model.evaluate(test_image, test_label)

```

<hr/>

### paddlepaddle测试：
```python
import paddle
r = paddle.fluid.is_compiled_with_cuda()
print(r)
```

#### GPU测试：
>- 查看显卡： `lspci | grep -i nvidia`
>- Conda安装tensorflow:conda install tensorflow-gpu
>>- ***依赖包：***
>>>- `conda install cudatoolkit`
>>>- `conda install cudnn`
>>- ***paddlePaddle安装:***
>>>- Conda安装Paddlepaddle:pip3 install paddlepaddle==1.4.1 -i https://pypi.douban.com/simple 会报错
>>>- 解决方案：
>>>>- 参考网址：[Paddlepaddle安装问题](https://github.com/PaddlePaddle/Paddle/issues/40559)
>>>>
>>>>- 安装 paddle_bfloat：`wget https://files.pythonhosted.org/packages/8a/8e/f2b5a82551f1397c6496f47d588b6fdd4811b720d0812effe368bec30b97/paddle_bfloat-0.1.2-cp37-cp37m-manylinux_2_27_x86_64.whl`
>>>>- 将paddle_bfloat-0.1.2-cp37-cp37m-manylinux_2_27_x86_64.whl名称改为paddle_bfloat-0.1.2-cp37-cp37m-linux_x86_64.whl
>>>>- `pip install paddle_bfloat-0.1.2-cp37-cp37m-linux_x86_64.whl`

 --- 

## Window环境下：
>- 切换环境：conda activate 名字

### 其他：
>- tensorflow包下载：[tensorflow安装包](http://mirrors.aliyun.com/pypi/simple/tensorflow-gpu/)
>-运维人员用过的命名，可能是配置GPU啥的：
 ![image](https://user-images.githubusercontent.com/70061450/171532772-646df603-df4c-4c29-9307-94c913564ff6.png)
 ![image](https://user-images.githubusercontent.com/70061450/171533022-47a9fa98-5dd6-4aba-acaa-f38c860111d3.png)
 ![image](https://user-images.githubusercontent.com/70061450/171533140-848fb3f3-818d-45d9-8f0d-0e8129e5cc7b.png)


