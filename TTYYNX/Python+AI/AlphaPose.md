# 配置环境
python环境要和numpy一致，torch三个包的环境版本要一致，PyYAML版本也要一致，matpilot也要版本一致
## 1. 安装cuda和cudann
参考[链接](https://blog.csdn.net/anmin8888/article/details/127910084)
## 2. 下载代码到本地调试
参考[链接](https://blog.csdn.net/qq_43694194/article/details/129910937)

## 3. 装gpu版本的pytorch
去官网找对应版本   然后去网站下载    虚拟环境路径进入下载的文件夹中     然后输入pip install+下载的文件名即可
下载gpu版本网址[链接](https://download.pytorch.org/whl/torch_stable.html)
下载版本对应网址[链接](https://pytorch.org/get-started/previous-versions/)

## 4. conda升级python版本
解决[链接](https://blog.csdn.net/ximaiyao1984/article/details/134809675?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-134809675-blog-88238427.235%5Ev43%5Epc_blog_bottom_relevance_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-134809675-blog-88238427.235%5Ev43%5Epc_blog_bottom_relevance_base3&utm_relevant_index=5)
# 报错问题
## 1. requirements.txt文件不存在
解决方法：
```
方式一：
首先 pip freeze > requirements.txt
再运行 pip install -r requirements.txt

方式二：
检查文件路径命名规范

方式三：
pip install -r requirements.txt的绝对路径，关闭代理
```
## 2. pip下载文件很慢
解决方法：
[国内镜像](https://blog.csdn.net/u013013797/article/details/107444659?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-107444659-blog-135396964.235%5Ev43%5Epc_blog_bottom_relevance_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-107444659-blog-135396964.235%5Ev43%5Epc_blog_bottom_relevance_base3&utm_relevant_index=2)非常多，换一个地址下载，记得关闭代理
```
示例代码：
pip install -r D:\Source_Code\Pycharm\AlphaPose\trackers\PoseFlow\requirements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```
## 3. 下载cython_bbox包失败
解决办法：
1、先安装cython
2、安装生成工具，[链接](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/)
![](Pasted%20image%2020240224162751.png)
下载相关内容，大概6.7G，bug解决

## 4. 安装gpu版本的 torchaudio失败
解决方案：
1、先安装对应版本的cpu版本
```
pip install torchaudio==xxx
```
2、再去安装对应版本的gpu版本，提前下载好
```
命令行进入下载好的目录，输入命令 pip install torchaudio-xxxxx版本号.whl
```
## 5. No module named 'cv2.cv2'
解决方案：
```
pip uninstall opencv-python
pip install opencv-python
```
## 6. ModuleNotFoundError: No module named numpy.core._multiarray_umath
解决方法：
```
pip install numpy --upgrade  python版本记得要对应  提前去查
```

## 7. ImportError: cannot import name 'MutableMapping' from 'collections'
解决方法：
```python
from collections.abc import MutableMapping
```

## 8. cannot import name '_path' from 'matplotlib'
解决方法：重装matplotlib

## 9. ModuleNotFoundError: No module named 'kiwisolver._cext'
解决方法：重装kiwisolver

## 10. ImportError: cannot import name '_ccallback_c' from 'scipy._lib' 
解决方法：重装scipy

## 11. No module named 'cython_bbox'
解决方法：[链接](https://stackoverflow.com/questions/46721713/importerror-cannot-import-name-ccallback-c)需科学上网

## 12. ImportError: Failed to load PyTorch C extensions:
解决方法：重装pytorch套件  版本记得对应

## 13. ERROR: Could not find a version that satisfies the requirement torch==2.1.1+cu118 (from torchvision) (from versions: 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0, 1.13.1, 2.0.0, 2.0.1, 2.1.0, 2.1.1, 2.1.2, 2.2.0, 2.2.1)
ERROR: No matching distribution found for torch==2.1.1+cu118
类似这样的错误解决方法：
1、关代理
2、试一试在下载的目录下运行以下类似的命令
```python
pip install torchvision-0.16.1+cu121-cp38-cp38-win_amd64.whl   一定要在那个文件夹下运行
```
3、或者以下方法
```python
pip install torchvision-0.16.1+cu118-cp38-cp38-win_amd64.whl -f https://download.pytorch.org/whl/torch_stable.html
```
版本不一定一致  但是方法一致

## 14. 找不到路径
解决方法：
看路径文件是否正确，文件是否在同一层级