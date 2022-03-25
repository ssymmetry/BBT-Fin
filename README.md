
<p align="center">
<a href=""><img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpro.statics.techuangyi.com%2F2018%2F06%2F21%2Fzt7NJjTG5r8PsHyY5SS3aw6b.jpg%3Fx-oss-process%3Dimage%2Fresize%2Cm_lfit%2Cw_1366%2Ch_0&refer=http%3A%2F%2Fpro.statics.techuangyi.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1650599174&t=cc22a495c7d6574cad47c1060626ef46" align="middle" width = "600"></a>
</p>

<a href=""><img src="https://img.shields.io/badge/python-3.8+-aff.svg"></a> <a href="https://www.ssymmetry.com/"><img src="https://img.shields.io/badge/Inc-SuperSymmetry%20Technologies-blue"></a> <a href=""><img src="https://img.shields.io/badge/OS-Linux-green"></a> <a href=""><img src="https://img.shields.io/badge/CEO-Hengkui%20Wu-red" align="right"></a>

## 简介

1. 自然语言方面
    - 语言，作为人类意识的载体，交流的媒介，是人工智能领域最重要的研究对象。
    - 自然语言处理(NLP)是以语言为对象，利用计算机技术来分析、理解和生成自然语言的一门学科。常见应用有文本分类，情绪分析，自动摘要，机器翻译，信息抽取等
    - 在深度学习时代， NLP所面临的最大难题在于，语言的抽象程度相对其他模态数据过高，不通过海量的标注数据无法使神经网络学会理解语言任务，在一般情况的数据量下模型的指标难以达到落地应用的水平。
2. 预训练语言模型方面
    - 预训练语言模型的提出是NLP领域划时代的进展。预训练语言模型的诸多开创者指出，语言本身可以通过自监督的形式进行学习，例如可以通过把完整的句子，通过随机遮蔽掉一部分再进行完形填空的方式训练神经网络理解语言，摆脱人工标注数据的束缚
    - 这种自监督的方式使得我们可以在海量无标注数据上训练模型。以预训练语言模型Bert-chinese为例，其在约14G的中文文本上进行训练，相当于阅读了几万本长篇小说。
    - 预训练语言模型已经事实上成为自然语言处理与认知智能的基础设施。而预训练语言模型的能力，与其参数规模和训练文本规模直接相关，越来越多的公司投入大量财力训练语言模型，不断推高其参数规模上限。

## 动机
- NLP+金融需求广阔：情绪分析，事件监测，信息抽取，自动摘要，自动写作
- 蓝海市场：目前金融领域预训练语言模型屈指可数 

## 各个版本及参数量介绍
- base:2.2亿
- XL:30亿

### Big Bang Transformer(BBT) T5
- 站在巨人的肩膀上
- T5模型由谷歌提出，是预训练语言模型的里程碑式进展之一。它开创性的提出可以把所有NLP任务归纳在一个统一的Text to Text框架内，无论是翻译，问答还是情绪分析，都可以通过输入任务提示+文本，返回答案文本的方式统一处理（如图1），这一建模方式极大的方便了迁移学习和人机交互的进行。
- 通过这一创新，BBT T5模型在语言理解评测基准SuperGLUE上成功接近人类的表现。
- BBT T5共有Base,Large,XL,XXL四个版本，分别对应220M,770M,3.3B和10B参数规模
- 我们目前已经训练完成Base版，正在训练XL版。

<p align="center">
<a href=""><img src="http://n.sinaimg.cn/translate/524/w976h348/20191025/88d1-ihmipqw7045979.png" align="middle" width = "600"></a>
</p>

- 为了使BBT T5能够更好的理解中文金融领域的文本，我们爬取了海量公开数据，收集整理了百G规模的公司公告，研究报告，财经新闻与网络论坛数据，形成了中文金融语料库BBT Corpus
- 在BBT Corpus上预训练出的BBT T5-Base，相对于普通文本上训练出来的T5，在金融评测任务上取得了显著提升。
- 在此基础上，我们还挖掘了知识增强和课程学习两大创新点：
    1. 知识增强：
        - 研究表明，由于知识在普通文本中的稀疏性，阅读过大量文本的语言模型虽然对语言非常熟悉，但在知识层面上仍然像是一个文盲。我们使用复旦大学开发的大规模中文知识图谱对语言模型进行知识增强训练，在多项任务上取得了提升。



