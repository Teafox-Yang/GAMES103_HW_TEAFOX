# GAMES103_HW_TEAFOX
* ***Labs for GAMES103-基于物理的计算机动画和模拟-王华民***
* 该课程仍在开展中，目前只布置了前两次任务，Lab的脚本结果都在对应UnityPackage中。

***
## 环境
* **引擎**: Unity3D
* **语言**: C# Script
***

## 目录
1. **RigidBody_Simulation**  
    - Lab分为两个模块，一部分是基于物理的刚体模拟，一部分是基于Shape Matching的刚体模拟。（都用纯C#实现)
    - 两部分都使用leap-frog方法更新速度和位置，前者更新角速度，速度，位置和旋转（四元数)，后者只用更新每个粒子的速度和位置并利用刚体的特性做约束。
    - 两者都采用impluse method做碰撞检测和响应(尝试过Penalty Method,效果不如impluse好).
    - 运行：勾选bunny的default mesh上对应的脚本，然后运行。基于物理的模拟按l开始，按r复位。
    基于Shape Matching的模拟按l开始，不支持复位。
    - 演示的mp4文件也一并放在了文件夹中。

2. **Cloth_Simulation**  
    - Lab分为两个模块，第一部分是基于弹簧系统的Implicit Cloth Solver，另一部分是利用Position-Based Dynamics(PBD)的布料模拟。(布料和球体的碰撞采用Impluse method处理)
        - **Implicit Solver**:
        	- 通过对隐式欧拉方法的方程进行变换，可以将隐式积分的求解问题转化为求一个特定的F(x)的非线性优化问题。
        	- 根据质点弹簧系统的性质，可以求出F(x)的梯度和二阶倒数(Herssian)，然后通过牛顿法进行迭代求解位置。其中，线性方程的求解使用Jacobi Method。
        	- 采用切比雪夫加速方法来加速迭代的收敛，让相同的迭代次数下的模拟效果更好。
        - **Position-Based Dynamics(PBD)**:
        	- 先将布料中的顶点作为简单的粒子进行位置和速度的更新。
        	- 进行Strain limiting（Jacobi fashion），在一次迭代中，遍历每一条边并根据约束计算一个新的位置，最终对于每一个顶点，计算出其位置的平均值作为这次迭代之后的位置（可与初始位置加权)，根据位置的变化更新速度。
	- 运行：勾选cloth上对应的脚本，然后运行即可开始布料模拟，可以用鼠标拖动球体碰撞布料以更好的观察模拟的情况，可以通过alt+鼠标左键转动视角。
	- 演示的mp4文件也一并放在了文件夹中。

3. **FVM_Simulation**  
	- Lab的目标是使用有限体积方法（Finite Volume Method)实现对于弹性体的模拟，给定的模型为四面体网格，因此主要是计算四面体在特定形变时的F(deformation gradient),然后通过系列计算得到P(the first Piola-Kirchhoff stress),最终计算得到每一个顶点在该四面体中所应收到的力，通过显式积分的方式实现速度和位置的更新。
	其中，对于P的计算采用了两种实现方式：
		- **Elastic Forces**:
        	- 通过得到的F矩阵，计算(Green strain)G=1/2(F.transpose\*F-I)
        	- 通过计算得到的G，计算(the second Piola-Kirchhoff stress)S=2s1\*G+s0*trace(G)\*I
        	- 最终得到P=FS
        - **Method using SVD**:
        	- 对形变矩阵F进行奇异值分解[U,S,V]=svd(F)，其中S即表示拉伸的对角矩阵。
        	- 通过StVK的方式来，利用S矩阵的奇异值s1,s2,s3，计算得到W
        	- 最终计算得到P=Udiag（dW/ds1,dW/ds2,dW/ds3)V.transpose
    - 运行：勾选house上对应的脚本，然后运行即可开始FVM弹性体模拟，通过鼠标拖动视角，按空格可给物体一个向上的速度。
	- 演示的mp4文件也一并放在了文件夹中。

4. **Wave_Simulation**  
    - Lab的目标是根据Shallow wave function实现浅水水体的模拟以及水体与刚体的交互，
    给定的水体实际上是一个网格平面，通过推导得到的浅水微分方程来更新水体的高度场从而实现水体的模拟。
        - **Ripples**:
            - 秉承Finite Differencing的思想来计算导数，根据前一刻的高度场来估计后一时刻的高度场。
            - 将边缘视作墙体(Neumann boundary) hi+1=hi
        - **One-way coupling**:
            - 计算方块排开水对水体的影响，经过过推导后，实际上是解一个线性方程组。
    - 运行：勾选wave脚本，然后运行即可开始水体模拟，通过拖动水中的方块即可观察模拟效果。
    - 演示的mp4文件也一并放在了文件夹中。


