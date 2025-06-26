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

 Language model pre-training has been shown to be effective for improving many natural language processing tasks(DaiandLe,2015;Petersetal., 2018a;Radfordetal.,2018;HowardandRuder, 2018).These include sentence-level tasks such as natural language inference(Bowmanetal.,2015; Williams et al., 2018) and paraphrasing (Dolan and Brockett,2005),which aim to predict the relationships between sentences by analyzing them holistically, as well as token-level tasks such as named entity recognition and question answering, where models are required to produce fine-grained output at the token level (TjongKim Sangand DeMeulder,2003;Rajpurkaretal.,2016).

### Fine-grained output:

### 在自然语言处理（NLP）中，它通常指：

- **不是一句话一个结果**，而是**对句子中的每个词或片段做判断**。
- 输出的结果更“精细”，可以逐个词地标注或处理。

------

### ✅ 举几个例子帮你理解：

#### 1. **命名实体识别（NER）**：

- 输入句子：**“比尔·盖茨是微软的创始人。”**
- 模型的 fine-grained 输出：
  - “比尔·盖茨” → 人名（Person）
  - “微软” → 组织名（Organization）

🔹 模型需要**对每个词作出细致分类**，这就叫“细粒度输出”。

------

#### 2. **问答任务（如SQuAD）**：

- 提问：**“谁创建了微软？”**
- 上下文：**“比尔·盖茨和保罗·艾伦在1975年创建了微软。”**
- fine-grained 输出：**“比尔·盖茨和保罗·艾伦”**

🔹 模型不仅要找出哪句话有答案，还要**精确提取出几个词**作为答案。

There are two existing strategies for applying pre-trained language representations to downstream tasks: feature-based and fine-tuning. The feature-based approach, such as ELMo (Peters etal.,2018a),uses task-specific architectures that include the pre-trained representations as additional features.The fine-tuning approach,such as the Generative Pre-trained Transformer (OpenAI GPT) (Radfordetal.,2018), introduces minimal task-specific parameters, and is trained on the downstream tasks by simply fine-tuning all pretrained parameters.The two approaches share the same objective function during pre-training,where they use unidirectional language models to learn general language representations.

### Downstream tasks:

在预训练语言模型（如 GPT、BERT）中，我们首先在大规模语料上训练一个通用模型，让它学会语言的基本规律。这叫做 **预训练（pretraining）**。

之后，我们会将这个预训练好的模型用于更具体的任务，比如：

- 文本分类（如情感分析）
- 命名实体识别（NER）
- 问答系统（QA）
- 文本生成
- 机器翻译
- 摘要生成

这些更具体、目标明确的任务，就被称为 **下游任务**（downstream tasks）。

We argue that current techniques restrict the power of the pre-trained representations, especially for the fine-tuning approaches. The major limitation is that standard language models are unidirectional,and this limits the choice of architectures that can be used during pre-training. For example,in OpenAI GPT,the authors use a left-to right architecture,where every token can only attend to previous tokens in the self-attention layers of the Transformer(Vaswanietal.,2017).Such restrictions are sub-optimal for sentence-level tasks, and could be very harmful when applying fine tuning based approaches totoken-level tasks such as question answering,where it is crucial to incorporate context from both directions.

### self-attention layers

**“自注意力层”** 或 **“自注意力机制层”**。

它指的是Transformer结构中用于计算序列内各个位置之间关系的层级，通过“注意力”机制让模型关注输入序列中不同位置的信息。

假设一句话是：“我 喜欢 吃 苹果”。

在自注意力层中，每个词都会看“自己”和句子里其他词的关系，决定自己应该关注哪些词的信息。

比如，词“吃”在计算它的表示时，会“注意”到“苹果”这个词，因为“吃”和“苹果”之间有强关联；同时它也会参考“我”和“喜欢”的信息，但权重可能没那么大。

具体来说，自注意力机制会为每个词计算一个权重分布，表示这个词对句中其他词的“关注度”，再根据这些权重综合其他词的信息，形成更新后的词向量。

“词向量”是自然语言处理（NLP）里非常重要的一个概念，简单来说就是把**词转换成数字表示**的一种方法。

具体解释：

- 计算机不能直接理解文字，它只能处理数字。
- 词向量就是把每个词转换成一个**固定长度的数字数组（向量）**，这样计算机才能处理和分析语言。
- 这个向量不仅仅是随机数字，而是经过训练，能够反映词的语义和上下文关系。
- 比如，“猫”和“狗”的词向量在数学空间中会比较接近，因为它们语义相似；而“猫”和“汽车”的词向量则相距较远。

举个例子：

“苹果”的词向量可能是这样的一串数字（这里只是举例）：
 [0.12, -0.05, 0.33, 0.87, ...]

“香蕉”的词向量也有类似的数字，但会和“苹果”更接近，而和“汽车”差别更大。

词向量的出现让机器能够“理解”词与词之间的关系，进而完成翻译、问答、文本分类等任务。

