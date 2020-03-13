# FaceNet

[感谢](https://zhuanlan.zhihu.com/p/24837264)

[代码参考](https://github.com/tbmoon/facenet/blob/master/train.py)


## 核心
直接将人脸图像映射到欧几里得空间，空间距离的长度代表了人脸图像的相似性。只要该映射空间生成，人脸识别，验证和聚类等任务就可以轻松完成。模型的优点是只需要对图片进行很少量的处理（只需要裁剪脸部区域，而不需要额外预处理，比如3d对齐等），即可作为模型输入。
## 应用
+ 人脸验证（是否是同一人）
+ 识别（这个人是谁）
+ 聚类（寻找类似的人）

## 模型
<img src="https://pic1.zhimg.com/v2-ced157b8ca1fa96603c30b651eb2e1e0_r.jpg" width="80%">

## Loss
采用基于triplets的LMNN（最大边界近邻分类）的Loss的函数进行训练。triplets包含两个匹配脸部缩略图和一个非匹配缩略图，loss函数目标是通过距离边界区分正负类。

### triplets loss

<img src="https://pic1.zhimg.com/80/v2-e97dea2c74c31b53803925294983b7c8_720w.png" width="80%">

### 公式

<img src="https://pic4.zhimg.com/80/v2-fb0de06aa80bfd4bb6eb9a24f9855c6b_720w.png" width="80%">

<img src="https://pic3.zhimg.com/80/v2-89f6cb30446edc2f7748ed0541d1aeba_720w.png" width="60%">
其中 [x]_+ 为取正函数，相当于max{x,0}

## Triplets 选取
选择大样本的mini-batch，每个mini-batch中，对单个个体选择40张人脸图片作为正例，随机筛选其他人脸图片作为负样本。
筛选负样本采用如下公式：

<img src="https://pic3.zhimg.com/80/v2-2af5cd0d92a4ab587cf44db2b463241a_720w.png" width="80%">

## Embedding 维度对实验结果的影响
<img src="https://pic2.zhimg.com/80/v2-41167c2bea4fd3602bcbbf68f5d8eb01_720w.png" width="80%">