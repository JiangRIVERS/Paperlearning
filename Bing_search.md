#【Learning】Internet-Scale Deep Learning for Bing Image Search

## Core point
How semantic vectors helped improve Bing Web Search.
## 搜索流程
```flow
s=>start: 用户搜索
cond=>condition: Bing
op1=>operation: 从包含文本文字的界面搜索图片
op2=>operation: 映射到语义空间搜索图片
op3=>operation: Deep Learning
op4=>operation: Image embedding && Text embedding

s->cond
cond(yes)->op1
cond(no)->op2
op2->op3
op3->op4
```