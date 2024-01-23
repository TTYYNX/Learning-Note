# 环境配置
## 1. yolo源码地址[链接](https://github.com/ultralytics)

## 2. 下载
``1、配置pytorch环境。
``2、若作者提供requirements文件
- 配置相关的库。
```python
install -r requirements.txt
```
``3、若作者没有提供requirements文件
- 根据运行报错信息，搜索，手动安装相关库。
# 相关报错
``解决报错 fatal: Not a git repository
```git
在该文件夹内打开git bash 输入 git init
```
``解决报错  AttributeError: Cant get attribute SPPF on module models.common
- model/ common.py添加如下代码
```python
import warnings

class SPPF(nn.Module):
    # Spatial Pyramid Pooling - Fast (SPPF) layer for YOLOv5 by Glenn Jocher
    def __init__(self, c1, c2, k=5):  # equivalent to SPP(k=(5, 9, 13))
        super().__init__()
        c_ = c1 // 2  # hidden channels
        self.cv1 = Conv(c1, c_, 1, 1)
        self.cv2 = Conv(c_ * 4, c2, 1, 1)
        self.m = nn.MaxPool2d(kernel_size=k, stride=1, padding=k // 2)
 
    def forward(self, x):
        x = self.cv1(x)
        with warnings.catch_warnings():
            warnings.simplefilter('ignore')  # suppress torch 1.9.0 max_pool2d() warning
            y1 = self.m(x)
            y2 = self.m(y1)
            return self.cv2(torch.cat([x, y1, y2, self.m(y2)], 1))
```
``解决报错 RuntimeError: The size of tensor a (80) must match the size of tensor b (56) at non-singleton``
- 这是由于用了版本5.1，需要替换成6.1的，下载V6.1的版本[点击下载](v5.0/https://github.com/ultralytics/yolov5/releases/download/yolov5s.pt)  
下载好之后替换原来的yolov5s。
``解决 UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument.``
- 地址[链接](https://blog.csdn.net/qq_43742820/article/details/126747455)
# 好用工具
``视频图片下载``
lux 、you-get、yt-dlp
ffmpeg配置[链接](https://blog.csdn.net/csdn_yudong/article/details/129182648)

# yt-dlp
```
yt-dlp --cookies-from-browser chrome "URL" -f bestvideo+bestaudio
```
