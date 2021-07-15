# 文脉(ParCKG)

### 简介

“文脉”是清华大学人工智能研究院自然语言处理与社会计算研究中心推出的一个概率式关联可信中文知识图谱（Probablistic-like Association Reliable Chinese
Knowledge Graph, ParCKG）。该知识图谱主要依据中文维基百科条目间链接信息建立，即：以中文维基百科条目（entry）为实体（entity）构造知识图谱中的节点（node），以条目文章（entry article）中对其他条目的内部链接（internal link）构造从头实体指向尾实体的有向边（directed edge），以尾实体在头实体条目文章中提及次数TF和头实体关于维基百科的倒排文档次数IDF得到TF*IDF值，作为该有向边的权重，并归一化为转移概率（transition probability），最后形成一个带权有向图（weighted directed graph）。现将此知识图谱面对研究者和普罗大众进行开源，以期能对知识指导的自然语言处理以及其他下游任务有所襄助。

### 统计信息

我们从原中文维基百科的5441558个条目中筛选合并出了979951个实体[^1]，作为我们知识图谱中的节点。初步的维基百科链接图谱（CKG-ini）在这些节点上通过内部链接构造了16719189条有向边。在此基础上筛选得到的“文脉”(ParCKG)则保留了其中的15277295条边，去除率达到了8.62%。

### 展示页面

我们对我们所挖掘得到的“文脉”，还设计了展示页面，对实体间的相关关系进行可交互的演示，方便用户直观了解知识图谱的内部结构，其网址为https://williamlwclwc.github.io/KG-Demo/

### 文件结构

GitHub仓库文件目录如下：

```
|-- ParCKG
    |-- ParCKG_pagerank.csv
    |-- ParCKG_nodeinfo.csv
    |-- ParCKG_edgeinfo
    |   |-- ParCKG_edgeinfo_1.csv
    |   |-- ParCKG_edgeinfo_2.csv
    |   |-- ……
    |   |-- ParCKG_edgeinfo_20.csv
    |-- README.md
```

在其中，`ParCKG_nodeinfo.csv`储存的是每个节点与其实体名及别名（重定向名）的对应信息，而`ParCKG_edgeinfo`文件夹下储存的是每条链接的头实体，尾实体，转移概率等信息。因为总文件过大，故而分为了20个子文件，每个存储了一部分头实体对应的出边，合并则可得到所有的边的信息。而`ParCKG_pagerank.csv`存储了我们利用在此图上利用`networkx`工具包在将每个节点初始值定义为入度值情况下得到的PageRank值结果。

### 开源信息

我们将挖掘所得的“文脉”进行免费开源，您若利用了此成果撰写论文或编写软件，请进行如下引用：

“在我们的研究/应用中，我们利用了清华大学人工智能研究院自然语言处理与社会计算研究中心所开发的概率式关联可信中文知识图谱“文脉”ParCKG，其资源网址为[THUNLP-AIPoet/ParCKG (github.com)](https://github.com/THUNLP-AIPoet/ParCKG)。”

并引用如下论文：

```latex
@inproceedings{lin-etal-2015-modeling,
    title = "Modeling Relation Paths for Representation Learning of Knowledge Bases",
    author = "Lin, Yankai  and
      Liu, Zhiyuan  and
      Luan, Huanbo  and
      Sun, Maosong  and
      Rao, Siwei  and
      Liu, Song",
    booktitle = "Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing",
    month = sep,
    year = "2015",
    address = "Lisbon, Portugal",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/D15-1082",
    doi = "10.18653/v1/D15-1082",
    pages = "705--714",
}
```

### 贡献者

指导教师：孙茂松

开发人员：李文浩，刘文长

### 引用文献

1.Lin, Yankai, et al. "Learning entity and relation embeddings for knowledge graph completion." *Proceedings of the AAAI Conference on Artificial Intelligence*. Vol. 29. No. 1. 2015.

2.Lin, Yankai, et al. "Modeling Relation Paths for Representation Learning of Knowledge Bases." *Proceedings of the 2015 Conference on Empirical Methods in Natural Language Processing*. 2015.

[^1]:其中有2767个实体在维基百科官方实体列表中，但官方定义文本列表中并无对应的定义文本，故此部分实体出边为0，但因为仍然有实体有指向其的链接，故我们予以保留

