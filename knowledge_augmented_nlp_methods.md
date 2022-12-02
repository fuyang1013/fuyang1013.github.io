# 借助知识来增强NLP模型的方法

> create time: 2022-12

在大规模预训练模型出现之后，NLP开始越来越频繁地谈论“知识”。知识是模型获取常识、逻辑和其他外部信息的关键。下面将通过一些SOTA工作来介绍如何把知识应用在NLU、NLG和常识推理上。

### 1. 介绍NLP和知识

近年来，更大的模型、更好的训练策略和更多的数据三者结合，极大地推动了NLP的发展，如BERT、RoBERTa和GPT. 这些预训练模型可以有效地从文本中学到语言模式并生成高质量的、上下文感知的表征。然而，这些模型的输入只有原文本，因而很难获取到和概念、关系、常识相关的外部世界知识。

本文用“知识”表示那些对模型预测目标输出很重要但是在当前模型输入中缺失的外部信息。知识对语言表征非常重要，理应融入到模型的训练和推理当中。知识也是实现高阶智能不可或缺的组成部分，也是在输入文本上统计学习无法获取到的。

### 2. NLU中的知识

NLU任务的目的是在输入文本的基础上对词、短语、句子、篇章的属性做预测，比如情绪分析、命名实体识别和文本推理。从知识资源的维度可将知识增强NLU大致分为两类，一类是结构化知识（如知识图谱），另一类是非结构化知识（如文本语料）。

将结构化知识融入到NLU的工作又可分为两种，一种是基于概念或者实体嵌入的显式方法[^zhang2019][^peters2019][^liu2020][^yu2020a][^zeng2020]，一种是通过实体遮掩预测的隐式方法[^sun2019][^shen2020][^xiong2020][^wang2019]。

比如，ERNIE[^zhang2019]使用TransE在知识图谱上显式地预训练实体嵌入，而EAE[^fevry2020]将其作为模型参数来学习。KEPLER[^wang2019]基于描述文本使用预训练模型来隐式地计算实体嵌入。

最近，一些工作提出联合训练知识图谱模块和语言模型。比如JAKET提出使用知识模块来生成文本中实体的嵌入，而用语言模型来生成知识图谱中实体和关系的上下文感知的初始嵌入。Yu等人[^yu2020c]和Xu等人[^xu2021]提出使用词典描述作为额外的知识源 来做NLU和常识推理任务。

将非结构化知识融入NLU模型，一般需要一个文本检索模块来从知识语料中获取相关文本。使用非结构化知识有很多方法，尤其是对于开放领域的问答任务。比如Lee第一个通过ICT(inverse cloze task)来训练retriever，然后联合训练retriever和reader用于开放领域的问答；DPR通过监督学习训练retriever在开放领域问答上取得了更好的成绩；REALM预测遮掩的包含重要实体的span来联合预训练reader和retriever；KG-FiD提出在检索阶段通过检索文章之间的结构化关系来过滤噪声文章。

### 3. NLG中的知识 

NLG的目标是从各种形式的语言或非语言数据（如文本数据、图像数据和结构化知识图谱）中生成人类语言的可理解文本。和NLU方法不同的是，NLG方法一般都采用encoder-decoder框架，在生成过程中，如果在解码下一个token时引入知识会面临很多挑战。

当前将知识融入NLG模型的方法大概分为三种：
- 通过模型结构融入知识，比如知识关联的注意力机制，知识关联的拷贝/指针机制
- 通过训练框架融入知识，比如posterior regularization, constraint-driven learning, semantic loss, knowledge-informed weak supervision；
- 通过推理方法融入知识，在推理时增加不同的知识约束来指导解码，比如lexical constraints, task-specific objectives, global inter-dependency；

如果从知识源的维度划分，

结构化的知识融入方法可以划分以下四种：
- 将预先计算的知识嵌入注入语言生成
- 通过三元组信息将知识迁移到语言模型
- 通过路径寻找策略来实现知识图谱推理
- 用图神经网络来提高图嵌入；

非结构化的知识融入方法可以划分为以下两种：
- 用检索信息来指导生成
- 将背景知识建模到文本生成中


4. NLP常识和推理

这里暂不赘述。

5 总结文章列表

- 知识增强NLU：[^zhang2019][^peters2019][^liu2020][^ding2019][^lv2020][^yu2022b]
- 知识增强NLG：[^zhou2018][^zhang2020a][^ji2020b][^lewis2020][^wang2021]
- 常识和推理：[^lin2019][^ma2019][^fan2020][^liu2021b][^wang2021][^guan2019][^guan2020b]
- 相关综述：[^yu2020b][^yang2021][^zhang2022][^wei2021]

6 代表人物

- Chenguang Zhu
- Yichong Xu
- Xiang Ren
- Bill Yuchen Lin
- Meng Jiang
- Wenhao Yu

[^zhang2022]: A survey of multi-task learning in natural language processing: Regarding task relatedness and training methods
[^wei2021]: Knowledge enhanced pretrained language models: A compreshensive survey
[^yang2021]:  A survey of knowledge enhanced pre-trained models
[^wang2021]: Retrieval enhanced model for commonsense generation
[^xu2021]: Fusing context into knowledge graph for commonsense reasoning
[^liu2021b]: Kg-bart: Knowledge graph-augmented bart for generative commonsense reasoning
[^yu2022b]: Jaket: Joint pre-training of knowledge graph and language understanding
[^fan2020]: An enhanced knowledge injection model for commonsense generation
[^guan2020b]: A knowledge-enhanced pretraining model for commonsense story generation
[^yu2020b]: A survey of knowledge-enhanced text generation
[^yu2020a]: Identifying referential intention with heterogeneous contexts
[^lewis2020]: Retrieval-augmented generation for knowledge-intensive NLP tasks
[^ji2020b]: Language generation with multi-hop reasoning on commonsense knowledge graph
[^lv2020]: Graph-based reasoning over heterogeneous external knowledge for commonsense question answering
[^fevry2020]: Entities as experts: Sparse memory access with entity supervision
[^xiong2020]: Pretrained encyclopedia: Weakly supervised knowledge-pretrained language model
[^shen2020]: Exploiting structured knowledge in text via graph-guided representation learning
[^zeng2020]: Tri-train: Automatic pre-fine tuning between pre-training and finetuning for sciner
[^yu2020c]: Dict-bert: Enhancing language model pre-training with dictionary
[^zhang2020a]: Grounded conversation generation as guided traverses in commonsense knowledge graphs
[^liu2020]: K-BERT: enabling language representation with knowledge graph
[^zhang2019]: ERNIE: Enhanced language representation with informative entities
[^sun2019]: Ernie: Enhanced representation through knowledge integration
[^wang2019]: Kepler: A unified model for knowledge embedding and pretrained language representation
[^peters2019]: Knowledge enhanced contextual word representations
[^guan2019]: Story ending generation with incremental encoding and commonsense knowledge
[^ding2019]: Cognitive graph for multi-hop reading comprehension at scale
[^ma2019]: Towards generalizable neuro-symbolic systems for commonsense question answering
[^lin2019]: Retrieval enhanced model for commonsense generation
[^zhou2018]: Commonsense knowledge aware conversation generation with graph attention
