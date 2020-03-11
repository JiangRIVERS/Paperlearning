## Siamese network
参考:https://zhuanlan.zhihu.com/p/35040994

<img src="https://pic3.zhimg.com/80/v2-5070e28622a2f3ee9e3cb5d2259fae86_720w.jpg" width="50%">
神经网络的连体通过==共享权值==实现
==若两边不共享权值，而是两个不同的神经网络，则称为"伪孪生神经网络"(pseudo-siamese network)==
### 孪生神经网络用途
衡量两个输入的相似度

### 早先论文
1. 1993《Signature Verification using a ‘Siamese’ Time Delay Neural Network》用于验证美国支票上的签名与银行预留是否一致
2. Hinton 2010 《Rectified Linear Units Improve Restricted Boltzmann Machines》用于人脸验证

### 损失函数
1. Contrastive Loss

2. Cosine

3. exp function

4. 欧氏距离
  ...
  根据[知乎作者](https://zhuanlan.zhihu.com/p/35040994)实验分析，cosine更适用于词汇级别的语义相似度度量，而exp更适用于句子级别、段落级别的文本相似性度量。其中的原因可能是cosine仅仅计算两个向量的夹角，exp还能够保存两个向量的长度信息，而句子蕴含更多的信息。

### 可以三胞胎连体，让相同类别的距离尽可能小，不同类别的距离尽可能大

