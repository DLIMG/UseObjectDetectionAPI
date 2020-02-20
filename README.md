# UseObjectDetectionAPI
快速使用TensorFlow Object Detection API

# 前言
由于每次使用Object Detection API都会出现一些问题，耗费大量时间，觉得有必要仔细的记录一下配置过程。

# 环境
Windows10
TensorFlow1.12
Python3.6

# 说明
在配置前有一些说明。
1.默认你已经安装好Anaconda;
2.Object Detection API版本最好与你安装的TF版本对应，否则可能会出现bug;
3.Python3.7对应Tensorflow最低的版本是1.13。

# 配置流程
1.为了环境干净，Anaconda新建一个虚拟环境； 
若网络受限，可切换至国内源； 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ 
conda config --set show_channel_urls yes 
conda create -n Tensorflow1.12 python=3.6 

2.安装Tensorflow1.12； 
这里你同样可以使用国内源； 
pip install tensorflow==1.12 -i https://pypi.tuna.tsinghua.edu.cn/simple 
若你需要安装GPU版的，那就用conda装吧，甚至都不用配置cuda、cudnn这些； 
conda install tensorflow-gpu==1.12 

3.下载Object Detection API代码； 
https://github.com/tensorflow/models 
这里需要注意的是，你需要选择一下版本。 
