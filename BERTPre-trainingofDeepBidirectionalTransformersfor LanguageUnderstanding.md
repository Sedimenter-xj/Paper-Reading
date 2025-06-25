# BERT:Pre-training of Deep Bidirectional Transformers for Language Understanding

 We introduce a new language representation model called BERT, which stands for Bidirectional Encoder Representations from Transformers. Unlike recent language representation models (Peters et al., 2018a;Rad fordet al., 2018),BERT is designed to pre train deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context in all layers. As a result, the pre-trained BERT model can be finetuned with just one additional output layer to create state-of-the-art models for a wide range of tasks,such as question answering and language inference,without substantial taskspecific architecture modifications.

BERT is conceptually simple and empirically powerful. It obtains new state-of-the-art results on eleven natural language processing tasks, including pushing the GLUE score to 80.5%(7.7% point absolute improvement), MultiNLI accuracy to 86.7%(4.6%absolute improvement),SQuADv1.1 question answer ingTest F1 to 93.2 (1.5point absolute im provement) and SQuADv2.0 Test F1 to 83.1 (5.1 point absolute improvement).

“Bidirectional” 的意思是“双向的”。在BERT里，“bidirectional”指的是模型在理解语言时，会同时考虑一句话中一个词左边和右边的上下文信息，而不是只从左往右或者只从右往左看。也就是说，模型是双向地理解句子里的每个词，能够捕捉到更多丰富的语义关系。

举个简单例子：
 句子“他**在银行**存了钱”，模型会同时关注“银行”左边的词“他”和右边的词“存了钱”，从而更准确理解“银行”是指金融机构，而不是河岸。

**deep bidirectional representations:**

- bidirectional:模型不仅看一个词左边的内容，也看它右边的内容，理解这个词在句子里的完整语义环境
- deep:这种理解不是只在表面做一次，而是在模型的多个隐藏层（很多层神经网络层）中反复进行，这样能捕捉更复杂、更抽象的语言特征。

**Question Answering（问答）**：指的是模型根据给定的文本（比如一段文章或知识库）来回答用户提出的问题。比如你给我一段文章，然后问我“这篇文章主要讲什么？”，模型就要从文章中找出答案。

**Language Inference（语言推理）**，也叫“自然语言推断”（Natural Language Inference，NLI）：指的是判断两个句子之间的关系，比如判断第二句话是不是第一句话的**蕴含**、**矛盾**，还是**中立**。比如句子A是“所有的猫都是动物”，句子B是“这只猫是一只动物”，模型要判断B是否由A蕴含。典型数据集有MultiNLI。

**GLUE（General Language Understanding Evaluation）**

- 一个由多个子任务组成的测试集合，用来全面评估模型的语言理解能力。
- 文本分类、句子配对、情感分析、自然语言推理等。
- 如果一个模型在GLUE得分高，说明它在很多种语言理解任务上都表现得很好。

**MultiNLI（Multi-Genre Natural Language Inference）**

- 一个专门用于**自然语言推理（NLI）**的任务。
- **任务目标**：给定一对句子（前提 + 假设），模型要判断假设是否是：
  - **蕴含**（entailment）
  - **矛盾**（contradiction）
  - **中立**（neutral）

**SQuAD v1.1（Stanford Question Answering Dataset）**

- 一个基于维基百科的问答数据集。
- **任务目标**：模型阅读一段文章，然后回答一个基于文章的问题，答案必须是**原文中的一段连续文本**。

**SQuAD v2.0**

- **是在v1.1基础上的升级版**
- **新加入的挑战**：增加了**无答案的问题**，即问题根本无法从文中回答。
- **模型任务**：不仅要回答正确的问题，还要学会判断某些问题是**没有答案的**。