### Big Bang Transformer(BBT) CUGE
- 为了验证我们模型在金融NLP任务上的先进性，也为了填补行业标准的空白，我们搜集、整理和标注形成了包含八个数据集的中文金融自然语言理解与生成评测基准BBT CUGE
- BBT CUGE涵盖了关系抽取、事件抽取、事件主体识别、负面消息判定及负面主体判定、新闻标签分类、自动化新闻摘要，论坛情绪分析和命名实体识别八类任务
- 下面我们将会展开介绍BBT CUGE

### Big Bang Transformer(BBT) QA
- 由百度篇章级事件抽取数据集DUEE-Fin转化而来，输入一段文本，针对其中发生的事件类型和事件角色进行提问，要求模型根据文本回答问题。
- 实例介绍
    - 输入：
    ``` json
    {"text":"下文中发生的事件类型有哪些？新浪港股讯，众安集团(0.248,-0.00,-0.80%)（00672.HK）发布公告，于2019年10月15日，公司耗资94.56万港元回购380.5万股，回购价格每股0.248-0.249港元。"}
    ```
    - 输出：'股份回购'
    ***
    - 输入:
    ``` json
    {"text":"股份回购事件对应的主体有哪些？新浪港股讯，众安集团(0.248,-0.00,-0.80%)（00672.HK）发布公告，于2019年10月15日，公司耗资94.56万港元回购380.5万股，回购价格每股0.248-0.249港元。"}
    ```
    - 输出:'众安集团'

### Big Bang Transformer(BBT) RE
- 财经新闻句子级关系抽取任务
- BBT RE是一个人工精标注的财经金融领域的数据集。给定句子和其中的头尾实体，要求模型预测头尾实体之间的关系。该数据集由新浪财经新闻语料标注得到，其中命名实体为商业公司，在关系上设计了除NA类之外的44个金融领域的关系类别（双向），包含拥有、持股、竞争、收购、交易、合作、减持等财经金融领域的特有关系类别。
- 实例介绍
    - 输入：
    ``` json
    {"text":"东方航空AH股临时停牌传将与上航合并","head":"东方航空","tail":"上航"}
    ```
    - 输出:
    ``` json
    {"label":"合并"}
    ```

### Big Bang Transformer(BBT) ESE:事件主体抽取
- 本评测任务的主要目标是从真实的新闻语料中，抽取特定事件类型的主体。即给定一段文本T，和文本所属的事件类型S，从文本T中抽取指定事件类型S的事件主体。
- 实例介绍
    - 输入:
    ``` json
    {"text":"公司A产品出现添加剂，其下属子公司B和公司C遭到了调查"}
    ```
    - 输出:
        - 对应的事件:产品出现问题
        - 对应的主体:公司A

### Big Bang Transformer(BBT) NSP:金融负面信息及主体判定
- 该任务分为以下两个子任务
    1. 给定一条金融文本和文本中出现的金融实体列表
    2. 负面信息判定
        - 判定该文本是否包含金融实体的负面信息。如果该文本不包含负面信息，或者包含负面信息但负面信息未涉及到金融实体，则负面信息判定结果为0。
- 负面主体判定:
    - 如果任务1中包含金融实体的负面信息，继续判断负面信息的主体对象是实体列表中的哪些实体。

- 实例介绍
    - 输入:
    ``` json
    {"text":"????#恒丰银行与小资钱包1[超话]##小资钱包涉嫌诈骗[超话]#七问经侦，小资钱包出借受害人期待执法透明：  1.冻结小资平台账户多少钱？  2.有没有追查北京正聚源通鼎信用管理有限公司，控制孙正、伟强、张赛相关涉案资产？  3.我们出借人的银行流水显示那么多第三方支付，进一步加大追赃力度，同时追缴小资 ?????"}
    ```
    - 输出：
    ``` json
    {"entity":"小资钱包;恒丰银行;北京正聚源通鼎信用管理有限公司","label":1,"negative_entity":"小资钱包;北京正聚源通鼎信用管理有限公司"}
    ```

