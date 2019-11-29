## YOLO V1

### Title: You Only Look Once: Unified, Real-Time Object Detection 

### Abstract 部分
1. 将物体检测看做一个回归问题
2. 整个检测流程是一个单一网络
3. 速度快
4. 有较多的定位误差，但假阳性（将背景检测为物体）目标较少
5. YOLO可以学习物体通用的表示特征 
6. YOLO假阳性少且泛化能力强均源于其利用了整张图的信息
7. 精度与sota比不高且对小物体不友好。

### 目标检测评价标准
True Positive(TP):IOU>=阈值
False Positive(FP):IOU<阈值
False Negative(FN):未被检测到的GT
True Negative(TN):忽略不计

Precision=TP/(TP+FP)=TP/all detections
Recall=TP/(TP+FN)=TP/all ground truths

map平均准确率:多个类别的ap值

### YOLO算法流程(将检测过程视为回归问题)
1. Resize image to 448x448
2. Run convolutional network
3. NMS
### YOLO算法思想
1. 将图片隐式的分为SxS个网格

<img src="https://pic3.zhimg.com/v2-258df167ee37b5594c72562b4ae61d1a_r.jpg" width="80%">
2. 将物体的中心落在哪个网格内，哪个网格就负责检测这个物体
3. 每个网格需要预测B个框（这B个框预测的为一个类别，即一个物体），C个类别，且最终根据NMS，只选取一个框。
4. 每个框包含了位置信息以及置信度(x,y,w,h,confidence)，所以一张图预测的信息一共有SxSx(Bx5+C)

<img src="https://pic1.zhimg.com/v2-8630f8d3dbe3634f124eaf82f222ca94_r.jpg" width="80%">

因为对于同一个网格的所有B个框，都只能检验为同一物体，因而YOLO对于靠的很近的物体以及小目标群体检测效果并不是很好。

损失函数存在问题，求和下标错误！！！