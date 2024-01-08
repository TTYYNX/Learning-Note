分别下载并安装VScode, TexLive

VScode下载与安装：[链接](https://code.visualstudio.com/)

TexLive下载（清华大学镜像）：[链接](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)

TexLive安装教程：[链接](https://www.bilibili.com/video/BV16b411o7gS/?spm_id_from=333.788.recommend_more_video.-1&vd_source=7664b55184fd63da03a03ef6c9be4310)

VScode安装插件：LaTex language support, LaTex Workshop

安装完毕后开始使用，创建临时文件temp.tex, 输入以下内容：

```Latex
\documentclass[UTF8]{ctexart}
    \title{文章标题}
    \author{David}
    \date{\today}
    \begin{document}
    \maketitle
    This is the context of the article.
\end{document}
```

然后按Ctrl+S 完成编译加保存功能。

查看PDF：

VSCode左侧工具栏选择 _TEX_-View LaTex PDF-View in VScode Tab后，右侧就会出现PDF,每次修改后，按Ctrl+S, 右边PDF会进行实时编译。

常用的便捷网站：
![](Pasted%20image%2020231218153656.png)

Latex模板的下载与使用：[链接](https://blog.csdn.net/MacWx/article/details/128414122?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522170288946616800185812016%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=170288946616800185812016&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-128414122-null-null.nonecase&utm_term=%E6%A8%A1%E6%9D%BF&spm=1018.2226.3001.4450)

vscode+latex环境搭建：[链接](https://blog.csdn.net/RZLu2000/article/details/122570686)