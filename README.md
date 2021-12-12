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

1. **Cloth_Simulation**  
    - Lab分为两个模块，第一部分是基于弹簧系统的Implicit Cloth Solver，另一部分是利用Position-Based Dynamics(PBD)的布料模拟。(布料和球体的碰撞采用Impluse method处理)
        - **Implicit Solver**:
        	- 通过对隐式欧拉方法的方程进行变换，可以将隐式积分的求解问题转化为求一个特定的F(x)的非线性优化问题。
        	- 根据质点弹簧系统的性质，可以求出F(x)的梯度和二阶倒数(Herssian)，然后通过牛顿法进行迭代求解位置。其中，线性方程的求解使用Jacobi Method。
        - **Position-Based Dynamics(PBD)**:
        	- 先将布料中的顶点作为简单的粒子进行位置和速度的更新。
        	- 进行Strain limiting（Jacobi fashion），在一次迭代中，遍历每一条边并根据约束计算一个新的位置，最终对于每一个顶点，计算出其位置的平均值作为这次迭代之后的位置（可与初始位置加权)，根据位置的变化更新速度。
	- 运行：勾选cloth上对应的脚本，然后运行即可开始布料模拟，可以用鼠标拖动球体碰撞布料以更好的观察模拟的情况，可以通过alt+鼠标左键转动视角。
	- 演示的mp4文件也一并放在了文件夹中。
