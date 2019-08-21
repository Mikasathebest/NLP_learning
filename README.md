# NLP learning code
NLP相关代码 学习

<details>
<summary>Assignment 1</summary>

* 定义语法，建立句子生成器   
* 由豆瓣影评训练语言模型，评估上面生成的句子   

</details>

<details>
 <summary>Assignment 2 </summary>

* 爬虫，爬取北京地铁数据
* 得到地铁数据，构建地铁网路  
* 用不同的搜索方式对地铁网路进行搜索（DFS BFS） 

</details>

<details>
<summary>Assignment 3</summary>

* 由sklearn得到Boston房价  
* 随机生成参数法，拟合房价  
* 给予一定方向后，拟合房价  
* 梯度下降法，拟合房价  
* 改变Loss函数后，拟合房价  
* 动态规划，解决切管子问题  
* 解析edit distance的解法（solution）
 
</details>

<details>
<summary>Assignment 4</summary>

* 下载中文维基百科，构建语料库
* 数据处理： 删减不必要的信息、繁体简体转换、切词
* 通过word2vec将文本进行转换： 词语—>向量  
* 绘制词云  
* 使用kaggle的T-SEN进行词向量可视化 

</details>

<details>
<summary>Assignment 5</summary>

* 读取新闻语料库，清理、切词
* 进行Word2Vec转换
* 对比：基于Word2Vec向量找近义词、基于图搜索找近义词 
* TFIDF找文本关键字  
* 绘制词云  
* 对文件进行TFIDF向量化  
* 词搜索引擎：朴素搜索、基于TFIDF排序搜索

</details>

<details>
<summary>Assignment 6</summary>

* 机器学习初步
* Overfitting & Underfitting
* ML应用

</details>

<details>
<summary>Assignment 6</summary>

* 目标：判别一篇新闻的来源是否为新华社
* 重点：样本中有 87% 来源是新华社，因此低于87%的的判别可以认为是无效的
* 方法：TFIDF向量化、Precision； Recall； F1 Score ；ROC AUC score
* 对以下方法均计算了上述参数： Logistic Regression、KNN、SVM、Naive Bayes、Random Tree、 Random Forest
* 最后在87052篇新闻中，找出了180篇疑似抄袭的新闻

</details>

