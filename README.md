Colaboratory 免费GPU服务器使用教程
==================================

    RSIDEA 刘寅贺 2019.4.30
<br>

近日，Google Colab 官方在Twitter上表示，将为用户提供免费的[Tesla T4](https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/t4-tensor-core-datasheet-951643.pdf) GPU（16 GB显存，2560个CUDA核心，8.1 TFLOPS）。随着组内越来越多的同学开始研究深度学习的方法，若能使用Colab可在一定程度上缓解组内计算资源紧张的情况。同时在虚拟机上还预装了大多数需要用到的库（TensorFlow,Keras, Pytorch,GDAL……），对新人来说也省去了配置环境的时间，可以直接开搞。并且与[GEE](https://earthengine.google.com/)的导出数据共用Google Drive的存储，如果能将两大杀器结合可能会有1+1\>2的效果。因此写了这个十分粗略的教程帮大家快速地薅到资本主义羊毛。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/0.png"  width = 40% height = 40% style="float: right">


准备工作
--------

适用人群：

1.  所用训练集不是特别大（数G以内）。

2.  数据不存在**涉密**、有版权等不宜公开的问题。
<br>

自行准备：

1. Google账号。

2. 翻墙工具，实在没有可以找我用本人搭的代理。
<br>

Colab配置：

1.  进入Google
    Drive（<https://drive.google.com/drive/my-drive>），所有Google用户应该都会开通Google
    Drive，若第一次使用让勾选隐私协议之类的一路同意即可。

2.  通过Colab新建一个ipynb文件，现在可能会默认添加了Colab，若更多里没有Colab请参照第3步。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/2.png"  width = 50% height = 50% style="float: right">

3.  已有Colab请略过此步。

    选择“更多”中“关联更多应用”，搜索并安装Colab，重复步骤2，此处不多赘述。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/3.png"  width = 50% height = 50% style="float: right">

4.  进入该界面表示Colab正常工作。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/4.png"  width = 100% height = 100% style="float: right">

5.  在“修改”内“笔记本设置”中将运行时类型设置为Python3，硬件加速器改为GPU。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/5.png"  width = 60% height = 60% style="float: right">

6.  运行`!nvidia-smi`（运行ubuntu命令时只需在前面加上！），若能出现图中结果，说明你成功薅到了资本主义羊毛。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/6.png"  width = 60% height = 60% style="float: right">

云端训练
--------

1.  将数据集上传到Google
    Drive上，这一步是GEE用户的福利，可以跳过。据我测试上传数据集的速度十分感人，尤其当文件个数比较多的情况下更是慢得过分，强烈建议上传单个压缩文件，然后使用CloudConvert解压。首次使用CloudConvert还要注册、提供访问权限，在此不多赘述。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/7.png"  width = 60% height = 60% style="float: right">
<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/8.png"  width = 60% height = 60% style="float: right">
<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/9.png"  width = 60% height = 60% style="float: right">

2.  为了访问google drive上的数据集，运行下面两行代码：

>   from google.colab import drive

>   drive.mount('/Drive')

3.  点击出现的链接，一路下一步，将授权码输入到框内回车。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/10.png"  width = 100% height = 100% style="float: right">
<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/11.png"  width = 100% height = 100% style="float: right">
<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/12.png"  width = 100% height = 100% style="float: right">

4.  出现图中结果表明google
    drive挂载成功，在左边文件里可以看到云盘的文件夹，对该文件夹的读写相当于直接对云盘内的文件进行操作。需要注意的是，想要访问该文件夹还需要先执行`cd..`命令。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/13.png"  width = 60% height = 60% style="float: right">

5.  接下来怎么利用好这块卡就各凭本事啦。 上述过程可参考该[例子](https://github.com/SilverSulfide/Colab-Tutorial/blob/master/examples/train.ipynb)。若已有实现好的代码，直接上传至Google Drive中用python命令运行即可。
>   cd ..    
>   ! python file.py

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/14.png"  width = 50% height = 50% style="float: right">

注意事项
--------

理论上Colab会毙掉一些长时间运行的虚拟机，注意保存。不过目前还没有遇到过这个问题，实测连续训练7小时没有任何问题。注意：Google
Drive的挂载有12小时限制，到时间需要重新挂载。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/15.png"  width = 100% height = 100% style="float: right">

理论上关闭浏览器代码依旧会在虚拟机中运行，并且据我测试确实是这样，可以比较放心地挂机。但还是不太建议，因为虽然目前还没有没有遇到过，但是如果长时间没有Colab所希望的“交互”，进程可能还是会被杀掉。

<img src="https://github.com/SilverSulfide/Colab-Tutorial/blob/master/figures/16.png"  width = 80% height = 80% style="float: right">
