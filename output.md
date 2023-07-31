---
tip: translate by openai@2023-07-31 08:23:01
On the Development of Reactive Systems\*
D. Harel and A. Pnueli
Department of Applied Mathematics The Weizmann Institute of Science
Rehovot 76100, Israel
January, 1985
---

## Abstract

Some observations are made concerning the process of developing complex systems. A broad class of systems, termed reactive, is singled out as being particularly problematic when it comes to finding satisfactory methods for behavioral description. In this paper we recommend the recently proposed statechart method for this purpose. Moreover, it is observed that most reactive systems cannot be developed in a linear stepwise fashion, but, rather, give rise to a two-dimensional development process, featuring behavioral aspects in the one dimension and implementational ones in the other. Concurrency may occur in both dimensions, as orthogonality of states in the one and as parallelism of subsystems in the other. A preliminary approach to working one’s way through this “magic square of system development is then presented. The ideas described herein seem to be relevant to a wide variety of application areas.

> 本文就复杂系统开发过程中的一些观察作出了报道。其中，一个被称为反应系统的广泛类别在寻找行为描述的满意方法时被特别挑出来。我们在这里推荐最近提出的状态图法作为这一用途。此外，观察到大多数反应系统不能以线性逐步的方式开发，而是产生一个二维的开发过程，一个维度是行为方面，另一个维度是实现方面。并发可能发生在这两个维度上，一个是状态的正交性，另一个是子系统的并行性。然后，提出了一种初步的方法来完成这个“系统开发的魔方”。这里描述的思想似乎与各种应用领域都有关联。

## Why Another Paper on System Development?

The literature on software engineering, programming languages, and system and hardware design, is brimming with papers describing methods for specifying and designing large and complex systems. Why then are we writing yet another one?

> 软件工程、编程语言、系统和硬件设计的文献充斥着描述大型复杂系统规范和设计方法的论文。那么，我们为什么还要写另一篇呢？

In many kinds of computation-oriented or data-processing systems, sometimes characterized as sequential or functional systems, there is, for the most part, consensus as to the basic philosophy for design. For more complex systems, involving many concurrently executing components, which at times integrate software and hardware, there is much less of an agreement. As we argue below, this is due to an essential difference between two kinds of systems that makes the process of developing the more complicated of the two inherently more difficult. Indeed, we would like to think of the present paper as primarily containing an attempt to clarify sone of the underlying notions which seem to us to be fundamental. In passing, we shall attempt to address such issues as the kinds of systems that require new ideas, and the gaps such ideas ought to fill.

> 在许多计算导向或数据处理系统中，有时被描述为顺序或功能系统，大部分人都认同其设计的基本理念。但是，对于涉及许多同时执行组件的更复杂的系统，其中有时会整合软件和硬件，人们的意见则不尽相同。正如我们在下面讨论的，这是由于两种系统之间的本质区别，使得开发更复杂的系统变得困难得多。实际上，我们希望将本文主要看作是一种尝试，旨在澄清我们认为基本的概念。在此过程中，我们将尝试解决诸如需要新思想的系统类型以及这些思想应该填补的空白等问题。

## Which Systems are Problematic?

We would like to state from the start that by “systems” we do not wish to restrict ourselves to ones which are software-based, hardware-based or so-called computer-embedded. The terminology we shall be using is general enough for these and others, and so we shall not be specific about the final form the implementation of the system takes.

> 我们想从一开始就声明，当我们提到“系统”时，我们不仅仅指基于软件、硬件或所谓的嵌入式计算机的系统。我们使用的术语足以涵盖这些系统以及其他系统，因此我们不会具体说明系统实施的最终形式。

In many circles it is common to try to identify the features characterizing "difficult” systems; that is, the ones for which special methods and approaches are needed. Resulting from these efforts are various dichotomies distinguishing the easily-dealt-with systems from the problematic ones. Some people (e.g. in the programming language semantics community) have put forward the deterministic/nondeterministic dichotomy, systems for which the next action is uniquely defined can be easily defined, while nondeterminism requires special treatment. Others (such as certain verification researchers) have suggested that the problems lie in perpetual systems, whereas terminating ones are easy. Additional dichc omies that have been suggested are the synchronous/asynchronous, “lazy / real-time, and off-line/on-line ones, and what is perhaps the most popular one: the sequential/concurrent dichotomy. Indeed, concurrency gives rise to problems that are quite different from the ones sequential systems present, and there are entire schools of thought devoted to solving the problems raised by the presence of concurrently operating elements.

> 在许多圈子里，人们常常试图确定“困难”系统的特征，即需要特殊方法和方法的系统。这些努力产生了各种二分法，将容易处理的系统与有问题的系统区分开来。一些人（例如编程语言语义界）提出了确定性/非确定性二分法，可以轻松定义下一个动作唯一定义的系统，而非确定性需要特殊处理。其他人（如某些验证研究人员）建议，问题在永久系统中，而终止系统是容易的。还有其他建议的二分法，如同步/异步，“惰性/实时”和脱机/在线，以及可能最受欢迎的序列/并发二分法。事实上，并发产生的问题与序列系统所带来的问题完全不同，有整个思想学派致力于解决由并发元素引起的问题。

Fig. 1: A transformational Fig. 2: A reactive system as a “black cactus’ system as a black box

> 图 1：变换系统 图 2：作为“黑仙人掌”系统的反应性系统

As it turns out, all the dichotomies mentioned are real and the problem.^' more difficult members of each pair present are mdeed — We system accepts inputs^ P'\_"™ °e“n the definition of a transfor-also"^ may ask for ad—inpuU aM/or speak, with its environment.

> 结果发现，所有提到的二分法都是真实的，而更困难的一方则是转换系统，它接受输入，并且可以与其环境进行交流。

Annint the reader should observe that reactive systems cohere From micXve ovens and digital watches, through man/machine based software systems, siljcono^2;nrgO^e“d complex

> 读者应该注意，反应系统从微型烤箱和数字手表，到基于人机的软件系统，硅谷的复杂系统都是相互关联的。

The transformational reactive dichotomy cuts across all the aforementioned ones: both types of systems can be deterministic or not, terminating or not, on-line or not, and contain concurrently executing components or not. Also, reactive systems can be required to respond in real-time or not, and the cooperation of their components can be required to be synchronous or not. What then is so important about the distinction we are making, and why are we claiming that it is the reactive nature of systems that is problematic?

> 转换反应二分法贯穿了所有上述系统：这两种类型的系统可以是确定性的或非确定性的，可以是终止性的或非终止性的，可以是在线的或不在线的，也可以包含同时执行的组件或不包含。此外，反应系统可以被要求实时响应，或者不要求实时响应，其组件的合作也可以要求是同步的或不同步的。那么，我们正在做出的区分有什么重要性，为什么我们声称系统的反应性是有问题的？

## What is the Problem?

The answer to these questions seems to us to be rooted in the notion of the behavior of a system. While the design of the system and then its construction are no doubt of paramount importance (they are in fact the only things that ultimately count) they cannot be carried out without a clear understanding of the system’s intended behavior. This assertion is not one which can easily be contested, and anyone who has ever had anything to do with a complex system has felt its seriousness. A natural, comprehensive, and understandable description of the behavioral aspects of a system is a must in all stages of the system’s development cycle, and, for that matter, after it is completed too.

