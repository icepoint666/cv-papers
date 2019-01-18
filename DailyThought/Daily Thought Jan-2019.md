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

![](__pics/ae-gan.jpg)

之后论文 ECCV2018的adaptive-style-aware 也就是这种AE+GAN的结构：https://arxiv.org/pdf/1807.10201.pdf

### 4.U-net网络结构 （1.18）
U-net与FCN差不多，区别就是
- 1.u-net是完全对称的，下采样与上采样一样的结构
- 2.u-net是skip connection的结构, FCN是也是skip connection的结构, 区别就是:
  - FCN用的是加操作summation
  - u-net用的是叠操作concatnation

关于U-net/FCN的思考：

U-Net和FCN为什么成功，因为它相当于给了一个网络的框架，具体用什么特征提取器，随便。这个时候，高引就出现了，各种在encoder上的微创新络绎不绝，最直接的就是用ImageNet里面的明星结构来套嘛，前几年的BottleNeck，Residual，还有去年的DenseNet，就比谁出文章快。这一类的论文就相当于从1到10的递进，而U-Net这个低层结构的提出却是从0到1。说句题外话，像这种从1到10的论文，引用往往不会比从0到1的论文高，因为它不自觉的局限了自己的扩展空间

U-net详细研习：https://zhuanlan.zhihu.com/p/44958351

### 5.skip-connection结构（1.18）
skip-connection属于**拓扑结构**的范畴

skip connection是由resnet里面提出的

关于resnet，densenet其中都涉及到了**dense topology**的观点

![](__pics/topology.jpg)

表面上resnet是一种简单的skip connection结构，但是《Mixed Link Networks》这篇论文推导证明了ResNet本质上也是一种Dense的密集拓扑连接。

换句话说，DenseNet并没有提出新的拓扑连接模式，它和ResNet唯一的区别就是：在一个相同的“Dense Topology”的基础上，ResNet使用了element-wise addition来连接，而DenseNet则使用了concatenation来连接。

很明显，ResNet和DenseNet都走了两个极端—一个只逐元素加“+”，一个只做拼接“||”。于是一个混合它们来提升的思路就非常显而易见了，mixnet就是两者融合了。

关于mixnet：https://zhuanlan.zhihu.com/p/33634915
