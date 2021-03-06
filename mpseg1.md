title: 最大概率汉语切分算法研究（一）词典构建
date: 2017-11-25 16:51:02
tags: [NLP, Python]

---

最近忙活了将近一个多月总算把计算语言学布置的最大概率汉语切分作业写完了，虽然中途一波三折，还发生了很多让人难忘的事情，所幸最后还是比较完整的写了出来，也学到了不少的知识。因此便有了这个系列的文章。

<!--more-->

# 问题

基于最大概率的汉语切分工具的开发，是要利用计算语言学课上学到的知识，选用合适的模型开发一个汉语分词的工具并且进行代码测试与评估。

# 阶段划分

一个完整的分词工具的开发包括以下几个步骤：

1. 选择合适的语料库
2. 根据语料库构建词典
3. 选择合适的分词模型和平滑技术
4. 语料库切分：训练集和测试集
5. 模型训练
6. 模型测试，包括分词技术调整等，增强代码健壮性

在本项目中选用的语料库是人民日报199801的语料库，分词模型选择2-gram 模型，平滑技术选用了最简单易行的加一平滑，分词技术包括了左近邻词，FMM 和 BMM 等，具体在接下来涉及到了再具体谈。

本文主要讨论的是从语料库构建词典的问题。

# TrieTree与词典

[TrieTree](https://baike.baidu.com/item/Trie/140945?fr=aladdin)，又名前缀词典树，是一个专门用于构建词典的数据结构，在这个数据结构上实现词语的添加和查找都可以获得非常高的效率。

## TrieTree 的 python 实现

在[知乎的一个回答](https://www.zhihu.com/question/21610353)有非常简短的代码可以实现 TrieTree 的添加和查找功能，不过在这里要用 Trie 树构建词典的话还需要小小的修改，将该回答中叶子节点的'Exist'字段替换成'count'，用于统计每个词在语料库中出现的次数，每次添加一个词的时候，为后面的概率计算作铺垫。

## 语料库分析

人民日报199801的语料库中，对于每一个词都是像`泽民/nr`这种形式，以`/`分割，前半部分为词，后半部分为该词的词性，词之间用两个空格进行分割。构建词典的时候，便可以读取语料库文件的每一行，用`split()`方法分割得到词列表，在每个词中再次执行分割获取每个词，添加到 Trie 树中，每次添加的时候首先进行判断，如果该词已经在树上，那么将该词的' count'字段计数加一，否则，将词加入到词典树中，并将计数字段设为1。

## 词典写入到文件

将词典写入到文件，其实就是遍历 Trie 树，每个包含‘count’键的节点对应于一个词，将这些词写入到文件中的过程。具体代码参考如下

```python
def foreachTree(TTree,string,file):
    if 'freq' in TTree :
        if len(TTree) == 1:
            print(string+' '+str(TTree['freq']),file=file)
            return
        else:
            print(string+' '+str(TTree['freq']),file=file)
            for kk in TTree:
                if kk == 'freq':
                    pass
                else:
                  	foreachTree(TTree[kk],string+kk,file)
    else:
        for kk in TTree:
            foreachTree(TTree[kk],string+kk,file)
```

对于树这种递归定义的数据结构，解决问题的最方便的方法自然也是递归，由于汉语词汇挂在“树”上的时候，每个节点都是单个“字”，因此需要一个 String 变量作为函数参数，记录前面的遍历状态。

要注意的地方是判断是否是完整词语的条件是‘count’或者‘freq’是否在该节点对应的字典中，而不是是否为‘叶子节点’。