### Big Bang Transformer(BBT) NL:新闻标签
- 财经新闻多标签分类，共有:中国、公司、能源、债券等11个标签
- 评价指标:F1
- 实例介绍
    - 输入：
    ``` json
    {"text":"市场消息：韩国监管机构表示，苹果公司已针对监管应用商店运营商的新法律提交了合规计划。"}
    ```
    - 输出：
        - '外国、公司'

### Big Bang Transformer(BBT) NA:新闻摘要
- 主要为财经新闻摘要
- 评价指标:rouge-1,rouge-2,rouge-L的F值均值
- 实例介绍
    - 输入:
    ``` json
    {"text":"天宇股份公告，预计2021年半年度归属于上公司股东的净利润1.7亿元-2.3亿元，同比下降39.68%-55.41%。公司主营产品沙坦类原料药受低端市场激烈竞争影响，原料药销售价格较去年同期下降；子公司山东昌邑一期项目和京圣药业生产基地建设完成，进入试生产阶段和达产阶段，产能利用率没有完全释放，生产成本阶段性较高等原因导致报告期毛利率较上年同期下降。"}
    ```
    - 输出:
        - '天宇股份：半年度净利润预降40%-55%'

### Big Bang Transformer(BBT) FE:论坛文本情绪
- 股票论坛文本情绪分类
    - 情绪指数等级
        |积极|中性|消极|
        |:---:|:---:|:---:|
        |1.0|0.5|0.0|
- 评价指标:准确率
- 案例介绍
    - 输入:
    ``` json 
    {"text":"十倍股，鱼跃就是其中之一。具有世界大企业之雏形，加上科研不断提升，投资收益颇丰为跨越式发展打下财务基础。先备足粮草，再一统天下"}
    ```
    - 输出:
        - 1 (意味语料语境为积极面)

### Big Bang Transformer(BBT) NER:命名实体识别
- 介绍：
    1. 命名实体一般指的是文本中具有特定意义或者指代性强的实体，命名实体识别任务则是从文本中识别出特定类别的命名实体并将其归类到相应的类别中。
    2. 细粒度命名实体任务不满足于常见的NER实体类别，如人名，机构名等，将实体的类别扩展、细化到较细粒度。
- 评价指标介绍:
    - 本评测任务旨在从多种来源的金融文本中识别出细分的十一种实体类别，如公司，政府机构，产品，行业等。
- 案例介绍
    - 输入:
    ``` json
    {"text":"沈峰表示,蔚来期望自己的合作伙伴可以集中在自己的工厂周围,70%的供应链企业在合肥工厂的600公里范围内,92%的零部件采购来自合作伙伴的中国工厂"}
    ```
    - 输出(可视化后)：
        |人物|公司|行业/领域|国家/地区|
        |:---:|:---:|:---:|:---:|
        |沈峰|蔚来|供应链企业|中国|


### 汇总
|model\dataset|BBT RE关系抽取|BBT ESE事件主体|BBT FE论坛情绪|BBT NSJ负面主体|BBT NA新闻摘要|BBT NL新闻标签|BBT RC阅读理解|BBT NER实体识别|AVG|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|T5-base|58.29|88.88|76.28|87.91|51.29|87.19| | |74.97|
|BBT T5-base|62.32|**90.73**|**80.05**|88.50|52.00|91.18| | |77.46|
|BBT T5-base-KS|63.59|90.39|79.23|**89.05**|**53.74**|**91.40**| | |**77.90**|

### 创新点罗列
- 知识增强
    1. 微软，创始人，比尔盖茨[SEP]比尔盖茨于19XX年创建了微软公司
    2. 随机mask三元组中的一元或两元

