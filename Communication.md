title: 通信的基础——大学这三年到底学了啥（主线课程篇）
date: 2016-03-08 22:33:57
tags: Communication
---
# 前言

每次跟其他专业的同学聊天的时候往往会被问到，“你们通信工程这个专业到底是学些啥的”，之前回答这个问题的时候一直都是支支吾吾，实在惭愧。到了这个学期，在几乎所有的专业基础课都学完的时候，总算可以稍稍整理一下这个问题了。
<!--more-->
# 正文

整理的第一件事，就是明确通信的概念。通信，就是说白了就是实现两点之间的信息传输。所以就字面上看，着眼点并不多，主要在于怎么表示信息和怎么传的问题。

本文的写作思路根据学校培养方案给出的每个学期开设课程的时间顺序来叙述。这两年多来学的课程庞杂，近乎无所不包，这里先整理出与通信最密切相关的课程来整理一下。



## 信号与系统
这是通信工程专业首先接触的一门与“通信”这个概念密切相关的专业基础课。在这门课中，我们首先接触到了“信号”这个概念。

平时我们现实生活中听到的声音，看到的图像，每一个场景，都是信息。目前受到技术的各种限制，这样的信息是没办法直接传输的（这么传输可能需要无限的带宽，需要极强的抗干扰性能，等等）。目前基于电的形式运作的通信系统只能传输“电”，所以，引入了“电信号”的概念。

好了，有了电信号的概念，一切就方便了，因为“电”这个东西的很多特性是从19世纪就开始有所研究的。于是，就有了各种用函数表示的确定信号。

只有函数表示的信号是没有用的，就像在二进制代码中只知道1和0而不了解上下文一样。要怎么对这些信号进行处理呢？这个时候引入了三大变换：傅立叶变换，Laplace变换和Z变换。三个变换的本质都是将时域信号转换成变换域进行分析处理。这些变换一个主要目的就是将时域中繁琐的卷积操作转换为变换域相成操作，为分析运算带来巨大的方便。

关于变换域概念的理解，是理解系统的一个先决条件。我们都是生活在时域世界，简单来说就是一切按照时间顺序发展和变化的，这样的缺点就是在自己的角度没办法“高屋建瓴”的去分析问题，所以很多小说为了描述整个故事，都会有并行支线，描写同一个时段不同人物的活动，还利用各种叙述方式。变换域也是同样的道理，拿傅立叶变换（时域频域变换）来举例，可以理解成在同一时间点有不同频率的分量同时活动，傅立叶变换的目的，就是把这样一个个“人物”抽离出来进行分析处理。

说完变换域之后，终于可以到“系统”这个词了。我记得通信原理老师的一句经典名言“通信里面对信号所有的处理都可以理解成滤波器。”滤波器是一个具体的系统，也就是说，“所有系统的本质就是对信号进行各种处理”。这个处理，通常是频域的，对某个频域分量进行操作，比如“砍掉”一部分分量，“强化（增益）”某些分量，等等。
## 数字信号处理
DSP，俗称“大山炮”，是通信主线课程的第二门专业基础课，顾名思义，在这门课上，讨论了“数字信号”的分析问题。

在信号与系统中，所有的信号都是“模拟”的，也就是时域连续，取值连续的信号。模拟信号的缺点就是无法用计算机进行处理。

数字信号，就是时域离散，而且取值离散的信号。数字信号可以通过模拟信号“取样，保持，量化”得到，在坐标系上表现出来就是一个个离散的点。

为了对数字信号的分析处理，引入了离散时间傅立叶变换和离散傅立叶变换的概念。DTFT是时域离散，变换域连续的，DFT是时域离散，变换域离散的。考虑到“系统”是对信号在变换域中进行处理，DFT更适合用计算机对信号进行分析处理。

## 随机信号分析
这门课讨论的重点是随机信号。这样做的实际背景是在实际通信系统中，信号都是随机的，我们永远不能预测别人下一句话会说什么；另外，在传输过程中会收到噪声的干扰，噪声也是一种随机信号。然而，之前学过的课程都是针对确定信号，也就是有确定数学表达式的信号的。所以我们有必要讨论如何处理随机信号，这样才能讨论信号的传输过程。

随机信号没有确定的数学表达式，这并不意味着在这些信号面前无计可施。在这门课程中，一个极为重要的地方就是引入平稳随机过程的概念，基本思想就是虽然在某一时间点我们不能确定信号的表达式，但如果以时间差为自变量，就可以将某一类随机过程转变为确定的函数表达式进行讨论了。这类随机过程，就是平稳随机过程。

讨论平稳随机过程引入了相关函数的概念，从物理意义上来看，这是两个信号表达式的乘积，因此在变换域中不能像以前那样用幅度谱来讨论了，在此引入了功率谱。

把要讨论的主角介绍完毕之后，就是就此引出的几个相关概念，其中最为挥之不去的就是加性高斯白噪声和匹配滤波器这两个牛鬼蛇神了。
## 通信原理
有了前面一系列的铺垫，各种概念定义表达式粉墨登场之后，终于迎来了这个专业基础课的最终“BOSS”，有多重要？之前的几乎所有课程都只讨论了“信”的来龙去脉，这门课着重在“信”的基础上研究“如何通”，讨论了所有情形之下的信息传输过程，把之前涉及的几乎所有相关知识串联起来，打通天地线，实现真正的通信大业。

因为学习这门课的时候，学院已经把前三章大部分内容抽离到随机信号分析课程了，所以很快就进入了对传输的讨论当中。首先是模拟信号的传输，在讨论中引入了调制和解调的概念，本质上就是实现信号在频域上的搬移，也为以后的讨论打下基调。

讨论完模拟信号的传输之后，就来到这整本书的重点，数字信号的传输。数字信号的传输包括了基带传输和频带传输。跟模拟信号不同的是，数字信号在基带和频带传输中都要进行调制的。因为理想的数字信号是冲激信号的线性组合，频带带宽无限带，根本没法直接传输，要所以进行脉冲编码调制，将其绝大部分能量集中在受限的带宽（成为“主瓣”）中，使传输成为可能。既然是传输，自然会受到噪声的影响，这里终于轮到“加性高斯白噪声”登场了。这种噪声特殊的地方就是在所有频段有相同的取值（就像Gundam里面GN粒子产生全频段电磁波干扰一样。。。）。这种噪声可以非常好的模拟信道传输过程中受到的“热噪声”等的特性，所以将会是整个讨论信号传输过程中的半个“主角”，在讨论信噪比时都默认收到的噪声是加性高斯白噪声。

另外就是匹配滤波器的概念。通过匹配滤波器，将接收信号的高斯噪声限值在传输带宽所覆盖的频域之内，使接收信噪比能够达到最大。

基带传输讨论完毕之后，就是数字信号的频带传输，具体的调制过程和模拟信号的调制过程有异曲同工之妙。真正特别的地方，就是为了提高信道利用效率而引入M进制调制的概念。

之后，就是在本学期学到通原2中学到的关于信息编码处理和信道编码等内容，由于刚开始学习，所以暂且不表。

# END
原本以为可以简要介绍，但不知不觉就来了废话一堆，能够把一个专业的核心问题说清楚真的不是什么轻而易举的事情，能够整理下来发现大学两年多也并非一无所获。等有时间了继续把其他光怪陆离的课程整理一下，也是对本科四年的一个交代罢了。

纰漏之处，还希望留言指正:-)