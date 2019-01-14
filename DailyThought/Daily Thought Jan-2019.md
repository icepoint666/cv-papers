# Daily Thought (2019.1.1 - 2019.1.31)
**Do More Thinking!** ♈ 

**Ask More Questions!** ♑

**Nothing But the Intuition!** ♐

### 1.为什么Encoder-Decoder要生成latent variable？（1.14)
理解：相当于是把原本高维图像降维成了一组相对低维度的vector，就叫做隐变量（latent variable）。

计算出latent variable目的就是**滤去无关信息，浓缩了有用信息的**，什么有关什么无关根据损失函数的定义来规划。

如果不生成这样一个latent variable，直接通过一层层网络生成，那么它就不能除去掉原来图片中不想要的信息。

例如：风格转换，滤去原图中的风格信息，保留内容信息，就是encoder-decoder的结构。

### 2.迁移理解：根据对latent variable的思考反过来理解bottleneck以及降维升维结构 （1.14）

关于bottleneck的理解：https://zhuanlan.zhihu.com/p/39976502

bottle-neck就是指将信息压缩再放大的结构：自编码器以及squeeze-net里的fire-module都是这种结构。

能够work的原因：

- 1.降维又升维，类似NMF，去除高频噪声的作用
- 2.不同应用或者不同需求，有用的信息域是不一样的。针对任意一个具体的需求（人脸识别，物体追踪……）,**数据里有用的信息只占少数**，而算法需要的就是**排除掉无用信息，仅保留有用信息的表达形式**。
- 3.正因为数据本身是臃肿的需要精简的，所以无用信息的损失是必要的。

图片可以通过简单的描述来压缩，长宽高，位置，角度，颜色，物体，材质等等。

所以理论上可以描述为：**图片是高维空间的低位流型**

### 3.GAN与VAE有什么关系和区别呢？（1.14）
