# DSMM

DSMM是Deep Structured Semantic Model 的缩写。核心思想是将query和doc映射到共同的语义空间中，通过最大化query和doc语义向量之间的==余弦相似度==，从而得到隐含语义模型，达到检索的目的。·

## DNN结构
<img src="https://pic1.zhimg.com/v2-da282bca52d5144ff17af5f8e30b9dd4_r.jpg" width="100%">

+ 使用tanh作为输出层和隐藏层的激活函数。
+ 使用R(Q,D)=consine(yQ,yD)来计算query与doc的语义向量的相关性分数。
+ 针对同一个query的正例和J个反例的相关性分数使用softmax，再使用loss计算损失
+ 缺点是输入的term向量使用的是one-hot编码，词典大小过大

## word hashing
DSSM中引入word hashing方法，将其作为DNN中第一层

+ word hashing方法是用来减少输入向量的维度，该方法基于字母的 n-gram。给定一个单词(good),我们首先增加词的开始和结束部分(#good#),然后将该词转换为字母n-gram的形式(假设为trigrams：#go,goo,ood,od#)。最后该词使用字母n-gram的向量来表示。
+ 缺点是在于可能造成冲突，因为两个不同的词可能有相同的n-gram向量表示。
+ 依靠用户点击来判断query与doc是否相关从而进行训练

## 优点与不足
+ 优点
  + 解决字典爆炸问题
  + 鲁棒性强
+ 缺点
  + 可能引起冲突
  + DSSM采用了词袋模型，损失了上下文信息
  + 依靠用户是否点击判断正负样本，噪声比较大，难以收敛
  + ==对于中文如何进行n-gram操作?偏旁？笔画？拼音？==

## 优化变种
+ CNN-DSSM
+ LSTM-DSSM
+ MV-DSSM

