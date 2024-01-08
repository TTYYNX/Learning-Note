---
number headings: auto, first-level 1, max 6, contents ^toc, start-at 1, _.1.1.
---
# jupyter notebook的使用
## 1. 默认路径修改[链接](https://blog.csdn.net/yuanxiang01/article/details/79217469)
## 2. 快速运行代码
shift + enter
## 3. 快捷键
![](Pasted%20image%2020231122160831.png)
# Matplotlib
## 1. 什么是Matplotlib？
他是一个画二维图表的Python库
## 2. 为什么学习它？
为了数据可视化，方便选择更合适的分析方法
奥卡姆剃刀原理 - 如无必要，不增实体

## 3. 实现一个简单的画图
```Python
import matplotlib.pyplot as plt
%matplotlib inline

plt.figure()
plt.plot([1, 0, 9],[4, 5, 6])
plt.show

```
## 4. 折线图绘制
```Python
# 折线图
# 温度变化折线图
import matplotlib.pyplot as plt
%matplotlib inline
import random

# 1、准备数据
x = range(60)
y_shanghai = [random.uniform(15,18) for i in x]
y_beijing = [random.uniform(1,3) for i in x]

# 中文显示问题
plt.rcParams['font.sans-serif']=['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus']=False #用来正常显示负号

# 2、创建画布
plt.figure(figsize=(20,8),dpi=80)

# 3、绘制图像
plt.plot(x, y_shanghai, color="r",linestyle='-.',label="上海")
plt.plot(x, y_beijing, color="b",label="北京")

# 显示图例
plt.legend()
# plt.legend(loc="lower left")
# plt.legend(loc=4)

# 修改x y刻度
x_label = ["11分{}秒".format(i) for i in x]
plt.xticks(x[::5],x_label[::5])
plt.yticks(range(0,40,5))

# 显示网格
plt.grid(linestyle='--', alpha=0.5)

# 添加描述 标题
plt.xlabel("时间")
plt.ylabel("温度")
plt.title("上海、北京11点0分到12点之间的温度变化图示")

# 4、显示图像
plt.show()
```
图片如下所示：
![](Pasted%20image%2020231126221551.png)
## 5. 多坐标系绘制
```Python
# 多坐标系
# 温度变化折线图
import matplotlib.pyplot as plt
%matplotlib inline
import random

# 1、准备数据
x = range(60)
y_shanghai = [random.uniform(15,18) for i in x]
y_beijing = [random.uniform(1,3) for i in x]

# 2、创建画布
# plt.figure(figsize=(20,8),dpi=80)
figure, axes = plt.subplots(nrows=1,ncols=2,figsize=(20,8),dpi=80)

# 3、绘制图像
axes[0].plot(x, y_shanghai, color="r",linestyle='-.',label="上海")
axes[1].plot(x, y_beijing, color="b",label="北京")

# 显示图例
axes[0].legend()
axes[1].legend()
# plt.legend(loc="lower left")
# plt.legend(loc=4)

# 修改x y刻度
x_label = ["11分{}秒".format(i) for i in x]
axes[0].set_xticks(x[::5])
axes[0].set_xticklabels(x_label[::5])
axes[0].set_yticks(range(0,40,5))
axes[1].set_xticks(x[::5])
axes[1].set_xticklabels(x_label[::5])
axes[1].set_yticks(range(0,40,5))

# 显示网格
axes[0].grid(linestyle='--', alpha=0.5)
axes[1].grid(linestyle='--', alpha=0.5)

# 添加描述 标题
axes[0].set_xlabel("时间")
axes[0].set_ylabel("温度")
axes[0].set_title("上海11点0分到12点之间的温度变化图示")

axes[1].set_xlabel("时间")
axes[1].set_ylabel("温度")
axes[1].set_title("北京11点0分到12点之间的温度变化图示")

# 4、显示图像
plt.show()
```
图片如下所示：
![](Pasted%20image%2020231126221719.png)
