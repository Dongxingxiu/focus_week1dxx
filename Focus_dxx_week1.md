# guthub及git入门

+ 相当于一个版本控制系统
+ 右键git bash打开命令行
+ 先初始化调整界面并配置用户名
  1. Git config --global user.name XXX
  2. Git config --global user.emal XXX@XXX.com配置邮箱（不需要真实存在）

+ 获取源代码命令: git clone http__（项目git链接）





# 机器人学--位置与姿态的描述

+ 坐标系的位置与方向统称为位姿
+ ![image-20230324113333622](https://github.com/Dongxingxiu/focus_week1dxx/blob/main/image-20230324113333622.png)

+ 相对位姿的表示与计算：

  ![image-20230324113540386](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324113540386.png)

  等式两边矢量一定闭合

  1. 等式两边同时乘以相对位姿的逆即可消除

  2. 任何相对位姿相对于0的相对位姿仍是本身

  3. 位姿复合运算中位姿不能随便交换

     ![image-20230324113915888](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324113915888.png)

     

## 2.1 二维空间位姿描述

为了在不同的参照系中表示点的位姿 --> 我们可以用旋转＋平移表示任意坐标系位置

1. 旋转：

   ![image-20230324203840409](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324203840409.png)

   + 将原坐标系B的X-Y方向的方向向量×旋转矩阵即可得到V的方向向量

   + 旋转矩阵的性质：

     标准正交矩阵：每列都是单位向量并且相互正交

     ![image-20230324204322172](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324204322172.png)

     

2. 平移与旋转结合：

   ![image-20230324204517078](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324204517078.png)

   相互平行的坐标系可以进行简单的向量相加，但是为了更简便的表达，我们将旋转矩阵扩充一个维度

![image-20230324204659152](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324204659152.png)

这样，通过扩充后的矩阵，我们可以只通过一个矩阵同时表示平移与旋转，我们记为T（齐次转换矩阵）

![image-20230324205101584](C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230324205101584.png)

<img src="https://img-blog.csdnimg.cn/20210609154632639.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTYzMjIyMA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:50%;" />

### 对旋转矩阵中负值的理解：

顺时针旋转会在矩阵中产生一个负值

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210609154935348.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTYzMjIyMA==,size_16,color_FFFFFF,t_70)



负值产生的原因：向量的点乘：

<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325100322095.png" alt="image-20230325100322095" style="zoom:67%;" />

**而个人感觉此处与线性代数联系紧密，旋转矩阵左右乘不能交换对应旋转顺序不同，结果不同**

**右乘旋转矩阵得到的坐标系经过同样对应顺序的左乘可以还原**



参考资料：https://blog.csdn.net/weixin_45632220/article/details/117735223?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167970832616800192299964%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=167970832616800192299964&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-5-117735223-null-null.142

## 2.2 robtics工具箱

工具箱包含函数和类，以矩阵、四元数、扭转、三重角和矩阵指数的形式表示二维和3D中的方向和姿势(SO(2)， SE(2)， SO(3)， SE(3))。工具箱还提供了在数据类型之间进行操作和转换的函数，如向量、齐次变换和表示三维位置和方向所必需的单位四元数。

除此之外，***Robotics System Toolbox***也可以实现机器人建模、运动学、动力学与控制的仿真计算。

对移动机器人和操作臂的运动学和动力学进行建模。使用[常用机器人模型](https://ww2.mathworks.cn/help/robotics/ref/loadrobot.html#mw_3b6f5928-5162-4696-90ba-121c354e177d)，或者导入 URDF 文件或 [Simscape Multibody™](https://ww2.mathworks.cn/help/robotics/ref/importrobot.html#mw_61d1a8e6-7616-4131-b41d-2a4d9217a4c9) 模型来创建自定义机器人模型。可视化和仿真机器人运动以验证自己设计的算法。

使用loadrobot功能可实现快速访问常见的机器人模型，该功能可加载商用机器人模型，如Universal Robots™UR10合作机器人、Boston Dynamics™Atlas人形机器人和KINOVA™Gen 3机械手。

可以使用loadrobot函数调用现有的机器人模型

```matlab
ur10 = loadrobot("universalUR10");

atlas = loadrobot("atlas");

gen3 = loadrobot("kinovaGen3","DataFormat","column");%在Matlab中输入上面的几行代码，就可以加载出自己所需的模型了。%loadrobot函数返回一个rigidBodyTree对象，该对象表示每个机器人模型的运动学和动力学。

disp(gen3)

show(atlas);%展示模型
```

<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325113819249.png" alt="image-20230325113819249" style="zoom:50%;" />



旋转的matlab可视化：

```matlab
T1=SE2(1,2,30*pi/180)%SE2函数得到旋转矩阵

axis([0  5 0 5]);

trplot2(T1,'frame','1','color','b')%画图表示

T2=SE2(2,1,0);

hold on

trplot2(T2,'frame','2','color','r')

T3=T1*T2%T3经过旋转与平移后得到

trplot2(T3,'frame','3','color','g')
```

<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325101216804.png" alt="image-20230325101216804" style="zoom:67%;" />





## 2.3 三维空间姿态描述

比二维空间多了z轴，满足向量叉乘

坐标轴的旋转方法：

+ 正交旋转矩阵


+ 旋转向量与欧拉角

  一共九个元素，但是自由度为三

  <img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325102319687.png" alt="image-20230325102319687" style="zoom:67%;" />

  <img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325103429344.png" alt="image-20230325103429344" style="zoom:67%;" />

  X-Y的旋转重合，丢失自由度

+ 旋转轴与角度



## 2.4 四元数

<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325112457840.png" alt="image-20230325112457840"  />

一般通过四元数与4*4齐次变换矩阵来用四元数同时描述平移与旋转

```matlab
T=transl(1,0,0)*trotx(pi/2)*transl(0,1,0)  %平移，旋转，平移

trplot(T)

t2r(T)

输出结果：
T =

     1     0     0     1
     0     0    -1     0
     0     1     0     1
     0     0     0     1


ans =

     1     0     0
     0     0    -1
     0     1     0

```

R = t2r(T)是齐次的正交旋转矩阵分量

T适用于SE(2)或SE(3)中的T

-如果T是4 × 4，那么R是3 × 3。

-如果T是3x3，那么R是2x2。

## 本章总结

<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325113655732.png" alt="image-20230325113655732" style="zoom:80%;" />





<img src="C:\Users\86155\AppData\Roaming\Typora\typora-user-images\image-20230325113714514.png" alt="image-20230325113714514" style="zoom:80%;" />