### fine tuning

具体来说：

- 微调是指在预训练模型的基础上，利用特定任务的小规模标注数据，进一步训练模型，让模型更好地适应这个具体任务。
- 例如，先用大规模无监督数据训练一个通用语言模型（预训练），然后用问答数据对这个模型进行微调，使它更擅长问答任务。

微调的好处是：

- 利用预训练的强大知识和表示能力，
- 快速适应具体任务，避免从零开始训练，节省时间和资源。

 In this paper,we improve the fine-tuning based approaches by proposing BERT: Bidirectional Encoder Representations from Transformers.BERT alleviates the previously mentioned unidirectionality constraint by using a “masked language model”(MLM)pre-training objective, inspired by theCloze task (Taylor, 1953). The masked language model randomly masks some of the tokens from the input, and the objective is to predict the original vocabulary id of the masked word based only on its context. Unlike left-to right language model pre-training, the MLM objective enables the representation to fuse the left and the right context, which allows us to pretrain a deep bidirectional Transformer. In addition to them asked language model,we also use  a “next sentence prediction” task that jointly pretrains text-pair representations.The contributions of our paper are as follows:

**“为什么要 mask 一些词？然后又让模型去预测它们？这是为了训练什么能力？”**

------

### ✅ 简单回答：

这是在训练模型学会**理解上下文，并捕捉语言中的语义和语法信息**。

------

### ✅ 具体解释：

1. **BERT 是一个预训练模型**，目标不是一开始就做分类、问答、翻译，而是先学会“看懂语言”。
2. 所以它用了一种类似**“填空题”**的方式训练模型理解语言结构：
   - 比如原句是：
      `The quick brown fox jumps over the lazy dog.`
   - 训练时它会随机遮住一些词，比如：
      `The quick [MASK] fox jumps over the [MASK] dog.`
   - 然后模型的任务是：**仅靠前后上下文猜出 `[MASK]` 是什么词**。
     - 第一个 [MASK] 应该猜出是 `brown`
     - 第二个 [MASK] 应该猜出是 `lazy`
3. **“预测单词的词汇 ID”** 其实就等于预测出它原本是哪个词（词汇表中的编号），本质是一个**分类问题**。

------

### ✅ 为什么这样训练有用？

因为：

- 如果一个模型能仅靠前后词，正确猜出被遮住的词，那说明它真的**理解了语言中的词序、语义、搭配**等知识。
- 它训练出的词向量、句子表示就非常有用，可以迁移到下游任务，比如情感分析、问答、命名实体识别等。

------

### ✅ 总结一句话：

> Mask 一些词再让模型预测，是为了让模型学会“填空”，从而学会理解语言的上下文、词义和语法规律 —— 这是 BERT 预训练的核心目标。

### ✅ 什么是 text-pair representations？

它指的是：
 👉 把一对文本（比如两个句子、一个问题+一个回答）**作为一组输入**，通过模型编码，得到它们**联合的语义表示**。

------

### ✅ 为什么需要它？

因为很多任务涉及两个文本之间的语义关系，例如：

| 任务类型               | 文本对示例           | 模型目的                   |
| ---------------------- | -------------------- | -------------------------- |
| **自然语言推理 (NLI)** | Premise + Hypothesis | 判断是否蕴含 / 矛盾 / 中性 |
| **问答 (QA)**          | 问题 + 段落          | 找出段落中能回答问题的部分 |
| **句子相似度**         | 句子1 + 句子2        | 判断两个句子语义相似程度   |
| **句子配对**           | 评论 + 回复          | 判断是否是合理的一对       |



这些任务都要求模型理解两个句子之间的**关系**，而不仅仅是独立理解某一个句子。

------

### ✅ BERT 怎么处理 text-pair？

BERT 的输入格式支持句子对结构：

```
css


复制编辑
[CLS] 句子A [SEP] 句子B [SEP]
```

- `[CLS]`：整个句子对的“摘要”表示，用来做分类
- `[SEP]`：分隔两个句子

BERT 通过注意力机制把两个句子混合建模，最后得到这对文本的“联合表示”，也就是所谓的 **text-pair representation**。

------

### ✅ 总结：

> “Text-pair representations” 就是模型对两个文本之间语义关系的建模和编码方式，是实现自然语言推理、问答、句子匹配等任务的核心表示方式。

We demonstrate the importance of bidirectional pre-training for language representations. Unlike Radfordetal.(2018),which uses unidirectional language models for pre-training,BERT uses masked language models to enable pretrained deep bidirectional representations.This is also incontrast to Peters et al.(2018a),which uses a shallow concatenation of independently trained left-to-right and right-to-left LMs.

We show that pre-trained representations reduce the need for many heavily-engineered task specific architectures. BERT is the first fine tuning based representation model that achieves state-of-the-art performance on a large suite of sentence-level and token-level tasks,outperforming many task-specific architectures.

