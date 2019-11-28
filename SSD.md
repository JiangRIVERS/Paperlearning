##SSD

This paper presents the first deep network based object detector that does not resample pixels or features for bounding box hypotheses and is as accurate as approaches that do.

###基本思想：
无需预先提出RP，网络直接预测输出物体的类别概率和位置坐标，即我们的网络是统一的网络，经过单次检测即可直接得到最终的检测结果，俗称(one-stage检测)。

SSD特征提取网络没有FC层
在6个特征图上进行RP，成为==(密集采样)==

bounding box概念：网络预测结果。bounding box 中心点坐标（x',y',h',w'）分别表示中心点坐标以及bounding box 的高和宽。

ground-truth 中心点坐标为(x,y,h,w),训练使得(a1,a2,a3,a4)(x',y',h',w')+(b1,b2,b3,b4)=(x,y,h,w).

bounding box 回归

通过KKT条件构建分类和回归的损失函数。

RP（Region propose）框指的是网络输出的预测值（IOU大于某一阈值的部分），bounding boxes指的是经过边框回归后修正的RP框