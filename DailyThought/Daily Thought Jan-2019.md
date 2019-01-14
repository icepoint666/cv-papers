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
不说loss里，JS散度和KL散度上的区别

主要说本质区别

**VAE**: Variational AutoEncoder

- 本质上：就是图片A encode 成为 latent vector 再 decode 成图片B
- 监督策略：（loss）就是图片A类与图片B类之间差别作为监督（就是看折腾一下前后一样不一样呗）
- 变分策略：variational变分具体就是指 encode 得到的latent vector经过高斯噪声（变化量）处理，为了防止前后生成都是一样的图片（就没有意义了），所以就是加一些变化。

**GAN**: Generative Adversarial Network

- 本质上：就是latent vector 通过 decoder(这里叫作generator) 生成 图片。
- 监督策略：就是对抗监督，加入一个discriminator来协助监督，loss就是这样的一个对抗损失。
- 变分策略：刚开始的latent vector就是由高斯分布生成的。

那么我们其实发现**VAE的侧重点是AE，也就是 encoder + decoder**， **GAN的侧重点就是对抗策略**

其实VAE的decoder就相当于GAN里的generator，所以就有了GAN+VAE结合的思路

![](
