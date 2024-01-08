---
number headings: auto, first-level 1, max 6, contents ^toc, start-at 1, _.1.1.
---
学习视频[视频](https://www.bilibili.com/video/BV1hE411t7RN?p=7&vd_source=7664b55184fd63da03a03ef6c9be4310)

# 环境配置及注意事项
环境配置教程[链接](https://www.bilibili.com/video/BV1hE411t7RN?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)
pycharm环境配置[链接](https://www.bilibili.com/video/BV1hE411t7RN?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)

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


