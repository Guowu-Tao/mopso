# 多目标粒子群算法简单实现

 * [算法流程](#算法流程) 
 
 ### （1）初始化粒子数量、迭代次数、存档阈值；初始化粒子速度、位置、适应度值、pbest、gbest、存档；初始化惯性因子、速度因子 

   初始化的pbest为粒子本身；存档即将非劣解存起来，非劣解就是无法严格对比出好坏，即有些目标好，有些目标差；gbest即从存档中随机选择一个，拥挤度越高被选择的概率越低<br>
   
   拥挤度计算公式：<br>
   
   ![密度计算](https://i.imgur.com/CebAhWp.png)
   
   根据拥挤度计算概率，拥挤度越高，被选择的概率越小：<br>
   
   ![概率](https://i.imgur.com/GhYXLo9.png)
 
 ### （2）更新速度、位置、存档、pbest、gbest、拥挤度
    
   ![速度更新公式](https://i.imgur.com/QzAj0kj.png)<br>
   ![位置更新公式](https://i.imgur.com/BU5iFFR.png)<br>
    
   更新存档：
- 根据支配关系进行第一轮筛选，将劣解去除，剩下的加入到存档中
- 在存档中根据支配关系进行第二轮筛选，将劣解去除，并计算存档粒子在网格中的位置
- 若存档数量超过了存档阈值，则根据自适应网格进行清除，拥挤度越高，被清除的概率越高，重新进行网格划分

 更新pbest：<br>
- 从当前新粒子和历史最优中选择支配粒子，如果不是支配粒子，随机选择一个

 更新gbest：<br>
- 存档中根据拥挤度随机选择一个（轮盘赌策略）
