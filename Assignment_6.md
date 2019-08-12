## 本次主要是探讨underfitting和overfitting的原因，附带一些解决办法
### 一.形成原因  
[参考资料1：wiki](https://en.wikipedia.org/wiki/Overfitting)  
[参考资料2：medium](https://medium.com/greyatom/what-is-underfitting-and-overfitting-in-machine-learning-and-how-to-deal-with-it-6803a989c76)  
**Underfitting**:wikipedia定义（渣翻），一个统计模型不能准确地抓住数据集的基本规律。  
欠拟合的形成原因，一般是模型过于简单了，如下图所示：
![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Underfit%201%20degree.png)

可以看出，数据用一次线性函数的模型拟合，基本不能描述数据特征，此时我们说模型的偏差（bias）很大---预测值与样本点距离过大，
方差（variance）---预测值基本不受样本点的影响。

**Overfitting**：wikipedia定义（渣翻），分析的产物（模型）与特定的数据集过于相关，
过于精确地拟合数据，可能导致不能对额外的数据做出很好的预测，失去了观测稳定性。
过拟合的曲线见下图：
![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Overfit%2025%20degree.png)  
可以看到，用25阶函数去拟合图形时，模型过于复杂，它可能对训练数据有较好的拟合，但是新的数据对它影响很大（或者说它没有泛化能力，不能有效抓住数据特点）

### 二.解决办法

* 使用K折验证（K-fold Cross-Validation）。  
e.g. K=5：把训练集切成5等份----尽量使数据均匀分布在五个子数据集中，
然后选择一个作为验证集，其余4个作为训练集。  
这样重复5次，我们由一组数据，得到五个训练结果，将各个训练结果取平均值，即可。  

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Five%20fold%20cross-validation.png)  

* 实际操作  
对于特定的一组数据集，我们可以采用1~40阶的函数----即40个函数去拟合它，然后分别求出交叉验证错误率，如下图所示，找出错误率最低的，即可。  

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Cross%20Validation%20Result.png)  
![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/CrossValidation%20Result%20Graph.png)  

可以看出，4阶方程的拟合误差最小。  
实际上，4阶方程确实能够最有效地抓住数据分布的特点，如下所示：

![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Balanced%204%20Degree%20polynomial%20model.png)  

## 三.进一步验证

为了进一步验证我们上述理论，我们将训练集和测试集的错误率曲线画出。
![image](https://github.com/Mikasathebest/NLP_learning/blob/master/images/Training%20and%20Testing%20Curves.png)   

可以看出，欠拟合的模型，它的误差在**训练集和测试集上都非常大**；过拟合的模型，**在训练集上误差很小、在测试集上误差很大**  
因此我们需要挑选出合适的模型，避免欠拟合和过拟合的发生

## 四.其他杂项

其实还有其他很多具体的方法解决上述问题，例如：  
* Overfitting  
加入惩罚性：L1、L2正则化  
全连接网络可以 Dropout  
降低模型复杂度，以及增加数据量  
加入噪声（输入加噪声、权值加噪声、网络响应加噪声）  
ensemble----结合多种模型，bagging：用不同模型拟合不同训练集； Boosting：使用简单神经网络，加权平均其输出  

* Underfitting  
增加其他特征项  
增加模型复杂度，例如加入二次项、三次项  
减少正则参数  

**Writing down three sceneries that machine learning has been used now**  
AlphaGo  
人脸识别  
广告推荐  

**Come out with three new sceneries with which machine learning may be applied**
NLP：理解文章语义   
CV：视频内容识别    
生物： 解析人体结构，例如大脑结构，细胞结构，蛋白质结构etc

