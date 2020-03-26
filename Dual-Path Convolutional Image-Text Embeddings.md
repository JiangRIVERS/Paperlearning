# Dual-Path Convolutional Image-Text Embeddings with Instance Loss

[感谢](https://zhuanlan.zhihu.com/p/33163432)

## 解决的问题
instance-level的图文互搜
文章想解决的问题是instance-level的retrieval，也就是说 如果你在5000张图的image pool中，要找“一个穿蓝色衣服的金发女郎在打车。” 实际上你只有一个正确答案。不像class-level 或category-level的 要找“女性“可能有很多个正确答案。所以这个问题更细粒度，也更需要detail的视觉和文本特征。

## 网络结构
+ 输入：实际上我们将每张训练集中的图像认为成一类。（当然, 如果只用一张图像一类，CNN肯定会过拟合）。同时，我们利用了5句图像描述(文本)，加入了训练。所以每一类相当于 有6个样本 （1张图像+5句描述）。

+ 整体网络架构

<img src="https://pic2.zhimg.com/v2-020b278e0cfc4f8250648e6006b0db8d_r.jpg" width="100%">

<img src="https://pic2.zhimg.com/80/v2-459a9d877cb3ab310a0d178ec1c80361_720w.jpg" width="80%">

对于文本侧同样使用CNN，输入网络前对文本进行word2vector

## 总结
文章主要解决了一个细粒度图文互搜的问题。文章有两个创新点，第一是使用CNN对文本word2vector结果进行卷积，而不是LSTM。第二是提出Instance loss。作者提出当前图文互搜不是细粒度，一个文本可能对应多个图片，Ranking loss只解决了图片与文本之间的相似度问题，而对图片与图片间，文本与文本间之间差别的区分没有帮助。于是作者将数据集中一张img+五个text视为一类，总共29000类，==对每类进行标注==。在stageI分别训练img CNN和text CNN，将img fc 和 text fc 经过一个共享权重的W层(共享是为了将img和text映射到同一语义空间中)后分别和label类计算CrossEntropy，回传，解决图与图之间、文本与文本之间相似度。stageII将img fc和text fc进行ranking loss，回传，解决图与文本之间相似度。