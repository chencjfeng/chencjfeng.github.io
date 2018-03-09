---
title: Python批量生成二维码
date: 2017-11-04 14:54:31
author: "chenJF"
tags:
    - Python
archives: Python
---
# Python2.7 批量生成二维

## 导语：
> 本文针对mac电脑利用Python2.7脚本批量生成二维码，由于Python生成二维码利用了qrcode和image库，需要先用pip安装这两个库。这里顺便说了下pip的安装。


### 1.pip的安装
* 用命令行安装pip
~~~
sudo easy_install pip
~~~
* 检查是否安装成功，只要不是not found pip，则安装成功
~~~
pip help
~~~
<br>
### 2.安装qrcode和image库
* 安装命令
~~~
#安装失败可以加sudo安装
pip install qrcode
pip install image
~~~
* 检查是否安装成功,安装成功会有相应的版本信息
~~~
pip show qrcode
pip show image
~~~
* 安装成功显示界面信息

* ![python-qrcode.png](http://upload-images.jianshu.io/upload_images/4970496-ce568913bd5e15a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<br>
### 3.示例代码
~~~
# 导入qrcode库
import qrcode

#生成一张二维码图片，url二维码的内容，name保存二维码图片的名字
def createOneQR(url,name):
qr=qrcode.QRCode(version = 2,
error_correction = qrcode.constants.ERROR_CORRECT_L, #容错样式
box_size=10,   #每个格子的像素
border=1)      #边框宽度
qr.add_data(url)
qr.make(fit=True)
img = qr.make_image()
img.resize((140, 140)).save(name)   #保存为140*140的图片


#根据文档批量生成二维码
def getQR():
num = 0
#遍历文档每行内容生成二维码
for line in open("license-for-card.txt"):
imageName = "license"+str(num)+".png"
createOneQR(line,imageName)
num += 1

getQR()
~~~

* 参数 version 表示生成二维码的尺寸大小，取值范围是 1 至 40，最小尺寸 1 会生成 21 * 21 的二维码，version 每增加 1，生成的二维码就会添加 4 尺寸，例如 version 是 2，则生成 25 * 25 的二维码。

* 参数 error_correction 指定二维码的容错系数，分别有以下4个系数：
* ERROR_CORRECT_L: 7%的字码可被容错
* ERROR_CORRECT_M: 15%的字码可被容错
* ERROR_CORRECT_Q: 25%的字码可被容错
* ERROR_CORRECT_H: 30%的字码可被容错
* 参数 box_size 表示二维码里每个格子的像素大小。
* 参数 border 表示边框的格子厚度是多少（默认是4）。