> 答案似乎植根于系统行为的概念。虽然系统的设计和构建无疑是至关重要的（实际上它们是唯一真正重要的东西），但如果没有清楚地理解系统的预期行为，就无法实施它们。这一断言不容易受到质疑，任何曾经接触过复杂系统的人都会感受到它的严重性。在系统开发周期的所有阶段，以及完成后，都需要一个关于系统行为方面的自然、全面和可理解的描述。

Taking a very broad and abstract view, we may describe a typical top-down development process as a sequence of transformations:

> 采取一个非常广泛和抽象的视角，我们可以将典型的自上而下的开发流程描述为一系列转换：

```
s(°)) -+ (MW, sP>) ---------► (M^, s('))
```

The structure studied at each level is a pair (M^\_\ S^) comprising a specified system at the i’th level of detail; is the i’th level physical, or implementational. description, and is the behavioral specification. At the top level might be highly underspecified, with using such vague terms as “a data-base system responding to conjunctive queries”, “a plane for interception”, etc. Each level, even the O’th one, needs some description of the interface of the system with its environment. This can be done by including a list E^ in each of the M^, containing descriptions of those input and output channels, signals, requests and responses, that constitute the system’s interaction with the “outside world”. The level of detail in the interface lists can also vary with i, from highly abstract items such as “request communication” or “display target”, all the way down to concrete lists of buttons, levers, displays and alarms. The corresponding behavioral specification should characterise the desired behavior of •the system, in as complete a manner as possible, using the elements of

> 在每一层级研究的结构是一对（M^\_\ S^），包括在 i 级别的指定系统；是物理的 i 级别，还是实施的。描述，是行为规范。在最高层可能是非常不具体的，使用诸如“响应联合查询的数据库系统”，“拦截飞机”等模糊术语。每一层，甚至是 O’th 层，都需要一些系统与其环境的接口描述。这可以通过在 M^中包含一个列表 E^来完成，其中包含构成系统与“外部世界”交互的输入和输出通道，信号，请求和响应的描述。接口列表中的细节级别也可以随着 i 的变化而变化，从高度抽象的项目，如“请求通信”或“显示目标”，一直到具体的按钮，杠杆，显示器和警报列表。相应的行为规范应该以尽可能完整的方式描述系统的期望行为，使用元素。

```
Any development step progressing from level i to level i + 1 must include a verification of the consistency of with This is true
■ ' -ktllW IIP™^' :- ''1' '1 "\_ °f PO86ib'e
:::s«X” ™ .—■»■ »• •«-—■\*■•
transformations on the specification.

To be .lightly more specific,™ - think of a
„ 8 “Hack cactus\* of X XX Ue set E; see
of this caotys are^ simply the interfac give rise to a
```

Fig. 2. A behavioral description S of thsystem S

set consisting of the legal se= J^vior should boil down to events and conditions. Thus, descri g words over E of course, defining a subset of the set of finiU.for if timing is important, this P element in the sequence, or example by attaching a time s amp but for now specifying the by specifying the timing constraints sepa y, e and S, holds for sequences will suffice. This relationship between E the level-dependent versions M<‘), E^ and too.

> 由法律设定组成的集合应归结为事件和条件。因此，描述在 E 上的词语当然是定义有限集的子集。如果时间很重要，这个 P 元素在序列中，或者通过附加一个时间戳来示例，但现在指定时间约束分开，E 和 S，对于序列也是成立的。这种 E 和级别相关的版本 M（），E^也是如此。

```
Now, there have been numerous suggestions and formalisms to he used it. the deve opm^ a stepwise approach of these are extremely helpfel, an g^ well.structured such as the one just outlined. 1 y . development in a top-
r,.".....-™. -«■ ■“
certain kinds of formal reasoning.
```

However, as it turns out, the methods structured and coherent development ” .[possible, acUally formaiional in nature. In transformat y eflectjng the natural Lghly desirable, to decompose he %Ze"1 to toother words, “structure of the problem , as i is transformation, a high-level description of the problem m the form of th in or function, that the system >s o Ue .ame species, in the these methods into several smal er p appropriate identifications form of lower level transformations, with the app P made among incoming and outgoing items. Each lower level transformation is then considered in its own right, and further decomposed. This is but another way of saying that each S(t+1) consists of a set of transformations, each of which was obtained from a transformation in S by transformational, or functional, decomposition. The system description is then taken to match the transformations described in S^,+ as closely as possible.

> 然而，事实证明，这些方法是有结构和连贯发展的，实际上是形式化的。在转换中，反映自然是非常理想的，将问题的结构分解为更小的部分。换句话说，“以较低级别的转换形式描述问题的高级描述”，系统的行为就是同一种物种，在这些方法中分解成几个较小的部分，以适当的识别形式进行匹配。每个较低级别的转换都是单独考虑的，并进一步分解。这只是另一种说法，即每个 S（t + 1）由一组转换组成，每个转换都是通过转换或功能分解从 S 中获得的。系统描述然后尽可能匹配 S ^，+中描述的转换。

This is admittedly a very crude and sketchy account of such methods, but the point we wish to make is that the procedure it illustrates works nicely for transformational systems because transformations decompose naturally into other transformations, and implementations of transformations decompose into implementations of other transformations. It is therefore a small thing for one to observe that the two decompositions can (and then even recommend that they should) be essentially the same, or at least that they be related via a simple mapping. This is particularly attractive due to the fact that transformational decomposition provides not only static information but also the dynamics necessary for a good behavioral description. For example, a conventional structure diagram or a function tree, two of the kinds of descriptions recurring in the literature, can be given clear operational meanings when considered for transformational systems: inputs (data and/or control) flow into boxes, modules or functions, which proceed to perform their designated transformations, yielding outputs which in turn flow into others, etc. This is a wholly satisfactory behavioral description of a transformational system.

> 这显然是对这种方法的一个非常粗略和简略的描述，但我们想要表达的观点是，这种程序非常适合变换系统，因为变换可以自然地分解为其他变换，而变换的实现可以分解为其他变换的实现。因此，很容易观察到，这两种分解可以（甚至建议它们应该）基本上是相同的，或者至少通过一个简单的映射相关联。这一点特别有吸引力，因为变换分解不仅提供静态信息，而且还提供良好行为描述所必需的动态信息。例如，文献中经常出现的结构图或功能树可以在考虑变换系统时获得清晰的操作意义：输入（数据和/或控制）流入框、模块或功能，然后执行其指定的变换，产生输出，然后流入其他模块等。这是变换系统完全令人满意的行为描述。

It is for these reasons that in most software engineering views of the life cycle of a system the specification stage is more or less followed by the design one: decompose the problem (=specify), and then use its parts and their interconnections as the basis for planning the implementation (=design). This idea is also one of the implicit mottos of structured programming: let the structure of the program reflect the structure of the problem, or, as one might say, let chunks of implementation (e.g. procedures, blocks, tasks, etc.) be made to correspond to chunks of behavior.

> 为了这些原因，在大多数软件工程的系统生命周期视图中，规范阶段通常会被设计阶段所取代：分解问题（=规范），然后利用其部分和它们之间的连接作为实施计划（=设计）的基础。这个想法也是结构化编程的一个隐含的座右铭：让程序的结构反映问题的结构，或者，正如人们可能会说的，让实现的块（例如过程、块、任务等）与行为的块对应起来。

Our main argument here is that this cheerful situation does not apply to reactive systems at all. In a reactive system, even a pure software one, it is not clear if or how complex behavior can at all be decomposed beneficially into chunks, let alone for that decomposition to become the basis for system design. This observation notwithstanding, it is ironical that a breakup of the behavior is precisely what will eventually have to be found, whether one likes it or XnMsX-, consist of various increasing y mor existence, have to hardware or mixed), each of which will by 1Uve^ye ; have some kind of associated behavior. doping the system will most probably be reactive themse ■ ’ decomposition, which, one ultimately have to involve some kin of phy iora, dccomposition way or another, will have to be matched oy a u tO0' Let us for now however, ioral descriptions of reactive sys eacljTe behavior itself. How does s’s.. for behavioral description.

