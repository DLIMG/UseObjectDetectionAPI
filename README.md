# UseObjectDetectionAPI
快速使用TensorFlow Object Detection API

## 前言
由于每次使用Object Detection API都会出现一些问题，耗费大量时间，觉得有必要仔细的记录一下配置过程。

## 环境
Windows10
TensorFlow1.12
Python3.6

## 说明
在配置前有一些说明。  
1.默认你已经安装好Anaconda;  
2.Object Detection API版本最好与你安装的TF版本对应，否则可能会出现bug;  
3.Python3.7对应Tensorflow最低的版本是1.13，本文中选择Python3.6。

## 配置流程
### 1.为了环境干净，Anaconda新建一个虚拟环境  
若网络受限，可切换至国内源创建；  
`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`  
`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/`  
`conda config --set show_channel_urls yes`  
`conda create -n Tensorflow1.12 python=3.6 ` 

### 2.安装Tensorflow1.12  
这里你同样可以使用国内源；  
`pip install tensorflow==1.12 -i https://pypi.tuna.tsinghua.edu.cn/simple`  
若你需要安装GPU版的，那就用conda装吧，甚至都不用配置cuda、cudnn这些；  
`conda install tensorflow-gpu==1.12`  

### 3.下载[Object Detection API](https://github.com/tensorflow/models)代码  
这里需要注意的是，需要选择一下版本。  
![](https://i.imgur.com/RvTyVfc.png)  
前面安装了tensorflow1.12，这里对应安装r1.12.0版本的就好。  
国内下载很慢，可以在我的[百度云](https://pan.baidu.com/s/1oGEjSt3j1vFm6bSf8CnIGA)中下载。（用代理下载也花了好久==！）  
提取码：79td  

### 4.将源码导入Anaconda的环境中  
a.打开压缩包，找到research文件，我们所需要的Object Detection的源码就在其中；  
![](https://i.imgur.com/6U3gveS.png)  
b.将research文件解压到 （你的路径）/Anaconda/env/Tensorflow1.12/Lib/site-packages 下；  
![](https://i.imgur.com/FvsbfAh.png)  

### 5.编译proto文件
a.到[GitHub](https://github.com/protocolbuffers/protobuf/releases/tag/v3.4.0)下载protobuf包：  
![](https://i.imgur.com/Bq0sh5w.png)  
b.下载完后，将压缩包内的bin/protoc.exe 文件放入research/ 目录下；  
c.在research/ 目录下打开powershell，执行如下命令：  
`.\protoc.exe .\object_detection\protos\*.proto --python_out=.`  
编译成功不会显示其他信息，进入（\research\object_detection\protos）目录，发现所有.proto文件已被编译为.py文件。  
![](https://i.imgur.com/ii1neyD.png)  
  
### 6.装载research模块
a.cmd中进入Tensorflow1.12虚拟环境;  
`conda activate Tensorflow1.12`  
b.进入到research 下执行：
`python setup.py install`  
装载过程中会出现很多安装信息，最后出现：  
![](https://i.imgur.com/ljc7BbY.png)  
完成装载，装载过程中可能会出现缺少Cython这些问题，需要什么包pip安装就好。  
  
### 7.添加slim环境变量
在（\Anaconda\envs\Tensorflow1.12\Lib\site-packages）目录下新建文本文档，输入：
![](https://i.imgur.com/rv3MEPr.png)  
保存并重命名为tensorflow_model.pth，如图所示：  
![](https://i.imgur.com/gQcG3u6.png)  
  
### 8.Test Object Detection API
打开虚拟环境，转到（\research）目录下，输入命令：
`python object_detection/builders/model_builder_test.py`  
如图所示，安装成功：  
![](https://i.imgur.com/DGngFsJ.png)  
  
### 9.运行Demo
在Tensorflow1.12虚拟环境中运行Demo.py即可，运行过程中可能会缺少某个安装包，缺什么用pip install相应的安装包即可。  
运行过程中需要下载预训练模型，和加载相应的配置文件。由于资源来自于github，下载可能会限速，这里提供我的[ssd_mobilenet_v1_coco_2017_11_17](https://pan.baidu.com/s/1cPndOpT9palYBqrkgwonmA)下载。  
提取码：mol9  
相应的配置文件来自于research/object_detection文件夹下的data文件夹，测试图片可以将research/object_detection文件夹下的test_image文件夹复制过来，整理完后文件如下：  
![](https://i.imgur.com/u8K5KCg.png)    
运行Demo.py结果：  
![](https://i.imgur.com/wWHR1Oe.png)  
运行DetectInVideos.py结果：  
![](https://github.com/DLIMG/UseObjectDetectionAPI/blob/master/ShowImage/show1.png)
