# Daily Thought (2019.1.1 - 2019.1.31)
**Do More Thinking!** ♈ 

**Ask More Questions!** ♑

**Nothing But the Intuition!** ♐

### 1.为什么Encoder-Decoder要生成latent variable？(1.14)
理解：相当于是把原本高维图像降维成了一组相对低维度的vector，就叫做隐变量（latent variable）。

计算出latent variable目的就是**滤去无关信息，浓缩了有用信息的**，什么有关什么无关根据损失函数的定义来规划。

如果不生成这样一个latent variable，直接通过一层层网络生成，那么它就不能除去掉原来图片中不想要的信息。

例如：风格转换，滤去原图中的风格信息，保留内容信息，就是encoder-decoder的结构。

### 2.迁移理解：根据对latent variable的思考反过来理解bottleneck以及降维升维结构

关于bottleneck的理解：https://zhuanlan.zhihu.com/p/39976502
