---
number headings: auto, first-level 1, max 6, contents ^toc, start-at 1, _.1.1.
---
学习视频[视频](https://www.bilibili.com/video/BV1hE411t7RN?p=7&vd_source=7664b55184fd63da03a03ef6c9be4310)

# 环境配置及注意事项
环境配置教程[链接](https://www.bilibili.com/video/BV1hE411t7RN?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)
## 1. jupyter book 集成pytorch环境
1、管理员模式打开anconda prompt 输入``conda install nb_conda`` 
若python版本在3.9以上改为``conda install nb_conda_kernels``

2、``conda activate pytorch ``进入pytorch环境 输入``conda install ipykernel``

3、改变内核 在新建文件时候会显示 如下图所示：![](Pasted%20image%2020231226211958.png)
参考的两篇博客：
[博客1](https://blog.csdn.net/weixin_47038938/article/details/115470086)
[博客2](https://blog.csdn.net/qq_45138078/article/details/129274834)
# 框架学习过程中重要的两大函数
## 1. dir函数
dir（xxx）类似于是将xxx包拆解开 让你知道里面有哪些东西

## 2. help函数
help（xxx）是查询xxx方法的用法  给出官方的解释

# Dataset 数据载入
``注意导入数据集时选择在文件夹中显示项目、然后再将数据集粘到该目录内。
数据加载内容流程如下：
```Python
from torch.utils.data import Dataset  
from PIL import Image  
import os  
class Mydata(Dataset):  # 创建一个类继承Dataset  重写里面的相关方法  
    def __init__(self, root_dir, label_dir):  
        self.root_dir =  root_dir   # 数据集前部分文件夹地址  
        self.label_dir = label_dir  # 数据集后部分文件夹地址，还有标签的作用  
        self.path = os.path.join(root_dir, label_dir) # 将两个地址拼接起来  
        self.img_path = os.listdir(self.path) # 将文件夹的内容放入一个列表中  
  
    def __getitem__(self, idx):  
        img_name = self.img_path[idx] #获取图片的名字  
        img_item_path = os.path.join(self.root_dir, self.label_dir, img_name) #根据名字定位到图片的位置  
        img = Image.open(img_item_path)# 打开图片  
        label = self.label_dir # 标签  
        return img, label  
  
    def __len__(self):  
        return len(self.img_path)  
  
root_dir = 'dataset/train'  
ants_label_dir = 'ants'  
bees_label_dir = 'bees'  
ants_dataset = Mydata(root_dir, ants_label_dir) # 蚂蚁数据集  实例化对象  
bees_dataset = Mydata(root_dir, bees_label_dir) # 蜜蜂数据集  实例化对象  
train_dataset = ants_dataset + bees_dataset # 借用Dataset类中的方法 将两个实例化对象拼接到一起
```

console内容如下：
```Python
from PIL import Image
import os
class Mydata(Dataset):
    def __init__(self, root_dir, label_dir):
        self.root_dir =  root_dir
        self.label_dir = label_dir
        self.path = os.path.join(root_dir, label_dir)
        self.img_path = os.listdir(self.path) 
    def __getitem__(self, idx):
        img_name = self.img_path[idx]
        img_item_path = os.path.join(self.root_dir, self.label_dir, img_name)
        img = Image.open(img_item_path)
        label = self.label_dir
        return img, label
    def __len__(self):
        return len(self.img_path)
root_dir = 'dataset/train'
ants_label_dir = 'ants'
bees_label_dir = 'bees'
ants_dataset = Mydata(root_dir, ants_label_dir)
bees_dataset = Mydata(root_dir, bees_label_dir)
train_dataset = ants_dataset + bees_dataset
len(ants_dataset)
Out[3]: 124
len(bees_dataset)
Out[4]: 121
len(train_dataset)
Out[5]: 245
img,label = train_dataset[123]
img.show()
img,label = train_dataset[124]
img.show()
```

# 认识数据标签
源码如下：
```Python
import os  
  
# 蚂蚁数据集打标签  
# root_dir = 'dataset/train'  
# target_dir = 'ants_image'  
# image_path = os.listdir(os.path.join(root_dir, target_dir))  
# label = target_dir.split('_')[0]  
# out_dir = 'ants_label'  
# for i in image_path:  
#     filename = i.split('.jpg')[0]  
#     with open(os.path.join(root_dir,out_dir,"{}.txt".format(filename)),'w+') as f:  
#         f.write(label)  
  
# 蜜蜂数据集打标签  
root_dir = 'dataset/train'  # 数据源文件夹  
target_dir = 'bees_image'   # 待用数据文件夹  
image_path = os.listdir(os.path.join(root_dir, target_dir)) # 将文件夹的内容存入数组（列表）  
label = target_dir.split('_')[0]    # 将target_dir的内容分割开，取第一个元素  
out_dir = 'bees_label'  # 标签文件保存地址  
for i in image_path:    # 遍历所有文件，将文件名的前部分作为标签文件名，并在标签文件内写入标签内容  
    filename = i.split('.jpg')[0]  
    with open(os.path.join(root_dir,out_dir,"{}.txt".format(filename)),'w+') as f:  
        f.write(label)
```
# TensorBoard
## 1. 如何打开
控制台式输入tensorboard --logdir=logs  其中logs是自己创建的文件夹
## 2. 下载TensorBoard包
进入Pytorch环境输入pip install tensorboard 
## 3. add_image()
- 读取图片
- 格式转换，注意函数参数的接收类型
- 加载到Tensorboard中
代码如下：
```Python
from torch.utils.tensorboard import SummaryWriter  
from PIL import Image  
import numpy as np  
image_path = "data/train/ants_image/67270775_e9fdf77e9d.jpg"  
writer = SummaryWriter("logs")  # logs是自创的文件夹  
img_PIL = Image.open(image_path) # 打开图片  
img_array = np.array(img_PIL)   # 转换格式  
print(img_array.shape)  
writer.add_image("ants", img_array, 1, dataformats='HWC') # 加载到tensorboard
```
## 4. add_scalar()
- 画函数图像 例如y = x
代码如下：
```python
from torch.utils.tensorboard import SummaryWriter  
writer = SummaryWriter("logs")
for i in range(100):  
     writer.add_scalar("y = x", i, i)
```
# Transforms
## 1. 为什么使用Transforms
```
它包装了神经网络的一些参数
```
## 2. 如何使用
```python
# 1、导包
from torchvision import transforms
from torch.utils.tensorboard import SummaryWriter
# 2、使用
writer = SummaryWriter("logs")  
tensor_trans = transforms.ToTensor() # 创建一个Totensor对象  
tensor_img = tensor_trans(img) # 将图片转换为tensor类型  
writer.add_image("Tensor_img", tensor_img) # 将图片加载到tensorboard中  
writer.close()
```
## 3. 常见的Transforms
``多看官方文档  非常重要！
### 3.1. ToTensor 转换类型
将图片转为Tensor类型
```python
from PIL import Image  
from torch.utils.tensorboard import SummaryWriter  
from torchvision import transforms  
img_path = "images/pexels-emre-akyol-18082719.jpg"  
img = Image.open(img_path)  
writer = SummaryWriter("logs")  
print(img)  
# ToTensor  
trans_totensor = transforms.ToTensor() # 创建ToTensor对象  
img_tensor = trans_totensor(img)    # 将图片转为tensor格式  
writer.add_image("ToTensor", img_tensor) # 将其加入到TensorBorad
```
### 3.2. Normalize 标准化
方法详情[链接](https://blog.csdn.net/qq_38406029/article/details/115089644)
```python
# Normalize 归一化  
print(img_tensor[0][0][0]) # 第一channel 第一行 第一列  
trans_norm = transforms.Normalize([0.2, 0.2, 0.2], [0.3, 0.3, 0.3]) # 三个均值 三个标准差  
img_norm = trans_norm(img_tensor) # 将图片标准化  
print(img_norm[0][0][0])  
writer.add_image("Normalize", img_norm, 2)# 加入TensorBorad  
writer.close()
```
### 3.3. Resize 调节尺寸
方法详情[链接](https://blog.csdn.net/qq_40714949/article/details/115393592)
代码如下：
```python
# resize  
trans_resize = transforms.Resize((512, 512))  # 将图调整为512x512
# img PIL -> resize -> img_resize PIL  
img_resize = trans_resize(img)  # 载入图片进行调整
# img_resize PIL -> totensor -> img_reszie tensor  
img_resize = trans_totensor(img_resize)   # 更改类型
writer.add_image("Reszie", img_resize, 0)
```
### 3.4. Compose 多步骤合一
方法详情[链接](https://blog.csdn.net/u013925378/article/details/103363232)
代码如下：
```python
# compose -resize -2  
trans_resize_2 = transforms.Resize(512)  
# PIL -> PIL -> tensor  
trans_compose = transforms.Compose([trans_resize_2, trans_totensor])  # 将图片调整和类型转换步骤合并在一起
trans_resize_2 = trans_compose(img)  # 载入图片
writer.add_image("Resize", trans_resize_2, 1)  # 载入tensorboard
writer.close()
```
### 3.5. RandomCrop 随机裁剪
方法详情[链接](https://blog.csdn.net/lichaoqi1/article/details/123889330)
代码如下：
```python
trans_random = transforms.RandomCrop(512)  # 裁取大小512x512的图片
trans_compose_2 = transforms.Compose([trans_random, trans_totensor])  # 将图片调整和类型转换步骤合并在一起
for i in range(10):  # 裁取十张图片
    img_crop = trans_compose_2(img)  
    writer.add_image("RandomCrop", img_crop, i) # 载入tensorboard
```
# TorchVison中数据集的使用
``1、下载数据集
``2、转换类型
``3、载入TensorBoard
代码如下：
```Python
import torchvision  
from torch.utils.tensorboard import SummaryWriter  

# 将类型转换为tensor类型
dataset_transform = torchvision.transforms.Compose([  
    torchvision.transforms.ToTensor()  
])  
  
train_set = torchvision.datasets.CIFAR10(root="./dataset", train=True, transform=dataset_transform, download=True)  
test_set = torchvision.datasets.CIFAR10(root="./dataset", train=True, transform=dataset_transform, download=True)  
# print(test_set[0])  在没有转为tensor前，输出(<PIL.Image.Image image mode=RGB size=32x32 at 0x24C8C6C2D90>, 6)
# print(test_set.classes)  
# img, target = test_set[0]  自动赋值给img和target
# print(img)  
# print(target)  
# print(test_set.classes[target])  
# img.show()  
# print(test_set[0])  
writer = SummaryWriter("p10")  
for i in range(10):  
    img, target = test_set[i]  
    writer.add_image("test_set", img, i)  # 将前十张图片放入TesorBoard中
writer.close()
```
# DataLoader的使用
``1、准备数据集
``2、将数据集的内容拿出
代码如下：
```python
import torchvision  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
  
# 准备的测试数据集  
test_data = torchvision.datasets.CIFAR10("./dataset", False, transform=torchvision.transforms.ToTensor())  
# 1、batch_size 指每次抽出多少个数据
# 2、shuffle 指下次抽取数据是否要和本次一致
# 3、drop_last 指最后一次如果不够size是否保留
test_loader = DataLoader(dataset=test_data, batch_size=64, shuffle=True, num_workers=0, drop_last=True)  
# 测试数据集第一张图片及target  
img, target = test_data[0]  
print(img.shape)  
print(target)  

writer = SummaryWriter("dataloader")  
for epoch in range(2):  
    step = 0  
    for data in test_loader:  
        imgs, target = data  
        # print(img.shape)  
        # print(target)        
        writer.add_images("Epoch:{}".format(epoch), imgs, step)  # epoch是为了测试shuffle字段
        step = step + 1  
writer.close()
```
# 神经网络基本骨架-nn.Module的使用
``1、方法重写
``2、对象实例化
``3、传入tensor类型参数
代码如下：
```python
import torch  
from torch import nn  
class Tudui(nn.Module):  
    def __init__(self):  
        super().__init__()  
    def forward(self, input):  
        output = input + 1  
        return output  
  
tudui = Tudui()  
x = torch.tensor(1.0)  
output = tudui(x)  # 直接传入x参数也能调用到forward，因为其父类中有__call__方法
print(output)
```

# 卷积的步骤
详情见[17集](https://www.bilibili.com/video/BV1hE411t7RN?p=17&vd_source=7664b55184fd63da03a03ef6c9be4310)
代码如下：
```python
import torch  
import torch.nn.functional as F  
input = torch.tensor([[1, 2, 0, 3, 1],  
                      [0, 1, 2, 3, 1],  
                      [1, 2, 1, 0, 0],  
                      [5, 2, 3, 1, 1],  
                      [2, 1, 0, 1, 1]])  
kernel = torch.tensor([[1, 2, 1],  
                       [0, 1, 0],  
                       [2, 1, 0]])  
  
# 参看官方文档可知input要四维  
input = torch.reshape(input, (1, 1, 5, 5))  
kernel = torch.reshape(kernel, (1, 1, 3, 3))  
print(input.shape)  
print(kernel.shape)  
# stride的作用 控制kernel的步幅
output = F.conv2d(input, kernel, stride=1)  
print(output)  
  
output2 = F.conv2d(input, kernel, stride=2)  
print(output2)  
  
# padding  扩大input的行与列，一般扩充后的位置用0补充
output3 = F.conv2d(input, kernel, stride=1, padding=1)  
print(output3)
```
# 神经网络 - 卷积层
``需要解决的问题？
``1、如何卷积
``2、卷积核个数
``3、可视化
卷积层详情[链接](https://blog.csdn.net/weipf8/article/details/103917202)

代码如下：
```python
import torch  
import torchvision  
from torch import nn  
from torch.nn import Conv2d  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
  
# 准备数据集  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
# 从数据集取出数据的格式  
dataloader = DataLoader(dataset, batch_size=64)  
  
# 搭建训练骨架 继承模块 重写构造方法和forward方法  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        # 以下定义卷积操作，彩色图像输入为rgb三通道  
        self.conv1 = Conv2d(in_channels=3, out_channels=6, kernel_size=3, stride=1, padding=0)  
  
    def forward(self, x):  
        x = self.conv1(x)  
        return x  
  
# 对象实例化  
tudui = Tudui()  
  
# 引入tensorboard  
writer = SummaryWriter("nn_conv2")  
step = 0  
for data in dataloader:  
    imgs, targets = data  
    # 将图片放入卷积层 其中这样写和tudui.forward（imgs）都行  
    output = tudui(imgs)  
    # print(imgs.shape)  
    # print(output.shape)  
    # torch.Size([64, 3, 32, 32])  载入tensorboard  
    writer.add_images("input", imgs, step)  
    # torch.Size([64, 6, 30, 30])  需要改为三通道才可以显示  
    output = torch.reshape(output, (-1, 3, 30, 30))  
    # 载入reshape后的图片  
    writer.add_images("output", output, step)  
    step = step + 1  
writer.close()
```
# 神经网络 - 最大池化的使用
``注：池化不会改变通道数  池化可以理解为采样  压缩数据保持特征  减少电脑的渲染时间  
代码如下：
```python
import torch  
import torchvision  
from torch import nn  
from torch.utils.data import DataLoader  
from torch.nn import MaxPool2d  
from torch.utils.tensorboard import SummaryWriter  
  
# 数据准备  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
dataloader = DataLoader(dataset, batch_size=64)  
# 重写方法  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        # 池化步骤  
        self.maxpool = MaxPool2d(kernel_size=3, ceil_mode=False)  
    def forward(self, input):  
        # 将输入的内容放入池化层  
        output = self.maxpool(input)  
        return output  
tudui = Tudui()  
step = 0  
writer = SummaryWriter("maxpool")  
for data in dataloader:  
    imgs, targets = data  
    writer.add_images("input", imgs, step)  
    output = tudui(imgs)  
    writer.add_images("output", output, step)  
    step = step + 1  
writer.close()
```
# 神经网络 - 非线性激活
``relu和sigmoid都是激活函数。
详情见[链接](https://blog.csdn.net/qq_21190081/article/details/64127103)。
代码如下：
```python
import torch  
import torchvision.datasets  
from torch import nn  
from torch.nn import ReLU, Sigmoid  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
# relu函数效果优于sigmoid函数  
# 准备数据集  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
dataloader = DataLoader(dataset, batch_size=64)  
# 重写方法 构建神经网络  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        self.sigmoid1 = Sigmoid()  
  
    def forward(self, input):  
        output = self.sigmoid1(input)  
        return output  
# 实例化对象  
tudui = Tudui()  
step = 0  
writer = SummaryWriter("ReLu and Sigmoid")  
  
for data in dataloader:  
    imgs, targets = data  
    writer.add_images("input", imgs, step)  
    output = tudui(imgs)  
    writer.add_images("output", output, step)  
    step = step + 1  
writer.close()
```
# 神经网络 - 线性层（全连接层）
``线性层的作用是对输入数据进行线性变换，从而得到新的特征表示。在深度学习中，通常会将线性层与激活函数层组合使用，构成一个完整的神经网络层结构。常见的激活函数包括ReLU、Sigmoid和Tanh等，它们的作用是对线性层的输出进行非线性变换，从而增强模型的表达能力。
代码如下：
```python
import torch  
import torchvision.datasets  
from torch import nn  
from torch.nn import Linear  
from torch.utils.data import DataLoader  
  
# 准备数据  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
dataloader = DataLoader(dataset, batch_size=64, drop_last=True)  
  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        # 改变图像尺寸  
        self.linear1 = Linear(196608, 10)  
    def forward(self,input):  
        output = self.linear1(input)  
        return output  
  
tudui = Tudui()  
  
for data in dataloader:  
    imgs, targets = data  
    print(imgs.shape)  
    # 将图片展平为一条  
    output = torch.flatten(imgs)  
    print(output.shape)  
    output = tudui(output)  
    print(output.shape)
```
# 搭建实战和sequential的使用
参考图片如下：
![](Pasted%20image%2020240112223519.png)

代码如下：
```python
import torch  
from torch import nn  
from torch.nn import Conv2d, MaxPool2d, Flatten, Linear, Sequential  
from torch.utils.tensorboard import SummaryWriter  
  
# 构建神经网络 sequential方法更加方便  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        # self.conv1 = Conv2d(3, 32, 5, padding=2)  
        # self.maxpool1 = MaxPool2d(2)        
        # self.conv2 = Conv2d(32, 32, 5, padding=2)        
        # self.maxpool2 = MaxPool2d(2)        
        # self.conv3 = Conv2d(32, 64, 5, padding=2)        
        # self.maxpool3 = MaxPool2d(2)        
        # self.flatten = Flatten()        
        # self.linear1 = Linear(1024, 64)        
        # self.linear2 = Linear(64, 10)        
        self.module1 = Sequential(  
            Conv2d(3, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 64, 5, padding=2),  
            MaxPool2d(2),  
            Flatten(),  
            Linear(1024, 64),  
            Linear(64, 10)  
        )  
  
    def forward(self, x):  
        # x = self.conv1(x)  
        # x = self.maxpool1(x)        
        # x = self.conv2(x)        
        # x = self.maxpool2(x)        
        # x = self.conv3(x)        
        # x = self.maxpool3(x)        
        # x = self.flatten(x)        
        # x = self.linear1(x)        
        # x = self.linear2(x)        
        x = self.module1(x)  
        return x  
  
tudui = Tudui()  
print(tudui)  
input = torch.ones((64, 3, 32, 32))  
output = tudui(input)  
print(output.shape)  
  
writer = SummaryWriter("nn_seq")  
# graph方法能在tensorboard中看见训练步骤  
writer.add_graph(tudui, input)  
writer.close()
```
# 损失函数和反向传播
``作用：
``1、计算实际输出和目标之间的差距
``2、为我们更新输出提供一定的依据（反向传播），grad
损失函数详情见[链接](https://blog.csdn.net/qq_44942936/article/details/104721868)
代码如下：
```python
import torch  
import torchvision  
from torch import nn  
from torch.nn import Conv2d, MaxPool2d, Flatten, Linear, Sequential  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
  
# 准备数据集  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
dataloader = DataLoader(dataset, batch_size=1)  
  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        self.module1 = Sequential(  
            Conv2d(3, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 64, 5, padding=2),  
            MaxPool2d(2),  
            Flatten(),  
            Linear(1024, 64),  
            Linear(64, 10)  
        )  
  
    def forward(self, x):  
        x = self.module1(x)  
        return x  
# 损失函数
loss = nn.CrossEntropyLoss()  
writer = SummaryWriter("nn_loss_network")  
tudui = Tudui()  
for data in dataloader:  
    imgs, targets = data  
    outputs = tudui(imgs)  
    result_loss = loss(outputs, targets)  
    print(result_loss)  
    # 下降梯度
    result_loss.backward()  
    print("ok")
```
# 优化器optim
``通常与损失函数搭配使用。
优化器详情见[链接](https://zhuanlan.zhihu.com/p/261695487)
代码如下：
```python
import torch  
import torchvision  
from torch import nn  
from torch.nn import Conv2d, MaxPool2d, Flatten, Linear, Sequential  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
  
# 准备数据集  
dataset = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                       download=True)  
dataloader = DataLoader(dataset, batch_size=1)  
  
# 构建神经网络  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        self.module1 = Sequential(  
            Conv2d(3, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 64, 5, padding=2),  
            MaxPool2d(2),  
            Flatten(),  
            Linear(1024, 64),  
            Linear(64, 10)  
        )  
  
    def forward(self, x):  
        x = self.module1(x)  
        return x  
  
  
loss = nn.CrossEntropyLoss()  
tudui = Tudui()  
optim = torch.optim.SGD(tudui.parameters(), lr=0.01)  
for epoch in range(20):  
    # 每一轮开始前loss均设置为零  
    running_loss = 0.0  
    for data in dataloader:  
        imgs, targets = data  
        outputs = tudui(imgs)  
        result_loss = loss(outputs, targets)  
        optim.zero_grad()  
        result_loss.backward()  
        optim.step()  
        # 这一轮整体的loss的求和  
        running_loss = running_loss + result_loss  
    print(running_loss)
```
# 现有网络模型的使用及修改
``去pytorch官网中找相关网络模型。
代码如下：
```python
import torchvision  
from torch import nn  
  
# 预训练的网络  
vgg16_true = torchvision.models.vgg16(weights='DEFAULT')  # pretrained = True  
# 没有预训练的网络  
vgg16_false = torchvision.models.vgg16(weights=None) # pretrained = False  
print(vgg16_true)  
# 在网络中添加全连接层  
vgg16_true.classifier.add_module("add_Linear", nn.Linear(1000, 10))  
print(vgg16_true)  
print(vgg16_false)  
# 修改网络中的全连接层  
vgg16_false.classifier[6] = nn.Linear(4096, 10)  
print(vgg16_false)
```
# 网络模型的保存与读取
代码如下：
```python
from model_save import *  
  
# 方式一 加载模型  
model = torch.load("vgg16_method1.pth")  
print(model)  
  
# 方式二 加载模型  
vgg16 = torchvision.models.vgg16()  
vgg16.load_state_dict(torch.load("vgg16_method2.pth"))  
# model = torch.load("vgg16_method2.pth")  
print(model)  
  
# 陷阱  
# 构建神经网络  
model = torch.load("tudui_method1.pth")  
print(model)
```
# 完整模型的训练套路
``步骤如下：
``1、准备数据集
``2、打印数据集长度
``3、利用DataLoader加载数据集
``4、创建网络模型
``5、损失函数
``6、优化器
``7、设置训练的一些参数
- 记录训练的次数
- 记录测试的次数
- 训练的轮数
``8、添加tensorboard
``9、定好轮数，训练开始
``10、测试开始及保存模型
代码如下：
```python
import torch  
  
import torchvision  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
  
from model import *  
  
# 准备数据集合  
train_data = torchvision.datasets.CIFAR10("./dataset", train=True, transform=torchvision.transforms.ToTensor(),  
                                          download=True)  
  
test_data = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                          download=True)  
  
# 数据集长度  
train_data_size = len(train_data)  
test_data_size = len(test_data)  
print("训练数据集的长度为:{}".format(train_data_size))  
print("测试数据集的长度为:{}".format(test_data_size))  
  
# 利用dataloader来加载数据集  
train_dataloader = DataLoader(train_data, batch_size=64)  
test_dataloader = DataLoader(test_data, batch_size=64)  
  
# 创建网络模型  
tudui = Tudui()  
  
# 损失函数  
loss_fn = nn.CrossEntropyLoss()  
  
# 优化器 梯度下降  
learn_rate = 1e-2  
optimizer = torch.optim.SGD(tudui.parameters(), lr=learn_rate)  
  
# 设置训练的一些参数  
# 记录训练的次数  
total_train_step = 0  
# 记录测试的次数  
total_test_step = 0  
# 训练的轮数  
epoch = 10  
  
# 添加tensorboard  
writer = SummaryWriter("train")  
  
for i in range(epoch):  
    print("------------第 {} 轮训练开始------------".format(i+1))  
  
    # 训练步骤开始  
    tudui.train()  
    for data in train_dataloader:  
        imgs, targets = data  
        outputs = tudui(imgs)  
        loss = loss_fn(outputs, targets)  
  
        # 优化器优化模型  
        optimizer.zero_grad()  
        loss.backward()  
        optimizer.step()  
  
        total_train_step = total_train_step + 1  
        if total_train_step % 100 == 0:  
            print("训练次数:{}, Loss:{}".format(total_train_step, loss.item()))  
            writer.add_scalar("train_loss", loss.item(), total_test_step)  
  
    # 测试步骤开始  
    tudui.eval()  
    total_test_loss = 0  
    total_accuracy = 0  
    with torch.no_grad():  
        for data in test_dataloader:  
            imgs, targets = data  
            # 放入神经网络  
            outputs = tudui(imgs)  
            # 计算loss  
            loss = loss_fn(outputs, targets)  
            # 测试集整体的loss  
            total_test_loss = total_test_loss + loss.item()  
            accuracy = (outputs.argmax(1) == targets).sum()  
            total_accuracy = total_accuracy + accuracy  
    print("测试集整体上的Loss:{}".format(total_test_loss))  
    print("整体测试集上的正确率:{}".format(total_accuracy/test_data_size))  
    writer.add_scalar("test_loss", total_test_loss, total_test_step)  
    total_train_step = total_train_step + 1  
  
    torch.save(tudui, "tudui_{}.pth".format(i))  
    print("模型已保存")  
  
writer.close()
```
# 利用GPU训练
``网络模型、数据（输入、标注）、损失函数这些可以使用.cuda（）,即可以使用gpu进行训练。
``代码加入if torch.cuda.is_available():即是否有显卡都可以运行。
``共有两种方法  个人推荐第一种
代码如下：
```python
import torch  
import torchvision  
from torch import nn  
from torch.nn import Conv2d, Sequential, MaxPool2d, Flatten, Linear  
from torch.utils.data import DataLoader  
from torch.utils.tensorboard import SummaryWriter  
# ******* gpu训练方式一和二 *******
# 定义训练设备  
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")  
# 准备数据集合  
train_data = torchvision.datasets.CIFAR10("./dataset", train=True, transform=torchvision.transforms.ToTensor(),  
                                          download=True)  
  
test_data = torchvision.datasets.CIFAR10("./dataset", train=False, transform=torchvision.transforms.ToTensor(),  
                                          download=True)  
  
# 数据集长度  
train_data_size = len(train_data)  
test_data_size = len(test_data)  
print("训练数据集的长度为:{}".format(train_data_size))  
print("测试数据集的长度为:{}".format(test_data_size))  
  
# 利用dataloader来加载数据集  
train_dataloader = DataLoader(train_data, batch_size=64)  
test_dataloader = DataLoader(test_data, batch_size=64)  
  
# 创建网络模型  
class Tudui(nn.Module):  
    def __init__(self):  
        super(Tudui, self).__init__()  
        self.module1 = Sequential(  
            Conv2d(3, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 32, 5, padding=2),  
            MaxPool2d(2),  
            Conv2d(32, 64, 5, padding=2),  
            MaxPool2d(2),  
            Flatten(),  
            Linear(1024, 64),  
            Linear(64, 10)  
        )  
  
    def forward(self, x):  
        x = self.module1(x)  
        return x  
  
tudui = Tudui()  
# 方式一  
# if torch.cuda.is_available():  
#     tudui = tudui.cuda()  
# 方式二  
tudui = tudui.to(device)  
# 损失函数  
loss_fn = nn.CrossEntropyLoss()  
# 方式一  
# loss_fn = loss_fn.cuda()  
# 方式二  
loss_fn = loss_fn.to(device)  
# 优化器 梯度下降  
learn_rate = 1e-2  
optimizer = torch.optim.SGD(tudui.parameters(), lr=learn_rate)  
  
# 设置训练的一些参数  
# 记录训练的次数  
total_train_step = 0  
# 记录测试的次数  
total_test_step = 0  
# 训练的轮数  
epoch = 10  
  
# 添加tensorboard  
writer = SummaryWriter("train")  
  
for i in range(epoch):  
    print("------------第 {} 轮训练开始------------".format(i+1))  
  
    # 训练步骤开始  
    tudui.train()  
    for data in train_dataloader:  
        imgs, targets = data  
        # 方式一  
        # if torch.cuda.is_available():  
        #     imgs = imgs.cuda()        #     targets = targets.cuda()        # 方式二  
        imgs = imgs.to(device)  
        targets = targets.to(device)  
  
        outputs = tudui(imgs)  
        loss = loss_fn(outputs, targets)  
  
        # 优化器优化模型  
        optimizer.zero_grad()  
        loss.backward()  
        optimizer.step()  
  
        total_train_step = total_train_step + 1  
        if total_train_step % 100 == 0:  
            print("训练次数:{}, Loss:{}".format(total_train_step, loss.item()))  
            writer.add_scalar("train_loss", loss.item(), total_train_step)  
  
    # 测试步骤开始  
    tudui.eval()  
    total_test_loss = 0  
    total_accuracy = 0  
    with torch.no_grad():  
        for data in test_dataloader:  
            imgs, targets = data  
            # 方式一  
            # if torch.cuda.is_available():  
            #     imgs = imgs.cuda()            
            #     targets = targets.cuda()            
            # 方式二  
            imgs = imgs.to(device)  
            targets = targets.to(device)  
            # 放入神经网络  
            outputs = tudui(imgs)  
            # 计算loss  
            loss = loss_fn(outputs, targets)  
            # 测试集整体的loss  
            total_test_loss = total_test_loss + loss.item()  
            accuracy = (outputs.argmax(1) == targets).sum()  
            total_accuracy = total_accuracy + accuracy  
    print("测试集整体上的Loss:{}".format(total_test_loss))  
    print("整体测试集上的正确率:{}".format(total_accuracy/test_data_size))  
    writer.add_scalar("test_loss", total_test_loss, total_test_step)  
    total_test_step = total_test_step + 1  
  
    torch.save(tudui, "tudui_{}.pth".format(i))  
    print("模型已保存")  
  
writer.close()
```
# 完整的模型验证（测试、demo）套路——利用已经训练好的模型，给它提供输入
``将已经训练好的模型，输入一些相关内容，让模型去判断,最后得出输入的内容是什么。
```python
import torch  
import torchvision.transforms  
from PIL import Image  
from model import *  
image_path = "./images/img.png"  
image = Image.open(image_path)  
print(image)  
image.convert('RGB')  
transform = torchvision.transforms.Compose([torchvision.transforms.Resize((32, 32)),  
                                            torchvision.transforms.ToTensor()])  
image = transform(image)  
print(image.shape)  
  
device = torch.device("cpu")  
model = torch.load("tudui_9.pth", map_location=device)  
print(model)  
image = torch.reshape(image, (1, 3, 32, 32))  
model.eval()  
with torch.no_grad():  
    output = model(image)  
print(output)  
print(output.argmax(1))
```
# 在github上找开源项目
