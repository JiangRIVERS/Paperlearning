# CDSSM

参考blog:https://blog.csdn.net/sxf1061926959/article/details/89344251

## 核心

+ 改变word embedding方式: letter-tri-gram + word-tri-gram (如果是中文则不需要分词，因为中文量太大)

+ 将DSSM中的全连接换成卷积

+ 引入了Max-pooling

<img src="https://img-blog.csdnimg.cn/20190417201720556.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9kZWVwLXJlYy5ibG9nLmNzZG4ubmV0,size_16,color_FFFFFF,t_70" width="100%">