> 我们的主要论点是，这种愉快的情况根本不适用于反应系统。在反应系统中，即使是纯软件系统，也不清楚复杂行为是否可以有益地分解为块，更不用说这种分解能否成为系统设计的基础了。尽管如此，令人讽刺的是，行为的分解最终还是必须找到，无论人们是否喜欢它。XnMsX-由各种不断增加的 y mor 存在组成，必须有某种与之相关的行为，无论是硬件还是混合的。拆解系统很可能本身就是反应性的，最终必须涉及某种物理分解，以某种方式或另一种方式，必须与反应系统的行为描述相匹配。现在，让我们来看看行为描述的方法。反应系统的行为本身是如何描述的？

(i) u should provide descriptions that are welLstructured, conc.se, unambiguous, readable, and easy to understand.

> 你应该提供结构良好、连贯、清晰、可读性强且易于理解的描述。

(ii) It should be solely descriptive, eliminating, or at least mimm.tmg, dependence on any implementation! issues.

> (ii) 它应该是纯粹的描述性，消除或至少减少对任何实施的依赖！问题。

Requirement (i) implies that ‘^"rttXoXX descZTon";het the Z'r'al decomposition of the probiem rather than that of the implementation.

> 要求(i)意味着“rttXoXX descZTon”；以问题的分解而不是实现的分解来获得'Z'r'al 分解。

## A Method for Behavioral Description

```
The sMfe^rf, method was introduced ' luprXof
XXltXX TXmi-Xd the system’s and
```

it consists of describing the system’s behavior in terms of states, events and conditions, with combinations of the latter two causing transitions between the former. Both states and transitions can be associated in various ways with output events, called activities, which can be triggered either by executing a transition or by entering, exiting, or simply being m a state. The system’s inputs are thus the (external) events and its outputs are the (external) activities; their union comprises the interface set E.

> 它包括用状态、事件和条件描述系统行为，其中后两者的组合导致前者之间的转换。状态和转换可以以各种方式与输出事件相关联，这些输出事件称为活动，可以通过执行转换或进入、退出或仅仅处于某个状态来触发。因此，系统的输入是（外部）事件，其输出是（外部）活动；它们的联合构成接口集 E。

This, as the reader can no dout see, is a standard and well-known idea, and is actually a simple combination of the Moore and Mealy definitions of finite state automata. The allowed sequences over E correspond to the language accepted by the automaton. Moreover, such automata come complete with a standard visual renderation, the transition diagram. T is classical state transition method, however, has been all but abandoned as a way of specifying the behavior of complex systems since it provides no modularity or hierarchical structure, and suffers acutely fropi the exponential blowup in the number of states that need be considered, and hence also in the number of transitions. Indeed, a state/event description seems to have to consider all possible combinations of states m all the components of the system; hence the exponential growth.

> 这一点，读者无疑可以看出，是一个标准且众所周知的想法，实际上是摩尔和米利定义有限状态自动机的简单组合。在 E 上允许的序列对应于自动机接受的语言。此外，这样的自动机还配有标准的视觉渲染，即状态转换图。然而，T 这种经典的状态转换方法已经几乎被抛弃，因为它不提供模块化或分层结构，而且受到指数爆炸所带来的影响，即需要考虑的状态数量和因此也会增加的转换数量。事实上，状态/事件描述似乎必须考虑系统中所有组件的所有可能状态组合；因此指数增长。

The statechart method is rooted in an attempt to revive this old and natural way of thinking about a system’s behavior, by extending it in several fundamental ways aimed at overcoming the aforementioned difficulties. The extensions apply to the underlying nongraphical formalism too, but personal preference towards visual descriptions has led us to present the ideas in terms of the graphical version. Some of the extensions are now briefly described, but the reader is strongly advised to consult the original paper for the others, as well as for a detailed example and further discussions.

> 状态图方法植根于试图复兴这种关于系统行为的古老而自然的思维方式，通过以几种基本的方式来克服上述困难。这些扩展也适用于基础的非图形形式，但个人偏好视觉描述导致我们以图形版本来呈现这些想法。现在简要介绍一些扩展，但强烈建议读者参考原始论文以了解其他扩展，以及详细的示例和进一步的讨论。

States in a statechart can be repeatedly combined into higher-level states (or, alternatively, high-level states can be refined into lower-level ones) using AND and OR modes of clustering. Fig. 3 shows a state B whose meaning is “to be in B the system must be in precisely one of D, E or F” and Fig. 4 shows a state A whose meaning is “to be in A tfie system must be both in B and in C.” Notice, however, that in Fig. 4,B and C are themselves OR states, thus the actual possibilities are the state configurations (D,G), (E,G), (F, G) and (F,H). We say that D, E and F are exclusive and B and C are orthogonal.

> 状态机中的状态可以使用 AND 和 OR 模式聚合重复地组合成更高级别的状态（或者相反，高级别的状态可以细化为低级别的状态）。图 3 显示了一个状态 B，其意义是“要处于 B，系统必须处于 D，E 或 F 中的恰好一个”，图 4 显示了一个状态 A，其意义是“要处于 A，系统必须同时处于 B 和 C 中。”但是，请注意，在图 4 中，B 和 C 本身是 OR 状态，因此实际可能的状态配置是（D，G），（E，G），（F，G）和（F，H）。我们说 D，E 和 F 是互斥的，B 和 C 是正交的。

```
Transitions in a statechart are not level-restricted and can lead from
Fig. 5: An output-free statechart
UvpI of clustering to any other. A significant decision a state on any level of clustering / . «SUDerstate” to mean
here is to take a transition w ose sourcpresent configuration •the system leaves this state no mattewh ch s the P within it.” In this way, wh.le event a m .J\* \_ causing the
from state K to L, the even exe P . being in J, and to enter system to leave L or M, i.e- Mf P°“‘ f thc ^-configurations
.......- -—
(L or the combination (E,G) in this example).
Actually, transitions are in general from Vs^e
rations, owing to the•P“’'bl{ ukes placc in configuration and’target states. Thus, m F g. happens in P the system en-
L^rco";^an^independence are both made possih.e by
```

orthogonality: on the one hand event m causes simultaneous transitions in B and C if the configuration is (E, G), and on the other p causes E to be replaced by D regardless of, and with no change to, the present state in C. It is noteworthy that orthogonality (and hence the possibilities it raises) is allowed and encouraged on any level of detail, as the statifier sees fit. Accordingly, a configuration can be layered too, containing orthogonal state components on many levels.

Outputs can be associated with transitions as in Mealy automata by writing a/b along an arrow; the transition will be triggered by a and will in turn cause b to occur. Similarly, b can be associated with (entering, exiting, or simply being in) a state, in line with Moore automata. In either case b can be an external event or an internal one, in the latter case triggering perhaps other transitions elsewhere in some orthogonal state.

