## TF-IDF简介
TF-IDF（Term Frequency/Inverse Document Frequency）是信息检索领域非常重要的搜索词重要性度量；用以衡量一个关键词w对于查询（Query，可看作文档）所能提供的信息。  
词频（Term Frequency, TF）表示关键词w在文档Di中出现的频率：
<img src="http://latex.codecogs.com/gif.latex?\frac{\partial J}{\partial \theta_k^{(j)}}=\sum_{i:r(i,j)=1}{\big((\theta^{(j)})^Tx^{(i)}-y^{(i,j)}\big)x_k^{(i)}}+\lambda \theta_k^{(j)}" />


$$ TF_{w,D_i}= \frac{count(w)}{|(D_i)|}$$

其中，count(w)为关键词w的出现次数，|Di|为文档Di中所有词的数量。逆文档频率（Inverse Document Frequency, IDF）反映关键词的普遍程度——当一个词越普遍（即有大量文档包含这个词）时，其IDF值越低；反之，则IDF值越高。IDF定义如下：

$$ IDF_w = log \frac{N}{\sum_{i=1}^{N}I(w,D_i)}$$

其中，N为所有的文档总数，I(w,Di)表示文档Di是否包含关键词，若包含则为1，若不包含则为0。若词w在所有文档中均未出现，则IDF公式中的分母为0；因此需要对IDF做平滑（smooth）：

$$ IDF_w = log \frac{N}{1+\sum_{i=1}^{N}I(w,D_i)}$$

关键词w在文档Di的TF-IDF值：

$$ TF-IDF_{w,D_i} = TF_{w,D_i} * IDF_W$$

从上述定义可以看出：

* 当一个词在文档频率越高并且新鲜度高（即普遍度低），其TF-IDF值越高。
* TF-IDF兼顾词频与新鲜度，过滤一些常见词，保留能提供更多信息的重要词。
