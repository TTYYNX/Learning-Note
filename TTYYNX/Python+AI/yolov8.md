参考教学[链接](https://www.bilibili.com/video/BV13V4y1S7MK/?spm_id_from=333.999.0.0)
# Aconda环境
## 1. 新建一个yolov8的环境
```
create -n yolov8 python=版本号
```
## 2. 安装Pytorch
```
去pytorch官网找寻对应版本（看显卡组件），用命令一键安装
```
## 3. 安装yolo环境
```
在终端进入解压后的yolov8文件夹，输入pip install -e .
```
## 4. 检测测试
```python
yolo predict model=yolov8n.pt source=ultralytics/assets/bus.jpg
```
# 报错解决
## 1. 出现No module named 'ultralytics.utils等类似情况
```Python
pip install --upgrade ultralytics  # 更新ultralytics包
```