## RetinaNet

###Titile:Focal Loss for Dense Object Detection

提出Focal Loss，解决了但阶段物体检测器中，正负样本数量和分类难易程度极度不平衡引起的损失值被大量容易分类的负样本损失炎魔的问题。（例子：10000个易分的负样本损失值为0.1，100个不易分的正样本损失为1，总损失为10000x0.1+100x1，正样本的损失被负样本的损失所淹没。）

单目标检测框架：RetinaNet(ResNet+FPN+FCN)

###Related Work
1. Cross-Entropy Loss：在但阶段物体检测器中，它会被大量的容易分类的样本控制，导致少量的不容易分类的样本被淹没。
pt=p if y==1 else (1-p)
In the above y ∈ {±1} specifies the ground-truth class and p ∈ [0, 1] is the model’s estimated probability for the class with label y = 1.
CE(pt)=-log(pt)

2. Balanced CE Loss：对正样本的损失值使用权重因子ɑ ∈ [0,1]，对负样本使用权重因子1-ɑ，从数量角度平衡了正负样本的损失值。
CE(pt)=-ɑtlog(pt)。

###Focal Loss
Balanced CE Loss虽然人为设计了正负样本损失的权重，加大正样本的权重，减少负样本的权重。然而在正样本中仍然可能存在较易分的物体，负样本中仍可能存在较难分类的物体。
于是作者提出Focal Loss，基于分类难易程度来分配权重。
Focal Loss降低了容易分类样本的权重，从而使损失更关注在难分类的样本上。