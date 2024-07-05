# HKG的博客空间

<p align="center">
 
大家好，欢迎来到我的博客空间，邮箱：1991588930@qq.com

</p>

> 总有人间一两风，填我十万八千梦
>
> 愿许清风知我意，散我心中意难平

- [x] 我是hkg
- [x] 安徽省滁州市凤阳县

![](./20240704-220111.png "我的签名")

本科毕业于[新疆大学物理科学与技术学院](https://phy.xju.edu.cn/)，毕业论文指导老师：[王淑英老师/教授](https://phy.xju.edu.cn/info/1121/2164.htm)

硕士毕业于BNU物理与天文学院，导师是[安维明老师/教授](https://astro.bnu.edu.cn/zw/gk/szdw/zrjs/js/102182.html)
在老师指导下，曾获得物中国物理学会[2022年学术会议优秀海报奖](http://meeting.cps-net.org.cn/sustech2022/multiinfo/74)
，发表学术期刊[等离子密度对尾场加速器中最优束流负载的影响](http://www.bnujournal.com/article/doi/10.12202/j.0476-0301.2023166)

[2017年周培源力学竞赛国三](https://publicqn.saikr.com/23ac802d349a4fb6bc7586455d363a341498643688769.xls?attname=%E9%99%84%E4%BB%B62%EF%BC%9A%E4%B8%AA%E4%BA%BA%E8%B5%9B%E4%B8%89%E7%AD%89%E5%A5%96%E5%92%8C%E4%BC%98%E7%A7%80%E5%A5%96.xls)

[大学生数学竞赛新疆赛区一等](https://mp.weixin.qq.com/s/JK12FDrq0Thcwr0rGBTbIA)

 ***
 ---
 




---

## 图片

https://v.douyin.com/i6H3S8jj/ 



## SLAM
-slam的定义：自动驾驶/无人驾驶/无人机/机器人感知中，即时/同时/同步 定位与建图算法(slam)通过传感器收集到的实时数据，对车辆的位置和姿态进行估计和优化，构建高精度的点云地图。一边估测下一时刻的位姿，一边动态构建并更新全局一致性地图.SLAM（Simultaneous Localization and Mapping）算法是一种用于无人机或移动机器人同时定位自身位置和构建环境地图的算法。
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

    3，坐标系之间的变化，两个坐标系之间的运动由一个旋转➕一个平移组成

    4，用四个数表示三维向量的做法称为齐次坐标，引入齐次坐标后，旋转和平移可以放到同一个矩阵中，称为变换矩阵

    5，对于变换矩阵T，左上角是旋转矩阵R，右侧是平移向量t，左下角为0向量，右下角为1

    6，用旋转向量来表示旋转，旋转可以用一个旋转轴和旋转角来表示，用一个向量的方向和旋转轴一致，向量长度等于旋转角大小

    7，旋转向量有三个量，且没有约束

    8，欧拉角和旋转向量具有奇异性
 
### 李群和李代数
#### 为啥引入李群
    1，一个刚体在三维空间中的运动由旋转和平移组成

    2，每一个三维参考系都有一组基底，世界坐标参考系中的向量a，经过一次旋转R和一次平移t后得到了a'。则a'＝Ra➕t ，t是平移向量

    3，可以用旋转矩阵和欧拉角和四元数描述同一个旋转。旋转矩阵相对直观，但是有9个量，过于冗余，所以引入了欧拉角，但欧拉角有万向锁的问题，因此引入了四元数，当四元数的第一项接近0的时候，剩下的三个分量会非常大，这个时候就会不稳定

    4，需要对下一时刻状态进行估计，会产生误差，需要使得误差最小。则对误差表达式进行求导：
     df(R➕ΔR)/ΔR

    因为旋转矩阵具有约束，即行列式为1且正交，因此两个旋转矩阵相加并不是一个旋转矩阵，因此这里不能对R求导，需要引入李代数来解决
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



## AR-HUD
HUD（head up display抬头显示器）是将重要信息显示在挡风玻璃上的一种显示系统，基本原理是：**投影仪**发出的光信息，经过一系列的折射、反射等投影到挡风玻璃上，人眼就能看到投射在上面的信息，感觉信息就像悬浮在前方一样。
![](./1.jpeg)

   [tu](https://nimg.ws.126.net/?url=http%3A%2F%2Fdingyue.ws.126.net%2F2022%2F0517%2F93bbb031j00rc179s00ffc000o000dim.jpg&thumbnail=660x2147483647&quality=80&type=jpg＂hud在车上的效果图＂)

跟许多军用转民用的设备一样，hud最早也是军用的，是用在了直升机上，可以把车速，导航信息，油量等等投影在挡风玻璃前，这样驾驶员不需要低头就可以查看到仪表盘上到信息，甚至不止这些，这样可以大大提高驾驶安全性

中国搞hud还没有几年，虽然越来越多的汽车开始搭配这个，但目前还是在一个开发阶段，还不是一个成熟的产品，而且搭配这个的车要多出一万块钱。

目前，hud的发展难点在三个方面：1成像质量还不够好，2价格成本问题，现在不仅仅是hud，整个汽车行业都在卷价格战，以及经济不好引发的降本增效，3空间体积，因为汽车不像直升机有这么大空间，要在车的仪表盘下的空间塞一个几升的hud还是对体积要求非常高，汽车里空间是寸土寸金的，如果hud太大，会影响别的设备在汽车内部的位置


## Zemaxg光学设计软件

### 坐标间断

## 卡尔曼滤波算法(kalman filter)
 算法思想：用预测值和观测值 的**加权**来求解最优估计值，从而不断逼近真值。得知道两个值的方差。
![image](https://github.com/222hkg/222hkg.github.io/assets/83269196/6cb79028-cacb-446b-856c-d0d51b8856ab)

 如何加权捏？假如有两个称，测量精度都是正负2g,呢么测量一个物体的重量，第一个称的示数是m1,第2个称示数是m2，呢么重量就是两者之和除以2；如果第一个称的测量误差是2g，第2个是3g,我们知道误差越大，其值可信度越低，加权系数院越小，则最终值是3/5m1 + 2/5m2;加权系数就是卡er曼系数

 
![img_v3_02bt_4488bf6f-eaf8-4f67-b648-d89f2e47b29g](https://github.com/222hkg/222hkg.github.io/assets/83269196/296fe3e4-8a52-4bf1-886c-399634b0f479)


## C➕➕

1. std::count，标准输出
2. 标准输出，cont << 变量 << endl;
3. 

## 相对论/光速/时间
1，大质量天体会弯曲周围的时空，为什么我们感觉不到
2，时间是什么？我们的上一秒去哪儿了？

把时间当成四维空间的一个维度就可以理解了

先从低纬度理解，比如在一维空间里，两个人吵架了，女的一直向上走，结果最后又回到了原点。因为他们缺少一个维度，所以他们不知道自己其实走的是一个曲线。这个曲线就是圆形，圆形是二维空间的东西

同样的，两个蚂蚁自认为生活在二维空间中，他们平行向上前进，结果诡异的事情出现了，两个蚂蚁相遇了，因为我们知道平行线是不可能相遇的，但这只满足二维空间，在三维空间中的球体上，两个平行线是可以相交的。但是二维空间的蚂蚁理解不了

## 卫星定轨


     低轨卫星指的是距离地面200(100)-2000km的卫星，近年来快速发展在各领域有广泛应用。

     而实时确定 地轨卫星 的轨道参数 是使其对地面上遥感和观测的基础条件

     定轨的目的是精确的知道卫星的坐标和速度信息

     定轨精度主要取决于"轨道观测技术"和"定轨算法"

     地轨卫星上搭载了"GPS接收机"，从而可以借助GPS来实现对地轨卫星的[实时定轨]，因为GPS具有全天候，高精度，低成本以及可连续观测的优势，所以越来越多的地轨卫星搭载GPS接收机这个硬件


     用数学模型对卫星在空间中的受力情况的描述成为"动力学模型"

## 工程项目积累


- 雾度（haze）是偏离入射光 2.5°角以上的透射光强占总透射光强的百分数，雾度越大意味着薄膜光泽以及透明度尤其成像度下降
- 太阳倒灌的步骤：一度一度的去算，360度/180度，找出哪个特定角度的太阳辐射最大
1.在眼盒处设置一个光源，天窗上/头顶上做一个靶结构，以眼盒为光源看看有没有光，因为光路可逆，可以确定杂光的路径
2.开始模拟真的太阳光，为了要看能量有多少，因为用眼盒做光源是模拟不出来光源的能量
  第一步是找杂光路径，第二步确定能量，如果能量特别小，可以忽略
  阳光倒灌要对元器件进行热分析
-

## 刘珂矣


## Github中Readme的编写规范--我这个博客的编写规则

     换行：两个空格+回车
     多行文本：4个空格
     加横线：三个 ***或---
     


# 111

