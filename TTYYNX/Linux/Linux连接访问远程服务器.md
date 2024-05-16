1、安装SSH
```linux
sudo apt-get install openssh-server
```
2、开启SSH服务
```linux
service sshd start
```
3、检查SSH是否启动
```linux
sudo ps –e |grep ssh
```
4、连接
```linux
ssh -p xx username@ip   # xx为端口号
```
# ubuntu虚拟机共享主机VPN
参考[链接1](https://www.jianshu.com/p/6c7abd4adc9b)
参考[链接2](https://www.wenpblog.com/info/138.html)
总结：
1、打开上网工具的局域网连接
2、ipconfig本机ip地址
3、去linux系统内的设置主机ip和局域网端口即可

# 使用Putty+Xming登录远程服务器Linux图形化界面
参考[链接](https://blog.csdn.net/Yinyaowei/article/details/108303562?spm=1001.2101.3001.6650.6&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-6-108303562-blog-106989473.235%5Ev43%5Epc_blog_bottom_relevance_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-6-108303562-blog-106989473.235%5Ev43%5Epc_blog_bottom_relevance_base3&utm_relevant_index=8)

# Linux 环境安装anaconda环境
参考[链接](https://blog.csdn.net/wyf2017/article/details/118676765)
安装完后进入退出指令
```linux
conda activate 环境名  # 进入conda环境
conda deactivate  # 推出conda环境
```

# Linux装cuda和cudnn的方法
参考[链接1](https://blog.csdn.net/qq_44961869/article/details/115954258)
参考[链接2](https://juejin.cn/s/cudnn%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B%20linux)
cuda和cudnn要版本对应一致

# Ubuntu下CUDA的卸载以及安装
参考[链接](https://blog.csdn.net/m0_37605642/article/details/119637836)

# Ubuntu下配置环境相关问题
有时的包报错可能是版本问题，换一个版本装即可。

# linux服务器如何指定gpu以及用量
参考[链接](https://blog.csdn.net/alxe_made/article/details/80471739)

# linux出现opencv视频不能解析的问题
换一个opencv-python版本