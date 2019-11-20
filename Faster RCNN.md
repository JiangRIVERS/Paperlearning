##Faster RCNN

###Title: Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks

Faster R-CNN是一个end-to-end模型，one-stage。

###RPN(Region Proposal Networks)：在feature-map上提取RP的方法
在conv5的feature map上用3x3卷积核进行卷积，再进行2次fc layer，每个点对应输出2k个scores以及4k个coordinates。k对应原图上k个anchor框。socres用于判断前景或背景类，前景类输入SPP-Net进行分类，coordinates用于regression。

<img src="https://img-blog.csdn.net/20160531141411874?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" width="60%">

在训练过程中，RPN的训练和Fast R-CNN交替训练，损失函数由四个小损失函数（共两个大损失函数构成），当loss小于某一threshold，停止网络训练。

在测试过程中先进行RPN，再进行SPPnet(Fast R-CNN)，Cascade方式联合。

<img src="https://img-blog.csdn.net/20180818153028492?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21kanh5NjM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="60%">



Faster R-CNN流程

<img src="https://img-blog.csdn.net/20180304220940218" width="90%">