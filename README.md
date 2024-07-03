# HKG的博客空间


<p align=＂center">
大家好，欢迎来到我的博客空间，邮箱：1991588930@qq.com
</p>


  
## 社会、政治、经济、历史、文化

### 土地兼并导致王朝覆灭
> 当农民无法活下去的时候，王朝离结束也就不远了

    朝廷的财政收入主要是靠土地税维持的，也就是农民种地，毕竟是农业大国。在王朝初期，可以收到很多税，
    一般王朝初期都是欣欣向荣，但是过了百八十年以后，也就是说经历了两三任皇帝以后，人口越来越多，官员
    越来越多，贵族数量越来越多，朝廷的财政收入和农民的收入开始入不敷出，
    在初期，贵族官员无需纳税，朝廷供养，此时人少，没有感觉，过了百八十年后，皇室贵族从个位数繁衍到数千
    名数万，他们还侵占了大部分土地，原本村里十户农民都有的耕地，现在只有两户了，剩下的八户农民没有地，只
    能给地主打工当佃户来交租，这个时候土地税就减少了，这两户耕地的农民除了骂骂街并没有什么办法。这个时
    候朝廷摊派的徭役就没有人去了，比如修水利，修河堤打水井这些基础设施
    没有人去干，朝廷拨下来的银子，因为河堤没修好，有的地方洪水泛滥，农民房子被毁，有的地方水井没人打，就
    干旱成灾，导致粮食产量大面积减少，有时候看起来是天灾 ，但是人祸的成分也不小。呢么朝廷要派人去赈灾，但是
    朝廷没有银子也没有粮食，可怎么办。在这种恶性循环下，王朝实力越来越弱，以前周边臣服的游牧民族趁你病要
    你命，朝廷要打仗，打仗要有军饷，不发工资谁替你卖命，想要筹备军饷就只能再问呢两户农民征收，但是重压之
    下这两户农民已经活不下去了，于是将黄色头巾绑在头上，皇帝看着亲王家里有两万亩田地，三个乡的农民都是他
    家的佃户，就连宦官家里都有一千亩田地和两家银行股份。如果皇帝处理好了，打土豪分田地，将他们的土地重新
    收回分给农民，此时回迎来王朝的中兴，降低了土地兼并的速度，但是朝廷里的势力盘根错节，互相帮助，他们联
    合起来的实力比皇帝还要大。明朝的崇祯就是面临这样的境地，所有臣子对他毕恭毕敬，但是心底里瞧不起的就是
    你崇祯帝，在座的各位都比你有钱，就算你这个王朝覆灭，换个王朝我也一样给皇帝打工古代封建王朝没有一个
    超过300年，历史反复上演，道理都懂，却没有一个王朝愿意去改变，
    

> 什么是[佃户](https://zhidao.baidu.com/question/991461279207700539/answer/4012922016.html)？和佃农的区别










  > 现代工业创造价值的速度快于土地兼并的速度
### 屁股决定脑袋
[车上和车下的人所在的位置不同，意味着立场不同](https://photo.baidu.com/photo/wap/albumShare/share/75997136071947416?from=linkShare)
车上的既得利益者总想保持自己的利益，这就是人性的自私，脑袋跟着屁股走，你的屁股坐在什么位置上，你的脑袋就会随之产生什么样的想法，原先没有的想法，现在都有了


## 视频
[小李](https://photo.baidu.com/photo/wap/albumShare/share/27143205929874584?from=linkShare)
[嘟嘟醉](https://h5.pipix.com/s/i6m3b8PB/)

## 图片




## Python

- np.random.normal()函数用于生成正态分布函数，有三个参数。第一个参数是随机数的期望值，对应的是整个分布的中心；第二个是随机数的标准差，数越大越矮胖；第三个数是生成随机数的个数，默认为NONE，则只输出一个数
- shape（）函数的功能是读取矩阵或数组的长度，shape（0）是读取行数，shape（1）是读取列数

### openCV库

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


### 相机和图像



### 视觉里程计（前端）
1，视觉slam的前端被称为视觉里程计(VO)，基于相邻帧之间的信息从而粗略的估计相机运动和特征。视觉里程计分为特征点法和直接法

2，把visual slam分为前端和后端。前端为视觉里程计和回环检测，是对图像数据进行关联。后端是对前端的输出结果进行优化，利用滤波或者非线性优化，从而得到最优的位姿估计和全局一致性地图

3，VO：研究图像帧间的变换关系完成实时位姿跟踪，对输入的图像进行处理，计算位姿变化，得到相机间的运动关系

4，视觉里程计的任务是 已知初始位置C0，通过上一时刻的位置Ck-1和Tk来计算当前时刻的位置Ck，其中Tk是k和k-1之间的变换矩阵

5，对于相邻的两张图片，判断相机在这两张图片之间的运动。对于特征点法，首先要对两张图片进行特征提取，也就是找到图片中特别的地方，比如角点，边缘点等，其次对这些特征点在两张图片之间进行特征匹配，把误匹配的点筛掉之后，利用特征点计算相机的位姿

6，位姿就是位置和姿态，位置在三维空间中有三个坐标，姿态是在三位空间中的旋转(r,p,y)，因此位姿包含6个自由度，

7，相机运动中，有4个常见的坐标系，
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

   [tu](https://nimg.ws.126.net/?url=http%3A%2F%2Fdingyue.ws.126.net%2F2022%2F0517%2F93bbb031j00rc179s00ffc000o000dim.jpg&thumbnail=660x2147483647&quality=80&type=jpg)



## Zemax



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




