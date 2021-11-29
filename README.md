# GAMES103_HW_TEAFOX
* ***Homeworks for GAMES103-基于物理的计算机动画和模拟-王华民***
* 该课程仍在开展中，目前只布置了第一次作业，作业的脚本结果都在对应UnityPackage中。

***
## 环境
* **引擎**: Unity3D
* **语言**: C# Script
***

## 目录
1. **RigidBody_Simulation**  
    - 作业分为两个模块，一部分是基于物理的刚体模拟，一部分是基于Shape Matching的刚体模拟。（都用纯C#实现)
    - 两部分都使用leap-frog方法更新位置，前者更新角速度，速度，位置和旋转（四元数)，后者只用更新每个粒子的速度和位置并做约束。
    - 两者都采用impluse method做碰撞检测和响应(尝试过Penalty Method,效果不如impluse好).
    - 运行：勾选bunny的default mesh上对应的脚本，然后运行。基于物理的模拟按l开始，按r复位。
    基于Shape Matching的模拟按l开始，不支持复位。
    - 演示的mp4文件也一并放在了文件夹中。
