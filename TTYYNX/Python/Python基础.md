---
number headings: auto, first-level 1, max 6, contents ^toc, start-at 1, _.1.1.
---
# 前期准备
## 1. IDE：Jupyter Notebook(Anaconda包含) or Pycharm下载[链接](https://www.jetbrains.com/zh-cn/pycharm/download/?section=windows)
## 2. Python的数据包 Anaconda,下载[链接](https://www.anaconda.com/download)
## 3. Python库下载地址[链接](https://www.lfd.uci.edu/~gohlke/pythonlibs/)
## 4. Pycharm关联Anaconda视频[链接](https://www.bilibili.com/video/BV1By4y1F7aY/?spm_id_from=333.880.my_history.page.click&vd_source=7664b55184fd63da03a03ef6c9be4310)
## 5. pycharm中配置anaconda的虚拟环境博客[链接](https://blog.csdn.net/ECHOSON/article/details/117220445)
# 1. 学习问题解析
## 1. 更改Jupyter  NoteBook 默认文件路径[链接](https://blog.csdn.net/C_ironhead/article/details/125148760)
## 2. pip install 安装的包放的位置[链接](https://blog.csdn.net/inthat/article/details/118711569)
## 3. 复习[链接](https://www.bilibili.com/video/BV1K14y1c75e/?spm_id_from=333.337.search-card.all.click&vd_source=7664b55184fd63da03a03ef6c9be4310)
# 基础内容
## 1. print
### 1.1. 转义字符``"\"``
Python 会将``"\"``后面的内容一起读出来。
如需换行输入``"\n"``即可。
### 1.2. 多换行
若需要输出跨行多的文本或者数字。在print语句中使用``"""``即可
## 2. 变量
应该见名知意，不能有空格等，下斜杠可以有
不能占用关键字。
## 3. 数学运算
次方运算用 ** ，例如``2**3`` 就是2的三次方。
math函数库，导包即可。可以查看math官方文档，支持的内容有哪些。
## 4. 注释
单行注释``#``,其中多行一起注释选中内容后按 ctrl+/ 即可
多行注释``"""``
## 5. 数据类型
字符串 str leng()函数得到字符串函数 通过索引即可获取单个字符
整数 int
浮点型 float
布尔类型 bool 返回 true 或者 false
空值类型 NoneType
返回数据类型 Type(内容)函数
## 6. input函数
作用是给用户展示并且接收用户输入的值
例如input("请输入您的年龄：")
将会在控制台显示该内容并等待    请输入您的年龄：

其中input会有返回值，返回值类型为字符串类型
转换为整型用 int("内容")函数
类似的还有float("内容")函数、str("内容")函数
## 7. 条件语句
```Python
if 条件:
	内容1
	内容2
else：
	内容3
	内容4
	
嵌套 1
if 条件
	内容
	if 条件
		内容
	else：
		内容
else：
	内容

嵌套 2
if 条件：
	内容
elif 条件
	内容
elif 条件
	内容
else：
	内容
```

## 8. 逻辑运算
and 对应于 &&
or 对应于 ||
not 对应于 ！
但Python 中有优先级顺序
其中not > and > or
## 9. 列表
列表是可变数据类型

列表用``[]``表示

列表名.append("内容")向列表中添加内容

列表可以直接用print打印出来

列表名.remove("内容")在列表中删除内容

其中leng(列表名)函数可以得出列表的长度

其中还可以通过列表名``[索引号]``得到列表的元素，或是对该元素进行某些操作

列表排序函数sorted(列表名)

列表最大值max(列表名)

列表最小值min(列表名) 
## 10. 字典
字典名 = {键1 : 值1,
				键2 : 值2,
				键3 : 值3,
				……}
插入数据   字典名``[键]`` = ``值``
获取某个键的值，即为字典名``[键]``

字典的键必须是不可变的数据类型

字典是可变的数据类型

元组数据类型，和列表相比它不可变，用``()``表示

相关字典函数如下：

![](Pasted%20image%2020231112161658.png)
## 11. for循环
### 11.1. 样式一
for 变量名 in 可迭代对象:
	相关操作
	……
### 11.2. 样式二
for 变量名 in range(num1,num2,num3):
	相关操作
	……


num3代表循环步幅，若num3没有写，则默认循环步幅为1
其中i的取值范围是 ``num1 <= i < num2``
## 12. while循环
while 条件:
	相关操作
