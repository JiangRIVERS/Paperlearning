## YOLO V3

### Title: YOLOv3: An Incremental Improvement

### YOLO V2 + YOLO 9000
1. YOLO V2
+ 利用wordTree设计，充分利用分类数据集，弥补目标识别类别数目的不足
+ 重新设计基础网络darknet-19，输入尺寸可变，从而在同一套模型上，提供速度和精度之间的切换
+ 重新设计anchor box和坐标变换格式，使网络收敛更快，精度更高

### YOLO V3
1. k-means++ 聚类产生anchor框