> 输出可以通过在箭头上写上 a/b 与 Mealy 自动机中的转换相关联；转换将由 a 触发，并反过来导致 b 发生。同样，b 可以与（进入、退出或仅仅处于）Moore 自动机中的状态相关联。在任一情况下，b 可以是外部事件或内部事件，在后一种情况下，可能会触发其他在某些正交状态中的转换。

The statification method is purely behavioral and requires of its user to think in terms of the system’s conceptual states and their interconnections. It caters for modular “chunking” of behavior in several ways, most notably by using exclusivity and orthogonality of states, and provides the mechanisms needed for manipulating these modules as separate entities. Statecharts are strongly oriented towards “deep” structured descriptions that are organized into many levels of detail, and permit “zooming easily in and out of these levels. One can construct them in a disciplined hierarchical "way, statifying a system level by level, or use interlevel transitions and vary the depth as deemed appropriate. Statification can proceed by top-down refinement, bottom-up clust zing, or a mixture of both. Note that the exponential blowup in stat .s does not arise here at all, as the option of using orthogonality on any level eliminates the need for explicit consideration of all state combinations.

> 状态化方法完全是行为性的，要求其用户以系统的概念状态及其相互联系的方式思考。它以多种方式提供了行为的模块化“分块”，最显著的是通过使用状态的排他性和正交性，并提供操纵这些模块作为单独实体所需的机制。状态图强烈倾向于“深层”结构化描述，它们被组织成许多细节层次，并允许“轻松缩放进入和退出这些层次”。可以有纪律地以分层的方式构建它们，以层层状态化系统，或使用跨层转换并根据需要改变深度。状态化可以通过自顶向下的细化、自底向上的聚类或两者的混合来进行。请注意，状态的指数爆炸在这里根本不会出现，因为在任何层次上使用正交性的选项可以消除显式考虑所有状态组合的需要。

As a truely simple example of the way statechart levels refine reactive behavior, consider the system whose interface set E is as in Fig. 6. Its behavioral specification is given on two succesive levels in Figs. 7 and 8. The allowed sequences in Fig. 7 can be described by the regular expression

> 作为真正简单的状态图层次改进反应行为的例子，考虑其接口集 E 如图 6 所示的系统。其行为规范在图 7 和图 8 的两个连续层次上给出。图 7 中允许的序列可以用正则表达式描述

```
B{ • (a • Bl • a • Bi‘)w U B\_ • (a • Bl • a • Bj)\* • (Bf U a ♦ B?)
```

where Bi = (6UeUd) and Bq = (6UcUe). The version in Fig. 8, on the other hand, refines the allowed behavior to the sequences given by the same expression, but with B\ = (6U i>cd), and Bq = (£>U bee).

> 在图 8 中，另一方面，它将允许的行为细化为由相同的表达式给出的序列，其中 Bi =（6UeUd），Bq =（6UcUe），而 B\ =（6U i>cd），Bq =（£>U bee）。

This, then, is the formalism we wish to recommend for specifying reactive behavior. It is important to observe that the description can be made to reflect the statifier’s personal and natural view of the system’s behavior free, if so desired, from implementational details. If lifting a receiver conceptually causes a communication system tc. enter conversation mode, and this mode entails certain actions, one can say just that, disregarding such questions as which component is responsible for sensing the lifting of the receiver and how the sensed fact is communicated to the others. Of course, the crucial problem here is bringing this concep ua description down to earth; meaning, how does one combine it with.the natural implementational process of breaking the system down into >ts physical parts and their interconnections.

> 这就是我们想推荐的用于指定反应行为的形式化方法。重要的是要观察到，如果需要的话，描述可以反映静态化者对系统行为的个人和自然观点，而不受实施细节的限制。如果概念上抬起接收器会导致通信系统进入对话模式，并且这种模式会带来某些动作，那么可以这样说，而不必考虑哪个组件负责感知接收器的抬起以及如何将感知到的事实传达给其他人。当然，这里的关键问题是如何将这种概念带入实际；也就是说，如何将它与将系统分解为其物理部分及其互连的自然实施过程相结合。

```
Fig. 6: A reactive system with its interface set
A v ♦ Fig. 8: A refined statechart
Fig. 7 : A statechart
```

## The Magic Square of System Development

Now that we know how to decompose reactive behavior, we can attempt to apply the “problem structure matches system structure pnnci-plXdeedJf there are no limitations on the implementation at all one can do just thai; refine the behavioral specification by adding sta tec hart level as illustrated above, and then perform the implementations! refinemen to match. While this might sound overly naive, in a pure software tem with a sufficiently high-level programming language the ^tech^rts can be directly encoded into software, with multi-level orthogonality being translated into nested concurrency. This applies to other possible methods for reactive behavior specification, such as Petri nets or languages like CCS.

> 现在我们知道如何分解反应行为，我们可以尝试应用“问题结构与系统结构相匹配”的原则，如果实施上没有任何限制，就可以这样做：通过像上面所示的添加状态图层来完善行为规范，然后执行实施！细化以匹配。虽然这听起来可能过于天真，但在纯软件系统中，如果使用足够高级的编程语言，状态图可以直接编码到软件中，多级正交性可以转换为嵌套的并发性。这也适用于其他可能的反应行为规范方法，如 Petri 网或诸如 CCS 之类的语言。

It is clear, however, that the vast majority of interesting reactive systems feature various preconceived, unavoidable limitations on the structure, distribution, capabilities and interconnections of their implemena-tional components. Examples include geographical distribution of portions of an airline reservation system, standard components of an avionics system, physical limits on hardware components and their interaction, etc. Even concurrent programs are, in general, not all that pure, as one typically is constrained by a limit on the maximal number of concurrently executing processors. In this way, if the implemenational restricions are to be honored, being overly liberal in the use of orthogonality, for example, can easily cause severe problems in a.naive attempt to model the implemenational refinement according to the behavioral one.

> 显然，大多数有趣的反应系统都具有各种预先设定的、不可避免的关于其实现组件的结构、分布、能力和互连的限制。例如，航空预订系统的部分地理分布、航空电子系统的标准组件、硬件组件及其交互的物理限制等。即使是并发程序也通常不是纯粹的，因为通常受到最大并发执行处理器数量的限制。通过这种方式，如果要遵守实现限制，那么在使用正交性时过于宽泛，可能会在根据行为模型对实现细化进行简单尝试时出现严重问题。

What this means is obvious: our recommendation for a method that enables natural behavioral decomposition notwithstanding, the impleman-tational description has a nasty habit of prescribing, at least in part, its own decomposition, which need not, in general, match our conceived behavioral one.

> 这意味着很明显：尽管我们推荐的一种使自然行为分解成为可能的方法，但实现描述有一个令人讨厌的习惯，至少在一定程度上，它自己的分解不必一定与我们构想的行为分解相匹配。

These observations prepare the ground for a very simple idea: by and large, the development of a reactive system is not a one-dimensional process in which specification and design are two temporally related stages, but rather it is a two dimensional “magic square” in which they play the role of the dimensions themselves. One might label the two dimensions simply “specification” and “design”, but we prefer to use those terms as verbs, and so we label the dimensions “behavior” and “implementation”. One thus specifies the system’s behavior but one designs its implementation. See Fig. 9.

