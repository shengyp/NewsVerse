# NewsVerse
## 一、总体架构
### 1. 功能架构

![图1 系统架构](https://img-blog.csdnimg.cn/0d404f3b81064e5293b9f530c7c1efec.png#pic_center)


### 2.工程文件结构（java packages 结构）

![  图2 java packages结构](https://img-blog.csdnimg.cn/04f6b7a2bab9462a956210256acaaf2d.png#pic_center)


## 二、系统包结构详解
### 1. /bean包
  在系统的包结构中，/bean包下是一些java been对象。
  
   ![图3 /bean包结构](https://img-blog.csdnimg.cn/79a75237c5ae47329a74cacb539f155a.png#pic_center)

 ### 2. /coref包
 /coref包下存放了使用[Stanford的CoreNLP工具](http://stanfordnlp.github.io/CoreNLP/)，对单篇文档进行指代消解的代码（在实现时，主要用到了StanfordCoreNlpDemo2.java，StanfordCoreNlpDemo3.java，TextCorefer.java这3个文件，该子包下其它的文件只为测试之用），对应系统架构图中的Coreference Resolution部分。
 
![ 图4 /coref包结构](https://img-blog.csdnimg.cn/5c46faf8ae7f448d8fccfae32fa5c583.png#pic_center)

### 3. /model包
/model包下存放了两套fact filtering的代码，在/glpk子包下，存放了使用glpk原生lib实现fact filtering的算法，但由于上述lib的稳定性不够高（最直接的反应是同一套代码应用于不同的triples file，有些能算出结果，有些就算不出结果）。鉴于以上情况，在matlab中调用整数线性规划的接口实现了filter algorithm，并将相应的代码打成.jar文件，在/SMat包中通过java程序调用生成的jar文件（java调用matlab，在工程实现时用的正是本子包下的代码），进而能够与用java实现的业务逻辑相互关联。

![图5 /model包结构](https://img-blog.csdnimg.cn/5f81d5030c7e4cbeba3a3b40787035b1.png#pic_center)

### 4. /openie包
/openie包下存放了使用[OpenIE工具](https://github.com/knowitall/openie)对fact进行提取的代码，对应系统架构图中的Knowledge Extractor部分。

![图6 /openie包结构](https://img-blog.csdnimg.cn/9d66c84cdca947658c82fc3345f501f6.png#pic_center)

### 5. /parser包
/parser包下存放了对文档进行解析的代码，对应系统架构图中的Document Ranking部分。

![图7 /parser包结构](https://img-blog.csdnimg.cn/d9929029348b4b6e98c9bd88beeb85a6.png#pic_center)

### 6. /similar包
/similar包下存放了fact filter中对两个triple的相似程度进行比较的代码，其中NewsSimilarity.java为最主要的文件，/word2vec包下的为使用word2vec对语料进行训练，进而计算triple间相似度的代码，在实现时并未用到。

![图8 /similar包结构](https://img-blog.csdnimg.cn/1b67c4b644db47d290b2736f6997666c.png#pic_center)

### 7. /tools包
/tools包下存放了一些工具文件的代码。

![图9 /tools包结构](https://img-blog.csdnimg.cn/d93d090082134b60b23e085e58d3cdde.png#pic_center)



