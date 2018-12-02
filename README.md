# OpenGL-ComputerGraphics
OpenGL demo

### Install
```shell
$ sudo pip3 install PyOpenGL
```
### OpenGL: Conventions
**Functions**
 - Most fucntions just `gl`
 - Functions starting with `glu` are utility functions
 - Functions starting with `glx` are for interfacing with the X Windows system
 
**Constants**
 - GL_2D, GL_RGB
 
**Data types**
 - GLbyte, GLfloat
 
**Function names indicate argument type and number**
 - Functions ending with f take floats
 - Functions ending with i take ints
 - Functions ending with b take bytes
 - Functions ending with ub take unsigned bytes
 - Functions ending with f take an array
 
**Examples:**
 - `glcolor3f()` take 3 floats
 - `glcolor4fv()` take an array 

OpenGL operates as an infinite
  - 1. Put things in the scene.(points, colored lines, textured polys)
  - 2. Describe the camera.(location, orientation, field of view)
  - 3. Listen for keyboard events.
  - 4. Render draw the scene.
 
OpenGL can render:
  - Geometric primitives(lines, points, polygens)
  - Bitmaps and images

OpenGL uses matrics:
  - Describes camera type
  - Describes current configuration of the 3D space 
  
### OpenGL: Coordinate system
**right handed(cartesian coordinate system)**
 
伸出你的右手， 你的大拇指(thumb)，手心(index)，中指(middle)形成一个互相正交(orthogonal)的坐标系

命名你的thum: x-axis

命名你的index: y-axis

命名你的middle: z-axis

摄像机默认look down negative z-axis

所以坐标系矩阵为
```
[[1 0 0]
 [0 1 0]
 [0 0 1]]
```
**现在想转变坐标系使得camera looks down x-axis**

x-axis -> nagative z-axis(A rotation of 90 degrees around the Y axis)
- x -> -z
- y -> y
- z -> x
```
[[0 0 1]
 [0 1 0]
 [-1 0 0]]
```
关于Y轴的旋转矩阵：
```
[[cosa 0 sina]
 [0 1 0]
 [-sina 0 cosa]]
```
**Setting up camera**
创造一个matrix， transform points in world coordinates to camera coordinates.
```
gluLookAt(eyeX, eyeY, eyeZ,
          lookX, lookY, lookZ,
          upX, upY, upZ)
```