> 这些观察为一个非常简单的想法奠定了基础：总的来说，反应系统的发展不是一个一维过程，其中规格和设计是两个时间相关的阶段，而是一个二维的“魔方”，它们扮演着维度本身的角色。人们可以简单地将这两个维度标记为“规格”和“设计”，但我们更喜欢用动词来使用这些术语，因此我们将维度标记为“行为”和“实现”。因此，一方面可以指定系统的行为，另一方面可以设计其实现。请参见图 9。

Fig. 9 : The magic square

Along both dimensions making progress amounts to supplying more detail but the two axes involve fundamentally different kinds of detail. Proceeding vertically (downwards), one is bringing the system closer o its final form by supplying more information about its implementation, and proceeding horizontally (rightwards), one is fine-tuning the system s performance by providing more information about its behavior. In either case and this explains in part our use of the term “magic square , every line or column amounts to a full, stratified, description of the system along one axis, but at a fixed level of detail along the other.

> 沿着两个维度取得进展意味着提供更多的细节，但是这两个轴涉及到基本上不同类型的细节。向下（向下）进行，通过提供有关其实施的更多信息，使系统更接近其最终形式，而向右（向右）进行，则通过提供有关其行为的更多信息来微调系统的性能。无论哪种情况，这部分解释了我们使用“魔方”这个词的原因，每一行或每一列都相当于沿着一个轴的系统的完整，分层的描述，但在另一个轴上的细节水平是固定的。

Ideally, the development process starts at the upper leftmost point, with nothing known about the system’s intended behavior or its desire implementation, and ends at the lower rightmost point with everyth g known about both. The more subtle side of the term “magic: square > rooted in the many possible ways of traversing the square from its initial point to its final one; following any of these correctly should result in the system being fully specified and fully designed.

> 理想情况下，开发过程从最左上角开始，对系统的预期行为或其期望实现一无所知，最终到达最右下角，对两者都了如指掌。“魔方”这一术语的更微妙的一面植根于从最初点到最终点的许多可能的穿行方式；沿着任何一条正确的路径都应该导致系统被完全指定和设计。

It seems almost an ac dent that for the easier systems in our dichotomy, i.e. transformational ones, or reactive ones with no implem tational Constraints, this process can actually be linearized by, m essenc , mapping one dimension onto the other relatively easily as discussed ear-lier In our opinion this accident is the heart of many misconceptions and difficulties encountered in the development of complex systems, and some extent also in pure concurrent programming.

> 似乎几乎是一个意外，对于我们的二分法中更容易的系统，即变换系统，或者没有实施约束的反应系统，这个过程实际上可以通过映射一个维度到另一个维度相对容易地线性化，正如之前讨论的那样。在我们看来，这种意外是许多复杂系统开发中遇到的误解和困难的核心，在某种程度上也是纯并发编程中遇到的困难。

We are aware of the fact that even with concrete formalisms in mind any discussion of such a general model for system development is bound to seem naively idealistic when considered for real-world applications, ertheless, we are determined to describe our model m the simplest•P°«'b terms, and for that purpose, besides adopting simple statecharts, free global constraints, for the behavioral axis, we adopt a very simple dec position method for the vertical, implementational axis.

> 我们意识到，即使有具体的形式主义，在考虑实际应用时，讨论这样一个系统开发的一般模型也必然显得过于理想化，但是，我们决心以最简单的方式描述我们的模型，为此，除了采用简单的状态图外，我们还采用自由的全局约束来描述行为轴，并采用非常简单的分解方法来描述垂直的实现轴。

At level 0 of the vertical axis the system resides as an unspecified entity Ml0’, together with its interface set E«». Progressing down the verticalTaxi; is characterised by a step of implementat.onal decompose tion For a typical descent from level i to level t + 1, a subsytem M level i, with interface set E, might be decomposed into its constituent components Mi.......M„, with their interface sets Ei,...,E„;

> 在垂直轴的第 0 级，系统作为未指定的实体 Ml0 存在，其界面集合为 E«»。沿着垂直轴向下进行的过程被描述为实现分解的一个步骤。对于从第 i 级到第 t+1 级的典型降落，具有界面集 E 的第 i 级子系统 M 可以分解为其组成部分 Mi......M„，其界面集分别为 Ei，...，E„。

For this decomposition to be acceptable certain obvmus property must be satisfied For exampie, each element of E, the interface set of M, must a^ar Tn at least »M sd Ej, or at least be refined into more concrete elements, each of which appears in at least one Ej.

> 对于这种分解来说，必须满足一些显而易见的属性才能被接受。例如，M 的接口集 E 中的每个元素都必须至少出现在 Ej 中，或者至少被细分为更具体的元素，每个元素至少出现在一个 Ej 中。

Fig. 10: Implementations! decomposition

In addition to interface elements that are external to the whole system, the interface set Ej of Mj may contain additional elements which are external to M.- but internal to M. These dements provide the components ■with the ability to communicate, synchronize, and influence one another. Thus, each element in Ej - E must be tagged with some indication as to its source or target subsystem(s) from among the others. We shall not go into more detail here so as not to detract attention from the underlying issues. Besides, our presentation of this decomposition method is highly simplified anyway, and many standard methods can be readily adopted for a satisfactory treatment of the implementational axis.

> 除了与整个系统外部的接口元素外，Mj 的接口集 Ej 还可以包含其他外部于 M，但内部于 M 的元素。这些元素使得组件之间能够进行通信、同步和影响。因此，Ej 中的每个元素-E 都必须标记一些指示，以指明其来源或目标子系统。为了不分散注意力，我们在此不再详细介绍。此外，我们对这种分解方法的介绍已经非常简化，许多标准方法可以轻松采用，以满足实施轴的要求。

In contrast to making progress down the vertical axis by refining the implementational design of the system, progressing along the horizontal axis refines and structures its behavior, and as discussed above can be thought of as adding levels to the appropriate statecharts. Having reached some fixed vertical level t, one has essentially decided upon a set of implementational modules, say and now proceeding horizontally at this vertical level amounts to statifying each of these. The outcome, of course, is a set Si,..., Sk of statecharts whose interface sets are simply those of Mi,, Mk.

> 相比于通过完善系统的实现设计来沿着垂直轴取得进展，沿着水平轴的进展可以细化和结构化其行为，正如上文所讨论的，可以将其视为为适当的状态图添加层次。到达某个固定的垂直水平 t，基本上已经决定了一组实现模块，现在在这个垂直水平上进行的进展就是将这些模块都状态化。当然，结果就是一组状态图 Si，...，Sk，其接口集仅为 Mi，...，Mk。

