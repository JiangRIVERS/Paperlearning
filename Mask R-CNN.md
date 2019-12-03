## Mask R-CNN
### Titile: Mask R-CNN

Mask R-CNN=Faster R-CNN + 分支网络

Mask branch 是对每个ROI使用一个small FCN
### Construction
<img src="http://jermmy.xyz/images/2019-4-12/mask-rcnn.png" width="100%">
### Innovation
+ 提出 ROIAlingn，优化了ROI池化，可以保留精准的空间位置。
+ 设计了Mask的loss，消除了类内竞争。 同时实现分割任务。
### 具体结构
分为Backbone和head两个sections
1. Backbone: ResNet-FPN+RPN
+ 采用ResNet形式的FPN提取feature map
+ 采用RPN提取ROI
2. head
+ 在head中有两个大branch
  + branch1类似fast R-CNN
  + branch2采用ROI Align+FCN获取mask，branch1提取的类别信息用于指导mask loss
### ROI Align
1. 提出问题
传统的ROI pooling由于存在两次取整操作导致feature map与原始图像mis-alignment，对于目标检测这种mis-alignment影响不大，但是由于分割是pixel-to-pixel，所以mis-alignment影响较大。这也是pytorch在分割任务中maxpooling参数ceil_mode==True的原因（个人观点）

<img src="https://pic4.zhimg.com/v2-e55e66c9c21136efa62beacfcb02f9ef_b.gif" width="80%">
如图所示，在feature map上选取ROI以及进行Pooling时，均存在取整操作。

2. 提出ROI Align
取缔取整操作，使用双线性插值获得相应位置的像素值。

<img src="http://jermmy.xyz/images/2019-4-12/roi-align.jpg" width="100%">
背景为feature map，黑实线区域是一个ROI，每个小框内蓝色点为采样点，本图中一个小框中有四个采样点。四个点的均值或最大值为这个小框的像素值。每个采样点的像素值由周围四个feature map上点双线性插值得到。该图本人认为存在不严谨，选取的用于进行双线性插值的feature map上的点应该在每个正方形背景小框中心，而非边角。但可以进行直观理解。该图并非论文中图，论文中没有图，是本人看各个blog中选取的一张。
作者将采样点设为4得到最佳性能，直接设为1性能也相差无几。
### Loss
在原文中，作者提到Loss=Loss(cls)+Loss(box)+Loss(mask)
前两项是Fast R-CNN中loss，用于分类和边框回归。
+ Loss(mask)

<img src="http://jermmy.xyz/images/2019-4-12/softmax.jpg" width="80%">
上图是传统分割任务的Loss: softmax+CE(或BCE)
由于分类任务会将该ROI识别为A类，分类的Loss只有A类的Loss。但是该ROI中可能不止存在A类，同时还存在B类，这时分割的Loss就包含A、B两类的Loss，造成类内竞争。
直观的来讲，分类任务告诉网络ROI是个车，但是分割任务告诉网络这个ROI既有车又有飞机，造成干扰，表现为梯度收敛存在问题。

<img src="http://jermmy.xyz/images/2019-4-12/sigmoid.jpg" width="80%">
作者认为，消除类内竞争就应该在分割时只对positive的物体进行分割。
具体表现为：ROI经过FCN后，网络得到一个KxMxM的feature map，K为类别数。分类网络得到结果该ROI属于第N类，在mask loss（也就是分割Loss）时，只计算第N类与其对应的GT图的Loss，不计算其余类的Loss。Loss采用BCE，计算Loss之前进行Sigmoid非线性函数。


