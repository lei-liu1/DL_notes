[TOC]

# Convolutional neural networks

###### ==卷积运算可以检测图像边缘==

<img src="https://i.loli.net/2020/08/10/yUGLNm951a6iqoh.png" alt="image-20200730101300765" style="zoom:50%;" />

###### ==为什么使用padding==

1. 防止图片大小缩小
2. 多次利用边角处的像素点

###### ==卷积运算(数学意义)==

原始3$\times$3卷积核：

|  3   |  4   |  5   |
| :--: | :--: | :--: |
|  1   |  0   |  2   |
|  -1  |  9   |  7   |

卷积运算之前，先左右翻转，再上下翻转：

|  7   |  9   |  -1  |
| :--: | :--: | :--: |
|  2   |  0   |  1   |
|  5   |  4   |  3   |

然后进行**互相关**运算

###### ==三维卷积==

<img src="https://i.loli.net/2020/08/10/lqrMc9ZkGXuTyYL.png" alt="image-20200730105208679" style="zoom: 50%;" />

<img src="https://i.loli.net/2020/08/10/QVZWI3KJiysSYPH.png" alt="image-20200730110118802" style="zoom: 50%;" />

**多个filter可以理解为同时进行水平边缘检测和垂直边缘检测，或者其它类型的边缘检测**

###### ==**GoogLenet**: inception module==

<img src="https://i.loli.net/2020/08/10/j6KNYOUVoBFSdMT.png" alt="image-20200801101609748" style="zoom: 33%;" />

###### ==$1\times 1$卷积层的作用==

1. 减少通道数，从而降低模型复杂度

###### ==迁移学习==

1. 如果自己的数据集很小，可以只改变最后的输出层，把预训练好的模型前面的参数都冻结

   数据集越大，可以冻结越少的参数

2. 计算机视觉经常用到迁移学习

# Recurrent neural networks

###### ==Why not a standard network==

<img src="https://i.loli.net/2020/08/10/2PVZoyLc7DjUXqt.png" alt="image-20200805103653110" style="zoom: 33%;" />

Problems

1. Inputs, outputs can be different lengths in different examples

2. Does not share features learned across different positions of text

   （不能共享那些从文本不同位置学到的特征）

###### ==RNN 类型==

<img src="https://i.loli.net/2020/08/10/RX3Kcv6n8y1PBwo.png" alt="image-20200805124659172" style="zoom: 33%;" />

one to many:音乐生成

many to one:根据一个句子进行电影评分

many to many:人名检测 / 机器翻译

###### ==矩阵求导==

$$
Y = Ax\\
\frac{\partial Y}{\partial x} = A^T\\
\frac{\partial Y}{\partial A} = x
$$

#### NLP

###### ==NLP中为什么使用词嵌入？==

每两个单词的one-hot向量不能表示这两个词的相似程度，为了使算法具有更强的泛化能力，选取一些特征来描述单词，例如：可以从 I want a glass of orange juice 推断出 I want a glass of apple____ 空格里面可以填 juice

###### ==Transfer learning and word embeddings==

1. Learn word embeddings from large text corpus(1-100b words)
    (Or download pre-trained embedding online)
2. Transfer embedding to new task with smaller training set (say, 100k words)
3. Optional: Continue to finetune the word embeddings with new data

###### ==相似度函数==

两个单词的相似度是他们的词嵌入向量夹角的余弦值

<img src="https://i.loli.net/2020/08/10/sFWhK8jO6RiAInB.png" alt="image-20200808095753600" style="zoom: 50%;" />

###### ==嵌入矩阵==

<img src="https://i.loli.net/2020/08/10/UfJkx5sPTKeLrwD.png" alt="image-20200808100618046" style="zoom: 50%;" />

#### Various sequence to sequence architectures

###### ==机器翻译==

![image-20200810093009116](https://i.loli.net/2020/08/10/tB4QVSgT1NYJGwM.png)

![image-20200810093148318](https://i.loli.net/2020/08/10/8GqRPm4wbxaEIMB.png)



###### ==Beam seatch==

每次都从序列中选出条件概率最高的B（超参数）个序列，传入到下一个时间步

![image-20200810100526679](https://i.loli.net/2020/08/10/Kef8uviZoNx7JlG.png)

因为目标函数是多个小于1的概率的连乘积，所以序列长度越长，目标函数值越小，模型倾向于输出短序列，为了消除这种影响，修改一下目标函数。其中$\alpha$是启发值，根据经验设置

---

![image-20200810100006476](https://i.loli.net/2020/08/10/95FVQhoYvXU3l64.png)

---

![image-20200810102138070](https://i.loli.net/2020/08/10/z3bLiZokWxGn8J2.png)

---

![image-20200810104931812](https://i.loli.net/2020/08/10/5E43hHGi9VwyeJP.png)

---

![](https://i.loli.net/2020/08/10/nm9UbTRBw6QaDxY.png)

###### ==Attention model==

![image-20200810112315013](https://i.loli.net/2020/08/10/YEpJNksDVa8fxcX.png)

**利用双向RNN产生的激活和注意力权重，做为另一个RNN模型的输入，从而产生翻译后的序列**![image-20200810114337391](C:\Users\叁铈化硫\AppData\Roaming\Typora\typora-user-images\image-20200810114337391.png)

**重新训练一个网络以得到注意力权重，所以时间复杂度是两倍的**

![image-20200810115519001](C:\Users\叁铈化硫\AppData\Roaming\Typora\typora-user-images\image-20200810115519001.png)

**注意力机制**

<img src="https://i.loli.net/2020/08/10/MG5Tulr9zKp1wUd.png" alt="attn_model" style="zoom: 50%;" />

<img src="https://i.loli.net/2020/08/10/UlQBzhmSFPwqNGr.png" alt="img" style="zoom: 67%;" />