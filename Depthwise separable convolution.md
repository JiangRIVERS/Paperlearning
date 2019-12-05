可分离卷积是对卷积的一种改进，减少了参数的数量，同时实验证明效果并不比卷积差。
整体的思想个人认为类似于Xception
举例说明：
对于一个CxHxW的feature map进行3x3的卷积，卷积后的channel数设定为C1
1. 正常卷积：
使用C1个Cx3x3 kernal size进行卷积
参数量：C1xCx3x3
2. Depthwise separable convolution
使用1个Cx3x3 kernal size进行卷积，进而使用C1个Cx1x1 kernal size对经过3x3卷积后的新feature map进行卷积
参数量：Cx3x3+C1xCx1x1

当C=3，C1=256时对比：
正常卷积参数量：256x3x3x3=6912
Depthwise separable convolution：3x3x3+256x3x1x1=795