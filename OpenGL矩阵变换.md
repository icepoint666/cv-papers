# OpenGL矩阵变换

### Overview
几何数据——顶点位置，和标准向量(normal vectors),在OpenGL 管道raterization 处理过程之前可通过顶点操作(Vertex Operation)和基本组合操作改变这些数据。

**重要的变换矩阵储存在 ModelView 矩阵**

**OpenGL保存一个相似的矩阵去描述camera type叫做PROJECTION_MATRIX**

![](imgs/1.png)

### Object Coordinates
对象的本地坐标系——任何变换之前的最初位置.为了变换(transformation)这些对象，可以调用glRotate(),glTranslatef(),glScalef()这些方法。

`glTranslate(x, y, z)` 移动object一定距离

`glRotate(theta, x, y, z)`About the ray from origin, 顺时针旋转一定方向

`glScale(x, y, z)` 放缩object一定比例

##### Modeling Transformations
因为我们观察特定的model transformations 共享于多个模型之间，所以我们想避免连续reloading 相同sequence of transformations

Model View matrix 对于OpenGL保存a stack of 矩阵

`glPushMatrix()`push所有stack中的矩阵往下一个level，然后复制最上面的矩阵

`glPopMatrix()`pop the matrix off the stack

`glMatrixMode(GL_MODELVIEW)`

### Eye Coordinates
使用GL_MODELVIEW矩阵和Object坐标相乘所得。

在OpenGL中用GL_MODELVIEW将对象对象空间(Object Space)变换到视觉空间(eye space)。

矩阵是模型矩阵（Model Matrix）和视觉矩阵（View Matrix）的组合 (M_view * M_model)。其中，Model 变换指的是将Object Space转换到World Space.
