Colaboratory 免费GPU服务器使用教程
==================================

刘寅贺 2019.4.27

近日，Google Colab 官方在Twitter上表示，将为用户提供免费的Tesla T4 GPU（16 GB
显存，2560个CUDA核心，8.1
TFLOPS）。随着组内越来越多的同学开始研究深度学习的方法，若能使用Colab可以一定程度上缓解组内计算资源紧张的情况。同时在虚拟机上还预装了大多数需要用到的库（TensorFlow,
Keras, Pytorch,
GDAL……），对新人来说也省去了配置环境的时间，可以直接开搞。并且与GEE的导出数据共用Google
Drive的存储，如果能将两大杀器结合可能会有1+1\>2的效果。因此写了这个十分粗略的教程帮大家快速地薅到资本主义羊毛。

![](media/a6f2cb2cefddb20d943cf0a087270552.png)

准备工作
--------

适用人群：

1.  所用训练集不是特别大（数G以内）。

2.  数据不存在**涉密**、有版权等不宜公开的问题。

自行准备：

1.  Google账号。

2.  翻墙工具，实在没有可以找我用本人搭的代理。

3.  进入Google
    Drive（<https://drive.google.com/drive/my-drive>），所有Google用户应该都会开通Google
    Drive，若第一次使用让勾选隐私协议之类的一路同意即可。

4.  通过Colab新建一个ipynb文件，现在可能会默认添加了Colab，若更多里没有Colab请参照第3步。

![](media/e22bec20afd87350fa459fa3b87d9826.png)

![](media/a8dd894f2bb5b87844927d3d91747c91.png)

1.  已有Colab请略过此步。

    选择“更多”中“关联更多应用”，搜索并安装Colab，重复步骤2，此处不多赘述。

![](media/5f157247d3d1890ad764edb8eea1aeac.png)

![](media/4c7b2bfc05ba2801f11a7b6b4785d6c6.png)

2.  进入该界面表示Colab正常工作。

![](media/4ccac37e52e1e51be514b45f8f271be5.png)

3.  在“修改”内“笔记本设置”中将运行时类型设置为Python3，硬件加速器改为GPU。

![](media/57fa0f9e891f5418b7356c015aaf42ec.png)

![](media/59585186514a0d2379b4a3aee6d86998.png)

4.  运行 “ !nvidia-smi
    ”（运行ubuntu命令时要在前面加上！），若能出现图中结果，说明你成功薅到了资本主义羊毛。

![](media/cd62fc02dcbc637b28bb4f0ccf0b3566.png)

云端训练
--------

1.  将数据集上传到Google
    Drive上，这一步是GEE用户的福利，可以跳过。据我测试上传数据集的速度十分感人，尤其当文件个数比较多的情况下更是慢得过分，强烈建议上传单个压缩文件，然后使用CloudConvert解压。首次使用CloudConvert还要注册、提供访问权限，在此不多赘述。

![](media/d16bdb44d18bcf1b154fb43deec03bbb.png)

![](media/5d4565b855b3385ef0f4aa54c160f5cf.png)

![](media/23c613c762016c8a238b3ac883a70757.png)

2.  为了访问google drive上的数据集，运行下面两行代码：

>   from google.colab import drive

>   drive.mount('/Drive')

3.  点击出现的链接，一路下一步，将授权码输入到框内回车。

![](media/52fc4de14b7b7f1219b0909acee10683.png)

![](media/729c787c38bea838abdbe1f7cc1d4105.png)

![](media/c4b86b34c7349c66469a9070527ea03f.png)

![](media/187fbcf1dfb4fb91587dbc503bbaec0a.png)

![](media/677ab1fe9837f38646b1787386173ba2.png)

4.  出现图中结果表明google
    drive挂载成功，在左边文件里可以看到云盘的文件夹，对该文件夹的读写会直接影响到云盘内的文件。需要注意的是，想要访问该文件夹还需要先执行‘cd
    ..’命令。

![](media/0791304843ecc1f09b16627032bb63b7.png)

![](media/a57cb6a31b24f64d046d67ba7bea85f6.png)

![](media/507e3b2dc089f8a76a2ba0af9971f837.png)

5.  接下来怎么利用好这块卡就各凭本事啦。若已有实现好的代码，直接上传至Google Drive中用python命令运行即可。
>   cd ..    
>   ! python file.py

![](media/449ea3adaebad7b20d7176498e2c5501.png)

注意事项
--------

理论上Colab会毙掉一些长时间运行的虚拟机，注意保存。不过目前还没有遇到过这个问题，实测连续训练7小时没有任何问题。注意：Google
Drive的挂载有12小时限制，到时间需要重新挂载。

![](media/5d26e62d4d24dafbe1baf8f3cd09d305.png)

理论上关闭浏览器代码依旧会在虚拟机中运行，并且据我测试确实是这样，可以比较放心地挂机。但还是不太建议，因为虽然目前还没有没有遇到过，但是如果长时间没有Colab所希望的“交互”，进程可能还是会被杀掉。

![](media/21d3b20869a9e3383e4381ea6b47aa5e.png)
