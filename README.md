柴宁 id_github：time-pervades
学号：202000460129

Project: implement the naïve birthday attack of reduced SM3
Project: do your best to optimize SM3 implementation (software)

1.birthday-attack
实验环境：python 3.8 64-bit

首先过程中需要用到sm3算法来获取杂凑值，所以参考了一个博客实现了一个python版的sm3加密算法；
因为16位二进制数的哈希值，产生碰撞的可能性为1/65535，即若有65537个用户，那么一定会发生碰撞，所以在实现的时候：
①首先随机生成两组包含2^16个数的集合，并对两组数据分别作为sm3的输入来获取两组杂凑值集合
②求出两组集合的合集，若合集不为空，则发生了碰撞，攻击成功。

运行截图：
![`)BOW8N2$}{@835U2L)WN@K](https://user-images.githubusercontent.com/105587393/182006661-7930acf2-d6fd-4e22-8e4c-0c3921e4333b.png)

2.SM3-SIMD
实验环境：VS2019

首先优化之前，需要编写一个sm3算法：
  ①sm3算法开始之前，因为VS没有进制转换函数，所以预编写了一些“进制转换”、“与或非”相关操作的函数；
  ②然后，sm3算法，包含两个主要内容：函数填充、迭代压缩，而迭代压缩又包含消息扩展、压缩函数，这两个又分别包含...（sm3的详细过程都有，不详细介绍了）；
  ③代码优化，根据提示，使用SIMD指令集中的函数对代码进行优化：
（因为忽略了SIMD只能对整型/浮点型进行类似循环展开的加速，即存储需要使用数组，而代码主要使用string型，所以需要原始代码需要大改，在这里只给出关键部分SIMD加速代码）

运行截图：
![image](https://user-images.githubusercontent.com/105587393/182007481-2592c51c-7179-4582-abe4-8f7f1099d8ad.png)
