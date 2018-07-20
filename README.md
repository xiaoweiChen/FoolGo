基于蒙特卡罗树搜索的围棋A.I.

目前只有在9路棋盘上表现出入门级棋力。

底层的数据结构和算法相当高效，在我的MacBook Air上1秒钟能跑4万局蒙特卡罗对局（多线程）。

关键方法：

* 并查集实现的棋串（简单的链表实现，若改为树结构，加上路径压缩，会更高效些，但对整体的表现应该影响不大）。
* 位或运算实现棋串『气』的更新。
* 棋盘的哈希算法用Zobrist哈希，通过哈希表存放每个状态的胜率等信息

在面向对象设计上，这个项目高度可扩展（参考了刘知青教授的《现代计算机围棋基础》），介绍主要的几个类：

* FullBoard类，功能完整的棋盘类，提供高效的落子方法等。
* Player抽象类，提供可扩展的棋步选择方法，子类如RandomPlayer，就是Player类的随机落子的实现。
* Game类，Player类的组合，比如子类MonteCarloGame就组合了两个RandomPlayer。

C++编码指南

* 本项目遵循google的guideline中的多数条目。
* 出于性能的考虑，本项目大量使用模板类，在编译期确定棋盘的大小，以便尽可能多地使用静态数组。
* C + class + 模板，不使用模板元编程。
* 用智能指针管理内存
* 用gtest做单元测试

有关N3LDG

* 本项目的深度学习部分采用经我魔改过（主要是针对每一类节点，实现了cuda部分，以期更好地压榨GPU性能）的N3LDG框架。
* N3LDG是一个用于自然语言处理的深度学习框架，支持动态计算图，C++实现。

## TODO

* 正实现policy network，俟国庆再续。
* 被value network要用的计算资源吓了一跳，如果谁有用有监督学习训练value network的思路，请不吝赐教！

## Make
* boost is required
* mkdir build && cd build
* cmake ..
* make

## 问题交流
* email : chncwang@gmail.com
* QQ群：823648893