## 13. 格式化字符串
format函数的使用方法
[链接](https://www.runoob.com/python/att-string-format.html)
## 14. 函数
### 14.1. 无参函数
def 函数名():
	相关代码
	……
	return xxx
### 14.2. 有参函数
def 函数名(变量1，变量2，……):
	相关代码
	……
	return xxx
## 15. 引入模块
当内置函数不满足需求时，可以导入相关的库
最重要的是Python有许多的第三方库，能够直接下载使用

## 16. 类的创建
class 类名:
	构造方法
	相关语句
示例代码如下：
```Python
class student :  
    def __init__(self,Name,No,Chinese,Math,English):  
        self.Name = Name  
        self.No = No  
        self.Chinese = Chinese  
        self.Math = Math  
        self.English = English  
    def sum(self):  
        return self.Chinese + self.Math + self.English  
  
stu1 = student('TTYYNX','123456',150,150,150)  
  
print(stu1.Name,stu1.No,stu1.Chinese,stu1.Math,stu1.English)  
print(stu1.sum())  
sum = stu1.sum()  
print(sum)
```
## 17. 类的继承
class 类名：
	构造方法
	super().父类构造方法
	相关语句
示例代码如下：
```Python
class emp:  
    def __init__(self,name,id):  
        self.name = name  
        self.id = id  
  
    def print_info(self):  
        print(self.name,self.id)  
  
  
class fullemp(emp):  
    def __init__(self,name,id,monsalary):  
        super().__init__(name,id)  
        self.monsalary = monsalary  
  
    def caculate_monsalary(self):  
        return self.monsalary * 1  
  
class partemp(emp):  
    def __init__(self,name,id,daily_salary,work_days):  
        super().__init__(name,id)  
        self.daily_salary = daily_salary  
        self.work_days = work_days  
    def caculate_monsalary(self):  
        return self.daily_salary * self.work_days  
  
emp1 = fullemp("陈","111",10000)  
  
emp2 = partemp("王","222",200,20)  
  
emp1.print_info()  
emp2.print_info()  
  
salary1 = emp1.caculate_monsalary()  
print(salary1)  
salary2 = emp2.caculate_monsalary()  
print(salary2)
```

## 18. 文件路径
绝对路径：指的是文件在电脑硬盘上的真实路径。例如``D:\Source Code\Pycharm\Python Learning\练习3.py``这就是一个绝对路径。即从系统盘符开始写，一直写到文件名称。

相对路径：指相对于当前目录的文件路径。``./``表示在当前目录下，``../``表示在当前目录的上一级目录，``../../``表示当前目录的上上级目录。例如``a.txt``文件在当前目录下，那么它的位置就可表示为``./a.txt``。若``b.txt``在当前目录的上级目录下，那它的位置就可以表示为``../b.txt``。

## 19. 文件操作
### 19.1. 打开文件
Python内置函数open。样式为:open(文件路径,打开方式，编码格式)。
其中编码格式除非指定，不然一般可省略。
打开方式的分类：
1、只读模式，用`r`表示。

2、写入模式，用`w`表示。

3、追加模式，用`a`表示。

4、可读可写模式，用`r+`,`w+`,`a+`表示。

可读可写三个模式的区别如下：
![](Pasted%20image%2020231113154320.png)
### 19.2. 读写操作
`读：`
Python内置函数read。样式为`文件名.read()`,会返回一个字符串。
Python内置函数readlines。样式为`文件名.readlines()`,会返回一个字符串列表。
`写：`
Python内置函数write。样式为`文件名.write(字符串参数)`。
Python内置函数writelines。样式为`文件名.writelines(字符串列表)`。

### 19.3. 关闭文件
Python内置函数close。样式为`文件名.close()`,会将该文件关闭，无法再进行读写。
另一种关闭方式：
```Python
with open(文件路径，打开方式) as 文件名:
	操作1
	操作2
	操作3
	……
```
在将缩进的所有操作完成后，文件会自动关闭。
### 19.4. 代码示例
```Python
with open("./a.txt","w+") as f1:  
   f1.write("123456789")  
  
with open("./a.txt","r+") as f1:  
   s = f1.read()  
   print(s)  
  
with open("./b.txt","w+",encoding="utf-8") as f2:  
    f2.writelines(["你好","Python","1234567"])  
  
with open("./b.txt","r+",encoding="utf-8") as f2:  
    arr = f2.readline()  
    for i in range(0,len(arr)):  
        print(arr[i])
```
## 20. 异常处理
```Python
try:
	代码段
except 异常类型:
	代码段
except:
	代码段
except Exception as e: # 这是一种常用写法
	print(repr(e)) # 输出异常信息
```
上述代码解释：若没发生异常，则不会运行except中的代码。若except后面有异常类型，那么只会捕捉那一种类型，若后面没有类型异常，则会捕获所有类型异常。既可以捕捉所有异常，又可以输出异常信息的代码如上。
示例代码：
```Python
while True:  
    try:  
        value = input("请输入一个整数:")  
        num = int(value)  
        print(num)  
        division = 10 / num  
        arr = [1,2]  
        print(arr[2])  
        break  
    except ValueError:  
        print("输入有误,请重新输入")  
    except ZeroDivisionError:  
        print("不能输入'0'! 请重新输入")  
    except Exception as e:          #捕获所有异常并输出异常信息  
        print(repr(e))  
        print("代码有误，请查看")  
        break
```
## 21. 测试
导入测试库 unittest
写一个测试类
在控制台写python -m unittest会运行全部测试案例
被测试类代码如下：
```Python
class shoppinglist:  
    def __init__(self,shoppinglist):  
        self.shoppinglist = shoppinglist  
  
    def get_item_count(self):  
        return len(self.shoppinglist)  
  
    def get_total_price(self):  
        total_price = 0  
        for price in self.shoppinglist.values():  
            total_price = total_price + price  
        return total_price
```
测试类代码如下:
```Python
from ShoppingList import shoppinglist  
import unittest  
  
class TestShoppingList(unittest.TestCase):  
    def setUp(self):  
        self.ShoppingList = shoppinglist({"1":8,"2":6,"3":10})  
    def test_get_item_count(self):  
        self.assertEqual(self.ShoppingList.get_item_count(),3)  
  
    def test_get_total_price(self):  
        self.assertEqual(self.ShoppingList.get_total_price(),24)
```

