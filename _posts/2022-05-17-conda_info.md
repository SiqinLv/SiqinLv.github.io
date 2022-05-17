## Linux:
>- 查看当前Cuda的版本，即实际安装的Cuda版本：nvidia-smi
>- 查看所有环境：conda env list
>- 退出虚拟环境：conda deactivate
>- 创建虚拟环境：conda create -n 虚拟环境名字 python=版本号 （2.7 / 3.6 / 3.7/ 3.8等可用的版本）
>- 删除虚拟环境：conda remove -n 虚拟环境的名字 --all
>- 切换环境：source activate 名字
#### GPU测试：
<hr/>
*** pytorch:***

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

#### tensorflow测试:
```python
# import tensorflow as tf
# if tf.test.gpu_device_name():
#     print('Default GPU Device: {}'.format(tf.test.gpu_device_name()))
# else:
#     print("Please install GPU version of TF")
import tensorflow as tf

tensorflow_version = tf.__version__
gpu_available = tf.test.is_gpu_available()

print('tensorflow version:',tensorflow_version, '\tGPU available:', gpu_available)

a = tf.constant([1.0, 2.0], name='a')
b = tf.constant([1.0, 2.0], name='b')
result = tf.add(a,b, name='add')
print(result)

```

<hr/>

#### paddlepaddle测试：
```python
import paddle
r = paddle.fluid.is_compiled_with_cuda()
print(r)
```

## Window环境下：
>- 切换环境：conda activate 名字
### GPU测试：
>- 查看显卡： lspci \| grep -i nvidia
>- **Conda安装tensorflow:conda install tensorflow-gpu**
>>- ***依赖包***：
>>>- ****conda install cudatoolkit****
>>>- ****conda install cudnn****
>>- ***paddlePaddle安装:***
>>>- Conda安装Paddlepaddle:pip3 install paddlepaddle==1.4.1 -i https://pypi.douban.com/simple 会报错
>>>- ***解决方案：***
>>>>- 参考网址：https://github.com/PaddlePaddle/Paddle/issues/40559
>>>>- ****安装 paddle_bfloat：wget https://files.pythonhosted.org/packages/8a/8e/f2b5a82551f1397c6496f47d588b6fdd4811b720d0812effe368bec30b97/paddle_bfloat-0.1.2-cp37-cp37m-manylinux_2_27_x86_64.whl****
>>>>- ****将paddle_bfloat-0.1.2-cp37-cp37m-manylinux_2_27_x86_64.whl名称改为paddle_bfloat-0.1.2-cp37-cp37m-linux_x86_64.whl****
>>>>- ****pip install paddle_bfloat-0.1.2-cp37-cp37m-linux_x86_64.whl****
