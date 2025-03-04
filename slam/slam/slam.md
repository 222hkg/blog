# Slam

## SLAM
slam的定义：自动驾驶/无人驾驶/无人机/机器人感知中，即时/同时/同步 定位与建图算法(slam)通过传感器收集到的实时数据，对车辆的位置和姿态进行估计和优化，构建高精度的点云地图。一边估测下一时刻的位姿，一边动态构建并更新全局一致性地图.SLAM（Simultaneous Localization and Mapping）算法是一种用于无人机或移动机器人同时定位自身位置和构建环境地图的算法。
[最详细的解释什么是slam](https://b23.tv/0KTcZWF)

传感器：双目相机，rgbd深度相机，结构光，激光雷达，毫米波雷达等都是常用的传感器，用来采集数据

分类：按照传感器的不同，分为视觉slam和激光雷达slam

用*相机*作为传感器的slam是视觉slam，但视觉传感器易受光线和天气变化的影响。而激光雷达可以准确获取三维数据且对环境变化不敏感

单一传感器获取的信息少，误差大，因此多传感器耦合，精度大

即使在多传感器耦合下，随着车辆位移的增加，在建图的过程中，帧与帧之间的匹配也会积累位姿误差，最终导致地图出现漂移，

回环检测可以检测当前传感器数据和历史传感器数据之间是否构成回环，然后构建回环帧之间的约束关系，从而有效地降低相邻帧之间匹配所造成的累计误差

在静止状态下，激光雷达发出的激光是旋转一周形成一个完整闭合的圆。但车辆是不断运动的，车载雷达旋转一周需要时间，会导致雷达开始扫描的起点和终点不在一条直线上，会产生一定程度的不完整漂移，这就是点云畸变，

惯性测量单元主要测量载体的角旋转速度和加速度，通过积分运算得到载体的位姿状态

### 三维空间中的刚体运动

    三维空间中的刚体运动的描述方式：旋转矩阵，变换矩阵，四元数和欧拉角

    1，三维空间由三个互相垂直的轴组成，一个点在三维空间中由三个轴的坐标指定

    2，一个刚体，不光有位置，还有姿态。相机是三维空间中的刚体，位置就是在空间中的哪个地方，姿态是相机的朝向

    3，坐标系之间的变化，两个4，用四个数表示三维向量的做法称为齐次坐标，引入齐次坐标后，旋转和平移可以放到同一个矩阵中，称为变换矩阵

    5，对于变换矩阵T，左上角是旋转矩阵R，右侧是平移向量t，左下角为0向量，右下角为1

    6，用旋转向量来表示旋转，旋转可以用一个旋转轴和旋转角来表示，用一个向量的方向和旋转轴一致，向量长度等于旋转角大小

    7，旋转向量有三个量，且没有约束

    8，欧拉角和旋转向量具有奇异性

#### 四元数

   四元数是复数引申来的，因此先介绍一下复数，复数由一个实部和一个虚部组成，复数平面是二维平面，分别由实轴和虚轴组成

虚数是从x²＝-1这个方程得出来的，因为无解。为了让其能解出来，定义虚数单位i，并令i²＝-1

我们知道复数(实数➕虚数)是可以表示旋转的
比如乘i表示逆时针旋转90度，乘i²也就是-1是逆时针旋转180度，所谓旋转，一定得乘上单位向量，因为我们考虑的是刚体运动，无论是相机还是机器人或者无人驾驶汽车，这些都是刚体，其形状不会随意变化，因为旋转只改变方向不会改变大小，单位向量的模长是1，因此需要乘单位向量来表示旋转

复数也可以表示缩放，比如一个复数乘上另外一个复数，相当于缩放了这个复数的模长，并旋转了一个角度。比如2+i这个复数，乘3+4i，相当于放大了5倍，再逆时针旋转arctan4/3度

因此，二维平面上的旋转可以用复数来描述，但是三维平面内却不能用三元数，这个就不证明了，因为会有bug，得用四元数来描述

四元数的表达方式是z＝w➕ai➕bj➕ck，其中第一项w是实部，后面三项是虚部

四元数是四维空间中的，因此对于三维空间中的三维向量，可以写成四维的形式，让实部为0就行了

对于四元数旋转来说，左乘一个二分之一角度的四元数，再右乘一个逆

但是为啥旋转关系式是p'＝qpq-1，为啥右边还要乘一个逆旋转向量？设想一下四维空间是由两个相互垂直的二维空间组成，有两个圆盘互相垂直，圆盘1占据两个纬度，圆盘2占据另外两个纬度，这两个圆盘的旋转互相不受影响。而四维空间中的旋转可以用这两个圆盘的旋转来表示，这两个圆盘可以同时逆时针旋转也可以同时顺时针旋转，也可以一个逆时针旋转一个顺时针旋转。不管是左乘还是右乘，都会同时旋转两个圆盘，而我现在需要的只旋转一个方向也就是一个圆盘，呢么如何实现捏？我让圆盘1先逆时针旋转，圆盘2旋转二分之一的角度，然后再让圆盘1顺时针旋转，圆盘2再旋转二分之一的角度，这样的话圆盘1相当于没动，圆盘2旋转了一定的角度，这样就可以把点p或者向量p按照一个固定的方向旋转了一定的角度
 
### 李群和李代数
#### 为啥引入李群
    1，一个刚体在三维空间中的运动由旋转和平移组成

    2，每一个三维参考系都有一组基底，世界坐标参考系中的向量a，经过一次旋转R和一次平移t后得到了a'。则a'＝Ra➕t ，t是平移向量

    3，可以用旋转矩阵和欧拉角和四元数描述同一个旋转。旋转矩阵相对直观，但是有9个量，过于冗余，所以引入了欧拉角，但欧拉角有万向锁的问题，因此引入了四元数，当四元数的第一项接近0的时候，剩下的三个分量会非常大，这个时候就会不稳定

    4，需要对下一时刻状态进行估计，会产生误差，需要使得误差最小。则对误差表达式进行求导：
     df(R➕ΔR)/ΔR

    因为旋转矩阵具有约束，即行列式为1且正交，因此两个旋转矩阵相加并不是一个旋转矩阵，因此这里不能对R求导，需要引入李代数来解决

坐标系之间的运动由一个旋转➕一个平移组成

#### 2

slam的过程就是不断的估计相机的位姿和建立地图

相机位姿就是变换矩阵T

假设某个时刻相机的位姿是T，观察到世界坐标系中的一个空间点p，在相机上产生了一个观测数据z

呢么z＝Tp➕noise

noise是观测噪声

观测误差e＝z-Tp

一共有N个三维点和观测值z，我们的目标是寻找一个最佳的位姿变换矩阵T，使得整体的误差最小
即
对矩阵求导，
对于变换矩阵T，所在的SE(3)空间，对加法计算不封闭，也就是说任意两个变换矩阵相加后并不是一个变换矩阵，这是因为变换矩阵对于加法是不封闭的。
李代数可以解决不封闭问题。

将SE(3)空间的T映射为李代数，记作se(3)，李代数由向量组成，向量对加法是封闭的，这样可以通过对李代数求导进而间接的对变换矩阵求导

旋转矩阵R具有一定的约束：RᵗR＝I，det(R)＝1
旋转矩阵R1和R2均满足此约束，但R1+R2不满足

群在数学上定义为一种集合加上一种运算的代数结构

slam中有两个群：一个是特殊正交群SO(3)，也就是旋转矩阵群。另一个是特殊欧式群，也就是变换矩阵群，3是三维

李群的定义是连续变化的光滑群

slam的目的是求解优化相机的最佳变换矩阵T，采用迭代优化，每次迭代都更新一个位姿增量delta，使得目标函数最小。通过误差函数对T求导得出delta，也就是说对T求导

李代数对应李群的正切空间，描述了李群局部的导数


第一个结论：旋转矩阵的微分等于一个反对称矩阵乘它本身

### 相机和图像

![img_v3_02cd_fb5f0507-c995-49b1-9c22-c03e949d2a1g](https://github.com/222hkg/222hkg.github.io/assets/83269196/180d4262-9914-49ad-b00a-0bcaa7870df7)


### 视觉里程计（前端）
1，视觉slam的前端被称为视觉里程计(VO)，基于相邻帧之间的信息从而粗略的估计相机运动和特征。视觉里程计分为特征点法和直接法

2，把visual slam分为前端和后端。前端为视觉里程计和回环检测，是对图像数据进行关联。后端是对前端的输出结果进行优化，利用滤波或者非线性优化，从而得到最优的位姿估计和全局一致性地图

3，VO：研究图像帧间的变换关系完成实时位姿跟踪，对输入的图像进行处理，计算位姿变化，得到相机间的运动关系

4，视觉里程计的任务是 已知初始位置C0，通过上一时刻的位置Ck-1和Tk来计算当前时刻的位置Ck，其中Tk是k和k-1之间的变换矩阵

5，对于相邻的两张图片，判断相机在这两张图片之间的运动。对于特征点法，首先要对两张图片进行特征提取，也就是找到图片中特别的地方，比如角点，边缘点等，其次对这些特征点在两张图片之间进行特征匹配，把误匹配的点筛掉之后，利用特征点计算相机的位姿

6，位姿就是位置和姿态，位置在三维空间中有三个坐标，姿态是在三位空间中的旋转(r,p,y)，因此位姿包含6个自由度，

7，相机运动中，有4个常见的坐标系:
       世界坐标系
       相机坐标系：以相机光心为原点，光轴为Z
       归一化坐标系：原点在相机坐标系下(001)处的二维平面坐标系
      像素坐标系：以图片左上角的像素为原点，以一个像素为最小单元的离散坐标系
8，我们能获取的是图片的像素信息，通过转换(相机投影模型，小孔成像)得到该像素(特征点)
在相机坐标系中的坐标位置，再通过坐标系转换，换成世界坐标系
![哈哈哈哈1](./qq.png)