As a side remark, note that the magic square is not a square at all. First, there is no reason whatsoever for the levels of implementationa e-tail to be equal in number to those of behavioral detail, so that at the very best the development model should be called a magic rectangle. Secondly, and more significantly, the implementational decomposition, even using the simple model above, forms a tree, and one whose branches are not necessarily of equal length, so that the outcome is more like a tree with 11 Thirdly and most significantly, for any given long sprkes; see Fig. 11. ™ m compOnent) the behavioral denode in the implementation tre ( y is actually a scription itself, even using simple statecharts on th amongst or tree or worse, again with no uniform , actual development within each other. For a fixed. sys em er ultidimensional tangled

> 作为一个旁注，注意魔方根本不是一个正方形。首先，实施细节的层次没有任何理由与行为细节的层次相等，因此最好的开发模型应该被称为魔方长方形。其次，更重要的是，即使使用上面的简单模型，实施分解也形成一棵树，而且其分支不一定是相等的，因此结果更像是一棵 11 叉树。第三，最重要的是，对于任何给定的长节点，请参见图 11。™m 组件）实施树中的行为节点实际上是描述本身，即使使用简单的状态图，也不能形成树或更糟的树，而且每个树枝的长度也不一样，因此实际开发中也不能彼此匹配。对于固定的系统来说，它是多维纠缠的。

Fig. 11: The magic square as a spiky tree

```
dominating dimensions.
An observation worth emphasizing is the presence, indeed highly desirable presence, of concurrency along both ^e^^
XSS— -i^IX^^^eom^ and in the behavioral axis concurrency appear the orthogonality
rsX’JK- ■'
of states, tiotn, ^.w+hn<rnnalitv seems to us to be a
conjunction.
```

With the story we have told so far, two obvious ways of traversing the magic square come immediately to mind: the L-shaped all-the-way-down then all-the-way-to-the-right traversal, and its dual. The first corresponds to a practice common in certain kinds of concurrent programs: obtain information as to the number, type and interconnections of available processors, and then specify the behavior of each, which is tantamount to programming them. Whether the programming, which can itself proceed in a stepwise-disciplined manner, is regarded here as specification or design is irrelevant; the main point is that one is programming per processor. Actually, one usually has some high level description of the intended behavior in mind even when one proceeds in this L-shaped way, but rather than being used in a rigorous way in the development process it is more often simply referred to at the end for the purpose of verifying the final product against it.

> 随着我们到目前为止讲述的故事，两种明显的穿越魔方的方式立即浮现出来：L 形的一路向下再一路向右的穿越，以及它的对立面。第一种对应于某些并发程序中的一种常见做法：获取可用处理器的数量、类型和连接的信息，然后指定每个处理器的行为，这相当于编程它们。在这种 L 形方式中，编程本身可以以逐步纪律的方式进行，但是它是被用作规范或设计，这是不重要的；主要的是，每个处理器都在编程。实际上，即使在以这种 L 形方式进行时，人们也通常有一些高层次的期望行为描述，但是它们不是用来严格地开发过程，而是在最后用来验证最终产品。

The dual traversal calls for a complete behavioral specification prior to any implementational decomposition, and was hinted at earlier. Neither of these traversals of the magic square can be particularly recommended for complex systems. Actually, neither of them makes essential use of the available two-dimensionality at all, and as a consequence neither requires that behavioral descriptions be projected in a nontrivial way from one vertical level to the next. This kind of behavioral projection, however, is one of the most crucial aspects of our magic square, as we now set out to show.

> 双重遍历要求在任何实施分解之前完成行为规范，并且之前暗示过。这两种魔方阵遍历方式都不适合复杂系统。实际上，它们都没有充分利用可用的二维性，因此也不需要从一个垂直层次到另一个垂直层次进行行为描述的非平凡投影。然而，这种行为投影是我们魔方阵的最关键的方面，正如我们现在要展示的那样。

## A Consistency Criterion for The Magic Square

In general, we wish to argue, a healthy development process prescribes some horizontal progress prior to each significant progress made on the vertical level. That is, at vertical level i system component M is given a behavioral specification S of certain depth, that is, extending to some horizontal point. One then decomposes M (or is provided with a decomposition of M) into its subcomponents Mi,..., Mn and somehow specifies the behavior of each, to the same horizontal depth, yielding the preliminary S{,..., S’n. The S’. are then refined as discussed above, yielding the final behavioral descriptions S\,..., Sn of vertical level t + 1. Of course, this set of behavioral descriptions of the Mj has to be consistent with behavior

> 一般来说，我们希望论证，健康的发展过程在每次在垂直层面上取得重大进展之前，都会先进行一些水平进展。也就是说，在垂直层次 i 系统组件 M 被给予某种深度的行为规范 S，即延伸到某个水平点。然后将 M 分解（或者提供 M 的分解）为其子组件 M1，...，Mn，并以某种方式为每个子组件规定其行为，达到相同的水平深度，从而产生初步的 S1，...，Sn。然后根据上述方法对 S1，...，Sn 进行细化，得到垂直层次 t+1 的最终行为描述 S1，...，Sn。当然，这组 Mj 的行为描述必须与行为一致。

```
Fig. 12: Traversing the magic square
CM
```

the behavioral description & of the higher-level system M, and we define the nature of this consistency below. The general progress can thus be schematically described as in Fig. 12, with the progress arrow aiming and hitting the final point corresponding to the fully-specified, fully-designed system. Each shaded area in Fig. 12 thus represents the collection of behavioral descriptions of all subsystems relevant to level i of the implementation.

> 行为描述和高级系统 M 的性质定义如下，因此，总体进度可以如图 12 所示概括地描述，进度箭头指向并达到最终点，对应于完全规定、完全设计的系统。图 12 中的每个阴影区域因此代表了与实现级别 i 相关的所有子系统的行为描述集合。

At the expense of sounding repetitious we remind the reader of Fig. 11 and its more realistic, hence far more complicated version of our simple “square”, meaning that the S' of each Af on any level is given at the depth of behavioral detail appropriate to it and its “neighbor” subsystems. However, as mentioned earlier, for our purposes the issues can be discussed under the pretensions implicit in Fig. 12.

> 就算听起来重复，我们还是要提醒读者参考图 11，它更加现实，因此也更加复杂，比我们简单的“正方形”更加精确，这意味着每个 Af 在任何一个层次上的 S'都是在适当的行为细节深度上给出的。然而，正如前面提到的，就我们的目的而言，这些问题可以在图 12 所隐含的假设下讨论。

Three questions come immediately to mind:

(1) What is, or should be, the precise consistency criterion relating SW to

> 什么是或者应该是将软件与简化中文之间的精确一致性准则？

(2) Given a satisfactory answer to (1), can one recommend a recipe for obtaining from the decompositions carried out when progressing downwards from level i to level t 4- 1, together with

> (2) 如果对(1)提出了满意的答案，那么可以推荐一个从第 i 层到第 t-1 层进行分解时获得的方案吗？

(3) Whatever the answers to questions (1) and (2) are, can one recommend a “good curve” for traversing the square?

> 无论问题（1）和（2）的答案是什么，可以推荐一条“好的曲线”来穿越正方形吗？

Question (1) is purely technical, and without answering it satisfactorily the whole magic square model collapses. There must be a firm and precisely defined connection between the specified behavior of a portion of the system and that of its constituent components, one which then transcends to become a global connection between the initial and final stages of the entire development process.

> 问题（1）纯粹是技术性的，如果没有令人满意的回答，整个魔方模型就会崩溃。必须在指定的系统部分行为和其组成部分行为之间建立一个坚定而精确定义的联系，这种联系将超越整个发展过程的初始和最终阶段之间的全局联系。

The answer to question (1) can be stated informally as follows:

The external behavior implicit in must be equivalent to that implicit in Sz(,+1\ the preliminary behavioral description on level i 4-1 which is of the same horizontal detail as S(‘).

> 外在行为中隐含的必须与在 Sz(,+1)中隐含的相等，这是等级 i 4-1 的初步行为描述，与 S(‘)的水平细节相同。

This simple answer contains some subtlety, since apart from the haziness of “external”, “implicit” and “equivalent”, sW, in our chosen framework of formalisms, is but a collection of statecharts, one for each component on level t, and Sz(,+1) is a different collection, assoc ated with a different level and different components. Nevertheless, the answer can be made precise quite naturally, as ..justrated in Fig. 13.

> 这个简单的答案包含一些微妙之处，因为除了“外部”、“隐式”和“等效”的模糊性之外，在我们选择的形式化框架中，sW 只是一系列状态图，每个组件在 t 级别上都有一个，而 Sz（，+1）是一个不同的集合，与不同的级别和不同的组件相关联。尽管如此，答案可以很自然地得到精确的表达，如图 13 所示。

Take a typical level i component M and its subsystems Mi,..., Mn on level i -I- 1. In SW there will be a statechart S for M and in S^,+1) statecharts S'J,..., S'n for the Mj. As discussed earlier, each pair (Mj, S'.)

> 對於 i 級別的元件 M 及其子系統 Mi，...，Mn，在 i-1 級別上，軟件中將有一個狀態圖 S 對應 M，以及 S^，+1)狀態圖 S'J，...，S'n 對應 Mj。正如前所述，每一對(Mj, S'.)將會有一個對應的狀態圖。

## System Components Behoviorol Descriptions

```
LEVEL i. LEVEL i + 1 M 1 decomposition Ej En _ ••• Mfl E S | question (2) E| E„ ♦ [ s; ] ... [ s; J 11 refinement E. E_ \_ 12lj Is" ]
```

## CONSISTENCY CRITERION

external behavioral equivalence

Fig. 13: The consistency criterion for the magic square has an interface set Ej, only part of which is extern^ { by corresponding directly to the £ of (M,\_ of simplicity let ns assume t discussed above, each selves refined in the transition to the S internal to Ei 'Til °f e'eM? Now form a new statechart S’ by simply placing {Ade by^de as orthogona! components. Their inte«ommrtm» via the interna! interface sets Ej - whose chart formalism itself, n whtch are not interna! to the cc «-• •• ’ •• " set of sequences over E.

> 图 13：魔方的一致性标准具有接口集 Ej，其中只有一部分是外部的，通过直接对应（M，\_），为了简化，我们假设上面讨论的每个状态本身都在转换到 S 内部时被细化了。现在通过将它们作为正交组件逐个形成一个新的状态图 S'。它们之间的内部接口集 Ej - 其图形形式本身是内部的，不是内部接口集的一部分 - 通过 E 上的序列集来实现。

If this equivalence holds when applied to each and every implemen-tational component on level, we say that ?e latter “t TFnsX^ former, together wi^ the fact that S^, the tri"y a""of deta”to the statecharts therein, thereby refining the behaviors they define.

> 如果这种等价性在每个实现组件的层面上都能得到应用，我们就可以说，后者“等同”前者，加上 S^的事实，即状态图中的细节，从而改进了它们所定义的行为。

In the case where E is indeed refi°^ ™^^0^ of consistence, tion, the notion of equivalence and imcor^ S? matching of interface has to be appropriately modifie af.roTnDanied by a set of additional elements. Also, if the sta^ar ’ amentioned earlier, the refinement of I1.?.1?') Ct"must\* adhPere to tJose, and hence might require a^parat^ straints too m the process of ma ing statecharts do, then relativize to the interface sets of each level, just a resulting in a for level 1, and,^^eroiis other possible consistency will have to change to . > the magic square, th:basic model in a natural way' ,-nd with the underlying principles being the same. nr thP definition of local consistency between The mam consequence of that consistency is vertical levels is in its transitivity. By this we m propagated down (or up) the vertical axis, resulting in the following fact:

> 在 E 确实是一致性的重新定义的情况下，等价性和接口的匹配必须适当地修改，并伴随着一组附加元素。此外，如果提到的标准是前面提到的，那么 I1.1 的细化必须遵守这些标准，因此可能需要额外的约束来完成状态图的制作，然后相对于每个层次的接口集，只有一个结果，对于第 1 层，以及其他可能的一致性，必须改变为魔方，这是一个自然的基本模型，其基本原则是相同的。垂直层次之间的局部一致性定义的主要结果是其传递性。通过这种方式，它可以向下（或向上）传播垂直轴，导致以下事实：

If a complete development process is carried out in the magic square model, using any desired traversal, while checking local consistency, the final behavioral description of the system, S^), is consistent with the initial one, S(°). In other words, if one constructs the entire system using the “atomic” implementational components prescribed by the final vertical decomposition level f and connects them as prescribed by the interface sets on that level, and if one then convinces oneself that each of these low-level components behaves as prescribed by its behavioral description in then the entire system is correct with respect to its initial specification

> 如果在魔方模型中完成整个开发过程，使用任何所需的遍历，同时检查局部一致性，系统 S^）的最终行为描述与初始描述 S（°）一致。换句话说，如果使用最终垂直分解级别 f 规定的“原子”实现组件构建整个系统，并按照该级别上的接口集进行连接，然后确保每个低级组件的行为描述符合其规定，那么整个系统就符合其初始规范。

This, by the way, should remind the reader of classical methods for program verification, where global correctness follows from the correctness of the consituent modules.

> 这提醒读者，经典的程序验证方法可以从组成模块的正确性得出全局正确性。

Precisely how one convinces oneself of the behavioral correctness of the ate nic components is of no concern here. It might follow from a manufacturer’s documentation, a programmer’s verification, or be regulated to mere belief. Just as in any typical verification process, the soundness of one’s use of the magic square in this fashion is a doubly-relative concept; it relies on an accepted initial specification, against which one verifies what one has constructed (in this case this is the initial behavioral specification S(0)), and it relies on an “axiomatic” acceptance of the fact that the atomic elements, which constitute the building blocks with which one has carried out that construction, are correctly specified (in this case this amounts to accepting the final vertical level as is).

> 不用担心如何说服自己行为上的正确性的原子组件。可能来自制造商的文档，程序员的验证，或者仅仅是信仰。正如任何典型的验证过程一样，使用这个魔方的正确性是一个双重相对的概念；它依赖于一个受接受的初始规范，用来验证我们构建的东西（在这种情况下，这是初始行为规范 S(0)），它依赖于“公理”接受的事实，即构成构建的原子元素是正确规定的（在这种情况下，这相当于接受最终的垂直水平）。

At this point, one might be tempted to ask the following question: if the S and S* appearing at a certain stage in the process (see Fig. 13) are required to be two equivalent descriptions of the same part of the final system, given in the same formalism, and over the same interface set E, why then is S* not constructed directly? Why was S\* not given as the level i behavioral description of component M, especially since it is already conveniently decomposed in accordance with the decomposition Mi,..., Mn of Ml It goes without saying that this would eliminate any necessity for checking the equivalence of behavioral descriptions. The answer, of course, embodies the main issue here: S\* is not necessarily a natural behavioral description of M because it is composed according to Mi,.., Mn. A good behavioral description of an airline reservation system which uses ten geographically distributed computers and a thousand terminals might be one whfch decomposes in ways that cut across this physical decomposition j^st as a good behavioral description of a VLSI chip need not be given’in terms which even mention its breakup into design-related bloc s. Whatever the case, the “unnatural” S‘, which consists of the behavioral descriptions St.....Si of the components Mi,.. ,, has be prepared somehow; but how? This is precisely question (2) above.

> 在这一点上，人们可能会诱惑性地问以下问题：如果在过程中的某个阶段出现的 S 和 S*需要是最终系统的同一部分的两种等效描述，并且使用相同的形式主义和相同的接口集 E，那么为什么不直接构造 S*？为什么不把 S*作为 M 的第 i 级行为描述，特别是因为它已经按照 M1，...，Mn 的分解方式很方便地分解了呢？不用说，这将消除任何检查行为描述等价性的必要性。当然，答案体现了这里的主要问题：S*不一定是 M 的自然行为描述，因为它是根据 Mi，...，Mn 组成的。一个使用十台地理分布的计算机和一千个终端的航空预订系统的良好行为描述可能会按照跨越物理分解的方式分解，就像一个良好的 VLSI 芯片行为描述不需要以甚至提及它分解为设计相关块的方式给出。无论如何，由行为描述 St，...，Si 组成的“非自然”S\*必须以某种方式准备；但是如何准备呢？这正是上面的问题（2）。

## How to Traverse the Magic Square?

We are in no position to present detailed answers to questions (2) and (3) and even less so to claim that we know of answers that can or should be’used uXersally. Quite to the contrary, different kinds of systems present different kinds of problems in behavioral 8Pec‘^at'on’ entire development process can be regarded as an art, with many and many possibilities.

> 我们无法就问题（2）和（3）提供详细的答案，更不用说声称我们知道可以或应该使用的答案了。恰恰相反，不同类型的系统在行为表现方面提出了不同的问题，整个开发过程可以被视为一种艺术，有着许多可能性。

Moreover, more often than not, a complex development effort does not start at the initial point of a totally blank magic square. It usually starts S ™ OUS portions of the square already filled in. That s, certain system comjxments, and even certain chunks of behavior, are already presented to”he developer in advance, and the development process must accomodate them as it proceeds. Therefore, as far as question (3) is concerned, we can only say that, when viewed as a function that plots honsontal progre s agains/vertical progress, the development curve should be monotonically S (see Fig 12); it makes very little sense to provide subcomponent with less behavioral detail than its parent component. However, other than that, and other than observing that the curve should Pr°bab£ be nontrivial (i.e., not L-shaped or its dual), developers should be free define their own preferred curves for traversing the square.

> 此外，复杂的开发工作往往不会从一个完全空白的魔方开始。通常情况下，一些魔方已经填充了部分内容。也就是说，某些系统组件，甚至某些行为块，已经提前提供给开发人员，开发过程必须在进行过程中适应它们。因此，就问题（3）而言，我们只能说，当将其视为将水平进度与垂直进度放置在一起的函数时，开发曲线应该是单调的（见图 12）;为子组件提供比其父组件更少的行为细节几乎没有意义。但是，除此之外，除了观察曲线应该可能是非平凡的（即不是 L 形或其双重形状），开发人员应该自由定义自己喜欢的曲线来遍历正方形。

As to question (2), there is one general point to be made here. Let M be a component on vertical level i, decomposed on level . + 1 into az. . and let S be the behavioral specification of M. If B and Ei ’... En are the interface sets of the components (no refinement in the E’s; as’above), then one can proceed as follows: for each 1 < 3 n, s ar with S itself as a first approximation to Sjt the behavioral specification of Mj on level t + 1.

> 至于问题（2），这里有一个总体的观点。让 M 是在垂直水平 i 上的一个组件，在水平+1 上分解为 az。。让 S 是 M 的行为规范。如果 B 和 Ei'...En 是组件的接口集（在 E'中没有细化；如上所述），那么可以按照以下步骤进行：对于每个 1 < 3 n，s ar 以 S 本身作为 Mj 在水平 t + 1 上的行为规范 Sjt 的第一个近似。

Now, clearly S is not a legal statification of Sj in general, since it refers to elements from E — Ej. However, this can be fixed as follows. Output elements in E - Ej are simply eliminated, and for each input element e therein one finds a k with e € Ek, and modifies the two copies of S, that of Ek and that of Ej, so that the former, whenever e is sensed, outputs a new item e' to Mj, in whose copy of S each e is replaced by e . In this way Mj can sense the input event e even though it can be directly sensed only by Mk. The resulting statecharts, call them Sf,..., Sn, are now legel behavioral specifications of the Mj, in the sense that their orthogonal product is equivalent to S. Moreover, the Sj are on the same horizontal level of detail as S. These S’!, therefore, conform to the definition of the preliminary description of see Fig. 12, and hence, in principle, we have answered question (2). However, we clearly do not recommend that one stop here; the result will be an exponentially growing behavioral specification, not to mention its complete detachment from any naturalness involved in the implementation refinement of M into the Mj. Rather, one should work on the S", simplifying and changing them to reflect the intended behavior of the Mj. In this sense, the only useful role S'! can play, is that of a starting point leading to the desired Sj, the final behavioral specification of Mj.

> 现在很明显，S 不是 Sj 的一般合法状态，因为它涉及到来自 E-Ej 的元素。然而，可以通过以下方式来修复。简单地消除 E-Ej 中的输出元素，对于其中的每个输入元素 e，找到一个 k，使 e 属于 Ek，并修改 S 的两个副本，即 Ek 的副本和 Ej 的副本，以便前者在感知到 e 时输出一个新项 e'到 Mj，其中 S 的每个 e 被 e'替换。这样，Mj 就可以感知输入事件 e，尽管它只能由 Mk 直接感知。得到的状态图，称之为 S'1，...，Sn，现在是 Mj 的合法行为规范，因为它们的正交积等效于 S。此外，Sj 处于与 S 相同的水平细节。因此，这些 S'1 符合图 12 中的初步描述的定义，因此，原则上，我们已经回答了问题（2）。但是，我们明显不建议停止在这里；结果将是指数级增长的行为规范，更不用说它与实现细化 M 到 Mj 中涉及的任何自然性完全脱节。相反，应该对 S'进行工作，简化和更改它们，以反映 Mj 的预期行为。从这个意义上说，S'只能发挥的有用作用是作为一个起点，引导到所需的 Sj，即 Mj 的最终行为规范。

Actually, we feel that it is worthwhile to search for good transformations for weeding out portions of S'- not really relevant to Mj, using the difference between E and Ej, and S itself as directives. Such transformations, certain simple examples of which come immediately to mind, should be required to preserve equivalence of the behavior, modulu the transition from E to Ej.

> 实际上，我们认为寻找良好的转换来消除与 Mj 不太相关的 S'部分是值得的，使用 E 和 Ej 之间的差异以及 S 本身作为指令。这样的转换，其中一些简单的例子立即浮现在脑海中，应该要求保留行为的等价性，模块从 E 到 Ej 的转换。

The equivalence problem for reactive behavioral specifications, and in particular equivalence-preserving transformations of Statecharts, seems to be an important area for future research. Satisfactory and useful results in this direction can help turn the magic square from a model of system development, which is the way we have tried to portray it here, into a detailed methodology, or prescription, a line we have not yet tried to pursue.

> 關於反應行為規範的等價問題，特別是對狀態圖的等價保護轉換，似乎是未來研究的重要領域。在這方面取得令人滿意和有用的結果，可以幫助將魔方從我們在這裡嘗試描述的系統開發模型轉變為詳細的方法學或處方，這是我們尚未嘗試去追求的一條路。

Acknowledgement

The contents of this paper owe much to many colleagues and authors. In particular, we have been influenced by several ideas found m the work of M. Alford, L. Lamport and D. Parnas.

> 本文的内容很大程度上要归功于许多同事和作者。特别是，我们受到了 M. Alford、L. Lamport 和 D. Parnas 的许多作品中发现的几个想法的影响。
