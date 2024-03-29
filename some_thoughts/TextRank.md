## TextRank 简介
TextRank由Mihalcea与Tarau于EMNLP'04 [1]提出来，其思想非常简单：
通过词之间的相邻关系构建网络，然后用PageRank(https://www.cnblogs.com/en-heng/p/6124526.html)
迭代计算每个节点的rank值，排序rank值即可得到关键词。
PageRank本来是用来解决网页排名的问题，网页之间的链接关系即为图的边，迭代计算公式如下：

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/PageRank.jpg)  

其中，PR(Vi)表示结点Vi的rank值，In(Vi)表示结点Vi的前驱结点集合，Out(Vj)表示结点Vj的后继结点集合，d为damping factor用于做平滑。

网页之间的链接关系可以用图表示，那么怎么把一个句子（可以看作词的序列）构建成图呢？
TextRank将某一个词与其前面的N个词、以及后面的N个词均具有图相邻关系（类似于N-gram语法模型）。
具体实现：设置一个长度为N的滑动窗口，所有在这个窗口之内的词都视作词结点的相邻结点；则TextRank构建的词图为无向图。
下图给出了由一个文档构建的词图（去掉了停用词并按词性做了筛选）：

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/PRgraph.jpg)

考虑到不同词对可能有不同的共现（co-occurrence），TextRank将共现作为无向图边的权值。那么，TextRank的迭代计算公式如下：

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/textRank.jpg)

可以看出，该公式仅仅比PageRank多了一个权重项Wji，用来表示两个节点之间的边连接有不同的重要程度。

在这里算是简单说明了TextRank的内在原理，以下对其关键词提取应用做进一步说明。

TextRank用于关键词提取的算法如下：

1)把给定的文本T按照完整句子进行分割，即

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Textrank_1.png)

2)对于每个句子Si属于T，进行分词和词性标注处理，并过滤掉停用词，只保留指定词性的单词，如名词、动词、形容词，即

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/TextRank2.jpg)

，其中 ti,j 是保留后的候选关键词。

　　3)构建候选关键词图G = (V,E)，其中V为节点集，由（2）生成的候选关键词组成，然后采用共现关系（co-occurrence）构造任两点之间的边，两个节点之间存在边仅当它们对应的词汇在长度为K的窗口中共现，K表示窗口大小，即最多共现K个单词。

　　4)根据上面公式，迭代传播各节点的权重，直至收敛。

　　5)对节点权重进行倒序排序，从而得到最重要的T个单词，作为候选关键词。

　　6)由5得到最重要的T个单词，在原始文本中进行标记，若形成相邻词组，则组合成多词关键词。

2.1 TextRank算法提取关键词短语

　　提取关键词短语的方法基于关键词提取，可以简单认为：如果提取出的若干关键词在文本中相邻，那么构成一个被提取的关键短语。

2.2 TextRank生成摘要

　　将文本中的每个句子分别看做一个节点，如果两个句子有相似性，那么认为这两个句子对应的节点之间存在一条无向有权边。考察句子相似度的方法是下面这个公式：
  
  ![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/TextRank3.jpg)
  
  公式中，Si,Sj分别表示两个句子词的个数总数，Wk表示句子中的词，那么分子部分的意思是同时出现在两个句子中的同一个词的个数，分母是对句子中词的个数求对数之和。分母这样设计可以遏制较长的句子在相似度计算上的优势。

我们可以根据以上相似度公式循环计算任意两个节点之间的相似度，根据阈值去掉两个节点之间相似度较低的边连接，构建出节点连接图，然后计算TextRank值，最后对所有TextRank值排序，选出TextRank值最高的几个节点对应的句子作为摘要。



3.对比总结：

TextRank与TFIDF均严重依赖于分词结果——如果某词在分词时被切分成了两个词，
那么在做关键词提取时无法将两个词黏合在一起（TextRank有部分黏合效果，但需要这两个词均为关键词）。
因此是否添加标注关键词进自定义词典，将会造成准确率、召回率大相径庭。
TextRank的效果并不优于TFIDF。
TextRank虽然考虑到了词之间的关系，但是仍然倾向于将频繁词作为关键词。
此外，由于TextRank涉及到构建词图及迭代计算，所以提取速度较慢。

发现以上两种方法本质上还是基于词频，这也导致了我们在进行自然语言处理的时候造成的弊端，
因为我们阅读一篇文章的时候，并不是意味着主题词会一直出现，特别对于中文来说，
蕴含的中心思想也往往不是一两个词能够说明的，这也是未来自然语言方面要解决的基于语义的分析，路还很长。

