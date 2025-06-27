# Finding Structure in Time

> Time underlies many interesting human behaviors. Thus, the question of how to represent time in connectionist models is very important. One approach is to represent time implicitly by its effects on processing rather than explicitly (as in a spatial representation).The current report develops a proposal along these lines  first described by Jordan (1986) which involves the use of recurrent links in order to provide networks with a dynamic memory. In this approach, hidden unit patterns are fed back to themselves: the internal representations which develop thus reflect task demands in the context of prior internal states. A set of simula-tions is reported which range from relatively simple problems (temporal version of XOR) to discovering syntactic/semantic features for words. The networks are able to learn interesting internal representations which incorporate task demandswith memory demands: indeed, in this approach the notion of memory is inextri-cably bound up with task processing. These representations reveal a rich structure, which allows them to be highly context-dependent, while also expressing generalizations across classes of items. These representations suggest a method for representing lexical categories and the type/token distinction.

“**Connectionist models**” 中文通常翻译为：

> 🧠 **连接主义模型**

------

### 📚 定义：

连接主义模型是指一种**类脑神经网络**的建模方法，它模仿人脑中**神经元之间的连接方式**，来处理信息和学习规律。

也叫作：

- **神经网络模型**（尤其是早期）
- **并行分布式处理模型（PDP models）**，即 *Parallel Distributed Processing*

------

### 🧠 特点包括：

1. **由大量简单单元（神经元）组成**
2. 信息通过连接（权重）传播，连接强度随学习而更新
3. 处理是**分布式的**，不是靠规则、逻辑推理，而是模式激活
4. 特别适合处理**语言、记忆、感知、时间序列**等任务

------

### 💬 举例：

> Jordan 网络、Elman 网络、Hopfield 网络、现代 RNN、Transformer 等神经网络架构都是 connectionist models 的不同形式。

“temporal version of XOR” 通常指的是 **在时间维度上对信号或数据做异或操作**。

举例说明：

- 普通的 XOR 是在同一时刻对两个信号进行比较，输出它们的异或结果。
- temporal XOR 可能是指 **对同一信号在不同时刻的值进行 XOR**，比如用当前时刻的值与之前某个时刻的值做异或，这样可以捕捉信号的变化或时间上的差异。

> Time is clearly important   in cognition.  It  is inextricably  bound up with  many behaviors (such as language) which express themselves as temporal  sequences. Indeed, it is difficult to know how one might deal with such basic  problems as goal-directed behavior, planning, or causation without some  way of representing time. 

> The question of how to represent time might seem to arise as a special  problem unique to parallel-processing models, if only because the parallel  nature of computation  appears to be at odds with the serial nature of temporal events. However, even within traditional (serial) frameworks, the representation of serial order and the interaction of a serial input or output with higher levels of representation presents challenges. For example, in models of motor activity, an important issue is whether the action plan is a literal  specification of the output sequence, or whether the plan represents serial  order in a more abstract manner (e.g., Fowler, 1977, 1980; Jordan 8c Rosen-baum, 1988; Kelso, Saltzman, & Tuller, 1986; Lashley, 1951; MacNeilage,  1970; Saltzman & Kelso, 1987). Linguistic theoreticians have perhaps tended   to be less concerned with the representation and processing of the temporal  aspects to utterances (assuming, for instance, that all the information  in an  utterance is somehow made available simultaneously in a syntactic tree); but  the research in natural language parsing suggests that the problem is not  trivially solved (e.g., Frazier 8c Fodor, 1978; Marcus, 1980). Thus, what is  one of the most elementary facts about much of human activity-that   it has  temporal extend-is sometimes ignored and is often problematic. 

关于如何表征时间的问题，乍看之下似乎是并行处理模型所特有的一个特殊问题，仅仅因为并行计算的特性似乎与时间事件的串行性质相冲突。然而，即使在传统的（串行）框架中，串行顺序的表征以及串行输入或输出与更高层次表征之间的交互，也带来了挑战。

例如，在运动行为的模型中，一个重要的问题是：动作计划是否是对输出序列的逐项明确指定，还是以更抽象的方式表征串行顺序（例如，Fowler, 1977, 1980；Jordan 和 Rosenbaum, 1988；Kelso、Saltzman 与 Tuller, 1986；Lashley, 1951；MacNeilage, 1970；Saltzman 和 Kelso, 1987）。

