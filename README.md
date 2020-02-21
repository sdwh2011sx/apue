by r00tk1t 	2019/04/13

# UNIX环境高级编程

## 缘起

无论是Linux后台开发，还是嵌入式Linux，Linux系统编程都是重中之重。而《UNIX环境高级编程》(APUE, Advanced Programming in UNIX Environment)无疑是这个领域的圣经，是每位开发者必读的神作。精准的用语、精良的语言组织，经历了漫长岁月的千锤百炼，可谓无出其右。数年来，这本书曾被我反复摩擦，然而每次重温，都会有新的理解。

之所以做这样一份视频教程，主要是以下3方面原因：

1. 夯实自我。一门技艺，达到了传道授业解惑的境界，才勉强算得上登堂入室。闻之不如见之，见之不如知之，知之不如行之。
2. 虽然这个行业往往是“前人挖坑，后人骂娘”，但偶尔也要栽栽树。
3. 不能免俗地、留一些印记，证明我曾存在过。

## 说明

- 本教程不适合编程初学者，需要以下必备基础：
  - C程序设计语言
  - 基本的Linux操作知识
  - 对操作系统(OS, Operating System)有一定程度的认知
  - 流畅的英文阅读能力
- 本教程所有相关资料，包括书籍、脑图和源码都会上传到该repo，欢迎star/fork，欢迎提issue。
  - 书籍上传了中文第三版的电子书，但教程不会照本宣科，仅作为参考书提供。有能力的建议入手一本实体书
  - 选用脑图作为教学白板，放弃PPT，全面拥抱思维导图
  - 源码工程结构抽离自apue.3e，我做了裁剪和补充，使得初学者可以更为平滑的过渡。采用doxygen兼容的注释语法，可以更为便利地生成文档
- 录制的视频会上传到百度云网盘和B站，欢迎订阅，欢迎投币
  - 百度云网盘链接：
    - https://pan.baidu.com/s/1CTP-B-a_Rmy2cABcYt90Cg
    - 提取码: kj4b
  - Bilibili链接：
    - https://www.bilibili.com/video/av49771435?from=search&seid=6947952255864046916
- Ubuntu x64虚拟机+宿主机Win10，该repo本地仓库在虚拟机中，通过samba工具映射到Win10。使用VSCode做开发，虚拟机中调试。你可以自己随意折腾，我这样做是为了更好的观赏效果。

## 课程目录

### 第一部分：Linux基础知识

**理论基础**

1. UNIX基础知识(1课时)

   开篇第一讲，旨在对Linux系统编程有一个泛泛的了解，不要被我全程的吹比、天马行空的各种概念与延展所吓倒，随着课程的深入，全都可以有。这要是一不小心起到了“从入门到退坑”的效果，我是要向全国人民谢罪的。教程中也会提及Windows的知识来横向对比，这对从Windows转到Linux领域的开发者来说极有裨益（我当初就是Windows行至山穷水尽，转到Linux看秋水汪洋）两开花，两开花。

2. UNIX标准(1课时)

   本系列课程最水的一节，围绕UNIX C环境相关标准、实现与编译时/运行时限制进行了展开。本节课内容无需死记硬背，只需要有一个概念即可。apue.3e的该章节源码是一大亮点，课程中进行了一一阐述。

3. 无缓冲I/O(2课时)

   从本节开始，真正的踏入Linux系统编程领域，这一节主要是讲解了POSIX标准提供的文件I/O接口函数以及其背后的一些重要概念(如fd, 进程fd表，内存中文件表项等等)。

4. 标准I/O(2课时)

   ISO C标准本身也定义了一套I/O接口，对应于上一节的无缓冲I/O来说，它的实现是有缓冲的。这一节的很多内容会与C语言的学习有所重复，但对于Linux系统编程来说，我们需要更深入的了解在Linux环境下标准I/O的一些注意事项以及与无缓冲I/O的混用与联动。

5. 文件和目录(3课时)

   这一节主要围绕着Linux文件的概念进行展开，众所周知，从软件到硬件，从文本到可执行程序，Linux下万物皆文件。了解Linux文件系统背后的文件存储方式以及文件系统涉及的Linux内核架构对上层的学习有非常大的助力。另外，一些偏向于底层的知识如VFS、物理文件系统存储结构等我并没有在课程中做延展（尽管脑图中有些许痕迹），也不要求初学者课后掌握。春华秋实，等到步入内核殿堂的那一天，上层与底层的知识点也就自然而然的无缝衔接了。

6. 系统信息(1课时)

   这一节主要讲述了Linux一些系统信息文件相关的API，此外，对系统本身的信息以及时间相关的API也透过实例程序做了简明扼要的讲解。至此，第一部分的理论知识就全部讲完了。本节只有一课时，内容相对单薄，重要程度也不比3、4、5节的内容，但这并不是字多不看的借口。

**琢磨轮子**

- Busybox(2课时)

  Busybox将Linux常用的命令行工具打包处理，是嵌入式Linux软件开发商的好伙伴。Busybox本身开源，其代码结构与设计都堪称Linux系统编程的教科书。两节视频会为大家介绍Busybox开源项目，选取诸如chown,chmod,cp等命令行子程序展开源码解读，旨在让刚入门的小伙伴掌握阅读开源项目的手段、领略大师级程序的丰采。**重点强调，本课程不是Busybox的解读系列教程，仅仅只是一个入门向的指引。**想要琢磨Busybox细节的童鞋请自行google，当然我个人建议是直接啃源码就行了，啃不下来只能说明基本功不行。源码之前，了无秘密。

- 待续。。

### 第二部分：进程与信号

7. 进程环境(1课时)

   这一节主要讲述了进程的概念以及Linux环境下进程环境相关的信息。本章是入门Linux进程的起手式，相对比较简单，通过与C语言的main函数紧密结合，使得初学者更容易理解Linux进程的本质。

8. 进程控制(2课时)

   待续。。。

## 写在最后

欢迎各路大神提供建议，资料或视频中如果有错误的地方，还望斧正。

也欢迎喷子们前来撕逼，但要走流程，issue的大门永远敞开，某无畏无惧，当年国服第一喷。

