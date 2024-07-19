# DOTSLearn

# 概览

## DOTS简介

### DOTS是什么？

DOTS全称 Data-Oriented Technology Stack，面向数据技术栈，实际为五个核心包定义的一种全新的Unity代码编写模型，在这些核心包外，还提供了一系列游戏功能相关的额外包和相关工具，是Unity面向数据设计与编程的一整套计数解决方案

包括：

C# Job System：多线程支持

Burst Compiler：优化C#代码编译器，可以编译比Mono和IL2CPP更快的代码

Unity Mathematics：可以在Job System中使用的数学库，在Burst Compiler中使用有特别优化

Unity Collections：提供常见的集合类型，在Job System中使用，支持安全检查

Entities(Entity-Component System)：为GameObject的更高效的替代品，与GameObject和MonoBehaviour不同，本身不承担任何代码，components只是数据片段集合，都有对应的system代码单元进行处理

其它包：

Entities.Graphics(Hybrid Renderer)：支持URP和HDRP的Entities渲染解决方案，可优化CPU性能

Netcode：DOTS网络解决方案

Physics：物理解决方案，有UnityPhysics和Hawk两个后端，UnityPhysics是无状态确定性物理库，适合多人网络游戏，Hawk是有状态不确定性物理库，更稳定强大

Animation(WIP)

Audio(WIP)



### DOTS的应用范围

大世界流式加载游戏

复杂大规模模拟游戏

多种网络类型多人联机游戏

客户都模拟预测网络游戏，如射击游戏

...



### DOTS学习途径

看：视频、官方文档、官方论坛DOTS区，官方Github例子

查：专业术语，相关概念，扩展资料

学：五大核心包，游戏扩展包，三方扩展包和工具

改：官方Github案例，Unity商店案例

调：官方Github案例，自己Demo

写：Demo

交流：官方论坛，社交媒体



## 面向数据设计DOD

### 需要思考的问题：

哪些数据需要绑定在一起，是一个概念还是有隐藏含义

如何设计数据布局，AOS/SAO，支持SIMD？

目标平台最小访问单位，CPU各级缓存大小

数据更新时间，一帧一次，还是一帧多次

如何访问数据，随机/连续还是stride或其它burst方式

总是修改数据还是读取数据，是修改所有内容还是只是一部分

哪些数据设计对带宽和延迟影响大



### 设计原则

先设计，后编码

为高效使用内存与缓存设计

为Blittable Data设计

为普通情况设计

使用迭代



## ECS架构

### 简介

实体组件架构，Entity Component System：

遵循组合优于继承的原则

面向数据设计

弱耦合

常用于游戏开发

Entity ：不是容器，是一个标识符，用于指示某个对象的存在，系统可以用其进行操作，可以通过分配组件来分配某些属性

Component ：组件是一个数据容器，没有任何逻辑，一组特定的参数关联在一起并定义属性

System：系统是负责对数据进行操作的部分，系统是对具有特定属性(组件)的特定实体执行操作



### 专有名词

Archetypes：标识符，标识拥有具有相同组件的实体

每个Archetype标记的内存，会被分成固定大小、连续的非托管内存块，称为Archetype Chunk，默认大小16KB

World：一系列Entity实体的组合，每个Entity在一个World中是唯一的，统一受到World中EntityManager管理

Structural Change：所有导致需要重新组织内存块或内存块内容的操作，都只能在主线程中操作，是资源密集型操作(Resource Intensitive)，效率低

添加或删除一个实体的组件，导致所属Archetypes(原型)发生变化，属于Structural Change

创建或销毁实体，设置Share Component值都被视为Structural Change

确定一定不会有Structural Change操作时，可以在运行时做Bake操作，提高效率

Query：查询



### Cache层级和排队管理

建议多次观看

https://www.bilibili.com/video/BV1kV4y1g7kA/?spm_id_from=333.788&vd_source=9bedd7b260a052e095df795440c0c591



## 核心包安装

安装Entities、Collection、