语言学理论家们或许较少关注言语中时间方面的表征与处理（例如，假设一句话中的所有信息以某种方式同时在句法树中呈现）；但自然语言解析方面的研究表明，这一问题并非可轻易解决（例如，Frazier 和 Fodor, 1978；Marcus, 1980）。因此，尽管人类许多活动的一个最基本事实是——它具有时间延展性——这一点有时却被忽视，而且往往是个难题。

“**Parallel-processing models**”（并行处理模型）是指一种**模拟或描述大脑或计算系统中多项处理同时进行的模型**。它是相对于传统的“串行处理模型”（serial processing models）而言的。

------

## 🧠 通俗解释：

当我们处理信息时，有两种方式：

- **串行处理**：一步一步来，比如排队买票，一个人处理完才轮到下一个；
- **并行处理**：多个任务同时进行，比如多个窗口同时售票，每个窗口并行处理。

------

## 📘 在认知科学中的含义：

在**心理学、神经科学或连接主义（connectionism）**中，parallel-processing models 主要指：

> **多个认知过程或神经信号在大脑中**可以**同时发生、互相影响**，而不是一个接一个地依次发生。

例如：

- 看一幅图画时，大脑可以**同时处理颜色、形状、运动方向等多个维度**；
- 听语言时，可以**同时识别音素、语调、语义背景**。

------

## 💻 在人工智能 / 神经网络中的含义：

在机器学习或神经网络中，**parallel-processing models** 指的是：

> **多个神经元（或节点）同时接收和处理输入信号**，反映了人脑神经元的并行结构。

例如：

- **前馈神经网络（Feedforward Neural Networks）**
- **卷积神经网络（CNN）**
- **Transformer 模型中的 self-attention**（每个 token 同时关注其他所有 token）

这些模型都不是按“一个单元完成任务后再交给下一个”的串行方式工作，而是**层内或网络内大量并行运算**。

>In  parallel distributed  processing models, the processing of sequential inputs has been accomplished in several ways. The most common solution is to attempt to “parallelize time” by giving it a spatial representation. However, there are problems with this approach, and it is ultimately not a good  solution.  A better approach would be to represent time implicitly rather  than explicitly. That is, we represent time by the effect it has on processing  and not as an additional dimension of the input.

在并行分布式处理模型中，顺序输入的处理已经通过多种方式实现。最常见的解决方法是尝试通过赋予时间以空间表示来“并行化时间”。然而，这种方法存在一些问题，最终并不是一个很好的解决方案。一个更好的方法是隐式地表示时间，而不是显式地表示。也就是说，我们通过时间对处理产生的影响来表示时间，而不是将时间作为输入的一个额外维度。

>This article describes the results of pursuing this approach, with particular emphasis on problems that are relevant to natural language processing.  The approach taken is rather simple, but the results are sometimes complex  and unexpected. Indeed, it seems that the solution to the problem of time  may interact with other problems for connectionist architectures, including  the problem of symbolic representation and how connectionist representations encode structure. The current approach supports the notion outlined  by Van Gelder (in press) (see also, Elman, 1989; Smolensky, 1987, 1988), 
>that connectionist representations may have a functional compositionality  without being syntactically compositional.

本文描述了采用这种方法所得到的结果，重点关注与自然语言处理相关的问题。这种方法本身相当简单，但结果有时却是复杂且出人意料的。事实上，时间问题的解决方案似乎与连接主义架构中的其他问题相互影响，包括符号表示的问题，以及连接主义表示如何编码结构的问题。当前的方法支持 Van Gelder（待出版）所提出的观点（另见 Elman, 1989；Smolensky, 1987, 1988）：连接主义表示可能具有功能性的组合性，而非句法上的组合性。

> The first section briefly describes some of the problems that arise when  time is represented externally as a spatial dimension. The second section  describes the approach used in this work. The major portion of this article  presents the results of applying this new architecture to a diverse set of prob-  lems. These problems range in complexity from a temporal version of the  Exclusive-OR function to the discovery of syntactic/semantic  categories in  natural language data. 

🚀 “Temporal version of XOR” 是什么？
当提到“时间版本的 XOR”时，意思是：

当前的输出值依赖于前一个时间点的输入值和当前输入值之间的异或关系。

