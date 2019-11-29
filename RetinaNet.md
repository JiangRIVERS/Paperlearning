## RetinaNet

###Titile:Focal Loss for Dense Object Detection

提出Focal Loss，解决了但阶段物体检测器中，正负样本数量和分类难易程度极度不平衡引起的损失值被大量容易分类的负样本损失炎魔的问题。（例子：10000个易分的负样本损失值为0.1，100个不易分的正样本损失为1，总损失为10000x0.1+100x1，正样本的损失被负样本的损失所淹没。）

单目标检测框架：RetinaNet(ResNet+FPN+FCN)