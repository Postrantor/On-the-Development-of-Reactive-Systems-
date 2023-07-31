---
On the Development of Reactive Systems*
D. Harel and A. Pnueli
Department of Applied Mathematics The Weizmann Institute of Science
Rehovot 76100, Israel
January, 1985
---

## Abstract

Some observations are made concerning the process of developing complex systems. A broad class of systems, termed reactive, is singled out as being particularly problematic when it comes to finding satisfactory methods for behavioral description. In this paper we recommend the recently proposed statechart method for this purpose. Moreover, it is observed that most reactive systems cannot be developed in a linear stepwise fashion, but, rather, give rise to a two-dimensional development process, featuring behavioral aspects in the one dimension and implementational ones in the other. Concurrency may occur in both dimensions, as orthogonality of states in the one and as parallelism of subsystems in the other. A preliminary approach to working one’s way through this “magic square of system development is then presented. The ideas described herein seem to be relevant to a wide variety of application areas.

## Why Another Paper on System Development?

The literature on software engineering, programming languages, and system and hardware design, is brimming with papers describing methods for specifying and designing large and complex systems. Why then are we writing yet another one?

In many kinds of computation-oriented or data-processing systems, sometimes characterized as sequential or functional systems, there is, for the most part, consensus as to the basic philosophy for design. For more complex systems, involving many concurrently executing components, which at times integrate software and hardware, there is much less of an agreement. As we argue below, this is due to an essential difference between two kinds of systems that makes the process of developing the more complicated of the two inherently more difficult. Indeed, we would like to think of the present paper as primarily containing an attempt to clarify sone of the underlying notions which seem to us to be fundamental. In passing, we shall attempt to address such issues as the kinds of systems that require new ideas, and the gaps such ideas ought to fill.

## Which Systems are Problematic?

We would like to state from the start that by “systems” we do not wish to restrict ourselves to ones which are software-based, hardware-based or so-called computer-embedded. The terminology we shall be using is general enough for these and others, and so we shall not be specific about the final form the implementation of the system takes.

In many circles it is common to try to identify the features characterizing "difficult” systems; that is, the ones for which special methods and approaches are needed. Resulting from these efforts are various dichotomies distinguishing the easily-dealt-with systems from the problematic ones. Some people (e.g. in the programming language semantics community) have put forward the deterministic/nondeterministic dichotomy, systems for which the next action is uniquely defined can be easily defined, while nondeterminism requires special treatment. Others (such as certain verification researchers) have suggested that the problems lie in perpetual systems, whereas terminating ones are easy. Additional dichc omies that have been suggested are the synchronous/asynchronous, “lazy / real-time, and off-line/on-line ones, and what is perhaps the most popular one: the sequential/concurrent dichotomy. Indeed, concurrency gives rise to problems that are quite different from the ones sequential systems present, and there are entire schools of thought devoted to solving the problems raised by the presence of concurrently operating elements.

Fig. 1: A transformational Fig. 2: A reactive system as a “black cactus’ system as a black box

As it turns out, all the dichotomies mentioned are real and the problem.^' more difficult members of each pair present are mdeed — We system accepts inputs^ P'\_"™ °e“n the definition of a transfor-also"^ may ask for ad—inpuU aM/or speak, with its environment.

Annint the reader should observe that reactive systems cohere From micXve ovens and digital watches, through man/machine based software systems, siljcono^2;nrgO^e“d complex

The transformational reactive dichotomy cuts across all the aforementioned ones: both types of systems can be deterministic or not, terminating or not, on-line or not, and contain concurrently executing components or not. Also, reactive systems can be required to respond in real-time or not, and the cooperation of their components can be required to be synchronous or not. What then is so important about the distinction we are making, and why are we claiming that it is the reactive nature of systems that is problematic?

## What is the Problem?

The answer to these questions seems to us to be rooted in the notion of the behavior of a system. While the design of the system and then its construction are no doubt of paramount importance (they are in fact the only things that ultimately count) they cannot be carried out without a clear understanding of the system’s intended behavior. This assertion is not one which can easily be contested, and anyone who has ever had anything to do with a complex system has felt its seriousness. A natural, comprehensive, and understandable description of the behavioral aspects of a system is a must in all stages of the system’s development cycle, and, for that matter, after it is completed too.

Taking a very broad and abstract view, we may describe a typical top-down development process as a sequence of transformations:

```
s(°)) -+ (MW, sP>) ---------► (M^, s('))
```

The structure studied at each level is a pair (M^\_\ S^) comprising a specified system at the i’th level of detail; is the i’th level physical, or implementational. description, and is the behavioral specification. At the top level might be highly underspecified, with using such vague terms as “a data-base system responding to conjunctive queries”, “a plane for interception”, etc. Each level, even the O’th one, needs some description of the interface of the system with its environment. This can be done by including a list E^ in each of the M^, containing descriptions of those input and output channels, signals, requests and responses, that constitute the system’s interaction with the “outside world”. The level of detail in the interface lists can also vary with i, from highly abstract items such as “request communication” or “display target”, all the way down to concrete lists of buttons, levers, displays and alarms. The corresponding behavioral specification should characterise the desired behavior of •the system, in as complete a manner as possible, using the elements of

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

```
Now, there have been numerous suggestions and formalisms to he used it. the deve opm^ a stepwise approach of these are extremely helpfel, an g^ well.structured such as the one just outlined. 1 y . development in a top-
r,.".....-™. -«■ ■“
certain kinds of formal reasoning.
```

However, as it turns out, the methods structured and coherent development ” .[possible, acUally formaiional in nature. In transformat y eflectjng the natural Lghly desirable, to decompose he %Ze"1 to toother words, “structure of the problem , as i is transformation, a high-level description of the problem m the form of th in or function, that the system >s o Ue .ame species, in the these methods into several smal er p appropriate identifications form of lower level transformations, with the app P made among incoming and outgoing items. Each lower level transformation is then considered in its own right, and further decomposed. This is but another way of saying that each S(t+1) consists of a set of transformations, each of which was obtained from a transformation in S by transformational, or functional, decomposition. The system description is then taken to match the transformations described in S^,+ as closely as possible.

This is admittedly a very crude and sketchy account of such methods, but the point we wish to make is that the procedure it illustrates works nicely for transformational systems because transformations decompose naturally into other transformations, and implementations of transformations decompose into implementations of other transformations. It is therefore a small thing for one to observe that the two decompositions can (and then even recommend that they should) be essentially the same, or at least that they be related via a simple mapping. This is particularly attractive due to the fact that transformational decomposition provides not only static information but also the dynamics necessary for a good behavioral description. For example, a conventional structure diagram or a function tree, two of the kinds of descriptions recurring in the literature, can be given clear operational meanings when considered for transformational systems: inputs (data and/or control) flow into boxes, modules or functions, which proceed to perform their designated transformations, yielding outputs which in turn flow into others, etc. This is a wholly satisfactory behavioral description of a transformational system.

It is for these reasons that in most software engineering views of the life cycle of a system the specification stage is more or less followed by the design one: decompose the problem (=specify), and then use its parts and their interconnections as the basis for planning the implementation (=design). This idea is also one of the implicit mottos of structured programming: let the structure of the program reflect the structure of the problem, or, as one might say, let chunks of implementation (e.g. procedures, blocks, tasks, etc.) be made to correspond to chunks of behavior.

Our main argument here is that this cheerful situation does not apply to reactive systems at all. In a reactive system, even a pure software one, it is not clear if or how complex behavior can at all be decomposed beneficially into chunks, let alone for that decomposition to become the basis for system design. This observation notwithstanding, it is ironical that a breakup of the behavior is precisely what will eventually have to be found, whether one likes it or XnMsX-, consist of various increasing y mor existence, have to hardware or mixed), each of which will by 1Uve^ye ; have some kind of associated behavior. doping the system will most probably be reactive themse ■ ’ decomposition, which, one ultimately have to involve some kin of phy iora, dccomposition way or another, will have to be matched oy a u tO0' Let us for now however, ioral descriptions of reactive sys eacljTe behavior itself. How does s’s.. for behavioral description.

(i) u should provide descriptions that are welLstructured, conc.se, unambiguous, readable, and easy to understand.
(ii) It should be solely descriptive, eliminating, or at least mimm.tmg, dependence on any implementation! issues.

Requirement (i) implies that ‘^"rttXoXX descZTon";het the Z'r'al decomposition of the probiem rather than that of the implementation.

## A Method for Behavioral Description

```
The sMfe^rf, method was introduced ' luprXof
XXltXX TXmi-Xd the system’s and
```

it consists of describing the system’s behavior in terms of states, events and conditions, with combinations of the latter two causing transitions between the former. Both states and transitions can be associated in various ways with output events, called activities, which can be triggered either by executing a transition or by entering, exiting, or simply being m a state. The system’s inputs are thus the (external) events and its outputs are the (external) activities; their union comprises the interface set E.

This, as the reader can no dout see, is a standard and well-known idea, and is actually a simple combination of the Moore and Mealy definitions of finite state automata. The allowed sequences over E correspond to the language accepted by the automaton. Moreover, such automata come complete with a standard visual renderation, the transition diagram. T is classical state transition method, however, has been all but abandoned as a way of specifying the behavior of complex systems since it provides no modularity or hierarchical structure, and suffers acutely fropi the exponential blowup in the number of states that need be considered, and hence also in the number of transitions. Indeed, a state/event description seems to have to consider all possible combinations of states m all the components of the system; hence the exponential growth.

The statechart method is rooted in an attempt to revive this old and natural way of thinking about a system’s behavior, by extending it in several fundamental ways aimed at overcoming the aforementioned difficulties. The extensions apply to the underlying nongraphical formalism too, but personal preference towards visual descriptions has led us to present the ideas in terms of the graphical version. Some of the extensions are now briefly described, but the reader is strongly advised to consult the original paper for the others, as well as for a detailed example and further discussions.

States in a statechart can be repeatedly combined into higher-level states (or, alternatively, high-level states can be refined into lower-level ones) using AND and OR modes of clustering. Fig. 3 shows a state B whose meaning is “to be in B the system must be in precisely one of D, E or F” and Fig. 4 shows a state A whose meaning is “to be in A tfie system must be both in B and in C.” Notice, however, that in Fig. 4,B and C are themselves OR states, thus the actual possibilities are the state configurations (D,G), (E,G), (F, G) and (F,H). We say that D, E and F are exclusive and B and C are orthogonal.

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

The statification method is purely behavioral and requires of its user to think in terms of the system’s conceptual states and their interconnections. It caters for modular “chunking” of behavior in several ways, most notably by using exclusivity and orthogonality of states, and provides the mechanisms needed for manipulating these modules as separate entities. Statecharts are strongly oriented towards “deep” structured descriptions that are organized into many levels of detail, and permit “zooming easily in and out of these levels. One can construct them in a disciplined hierarchical "way, statifying a system level by level, or use interlevel transitions and vary the depth as deemed appropriate. Statification can proceed by top-down refinement, bottom-up clust zing, or a mixture of both. Note that the exponential blowup in stat .s does not arise here at all, as the option of using orthogonality on any level eliminates the need for explicit consideration of all state combinations.

As a truely simple example of the way statechart levels refine reactive behavior, consider the system whose interface set E is as in Fig. 6. Its behavioral specification is given on two succesive levels in Figs. 7 and 8. The allowed sequences in Fig. 7 can be described by the regular expression

```
B{ • (a • Bl • a • Bi‘)w U B\_ • (a • Bl • a • Bj)\* • (Bf U a ♦ B?)
```

where Bi = (6UeUd) and Bq = (6UcUe). The version in Fig. 8, on the other hand, refines the allowed behavior to the sequences given by the same expression, but with B\ = (6U i>cd), and Bq = (£>U bee).

This, then, is the formalism we wish to recommend for specifying reactive behavior. It is important to observe that the description can be made to reflect the statifier’s personal and natural view of the system’s behavior free, if so desired, from implementational details. If lifting a receiver conceptually causes a communication system tc. enter conversation mode, and this mode entails certain actions, one can say just that, disregarding such questions as which component is responsible for sensing the lifting of the receiver and how the sensed fact is communicated to the others. Of course, the crucial problem here is bringing this concep ua description down to earth; meaning, how does one combine it with.the natural implementational process of breaking the system down into >ts physical parts and their interconnections.

```
Fig. 6: A reactive system with its interface set
A v ♦ Fig. 8: A refined statechart
Fig. 7 : A statechart
```

## The Magic Square of System Development

Now that we know how to decompose reactive behavior, we can attempt to apply the “problem structure matches system structure pnnci-plXdeedJf there are no limitations on the implementation at all one can do just thai; refine the behavioral specification by adding sta tec hart level as illustrated above, and then perform the implementations! refinemen to match. While this might sound overly naive, in a pure software tem with a sufficiently high-level programming language the ^tech^rts can be directly encoded into software, with multi-level orthogonality being translated into nested concurrency. This applies to other possible methods for reactive behavior specification, such as Petri nets or languages like CCS.

It is clear, however, that the vast majority of interesting reactive systems feature various preconceived, unavoidable limitations on the structure, distribution, capabilities and interconnections of their implemena-tional components. Examples include geographical distribution of portions of an airline reservation system, standard components of an avionics system, physical limits on hardware components and their interaction, etc. Even concurrent programs are, in general, not all that pure, as one typically is constrained by a limit on the maximal number of concurrently executing processors. In this way, if the implemenational restricions are to be honored, being overly liberal in the use of orthogonality, for example, can easily cause severe problems in a.naive attempt to model the implemenational refinement according to the behavioral one.

What this means is obvious: our recommendation for a method that enables natural behavioral decomposition notwithstanding, the impleman-tational description has a nasty habit of prescribing, at least in part, its own decomposition, which need not, in general, match our conceived behavioral one.

These observations prepare the ground for a very simple idea: by and large, the development of a reactive system is not a one-dimensional process in which specification and design are two temporally related stages, but rather it is a two dimensional “magic square” in which they play the role of the dimensions themselves. One might label the two dimensions simply “specification” and “design”, but we prefer to use those terms as verbs, and so we label the dimensions “behavior” and “implementation”. One thus specifies the system’s behavior but one designs its implementation. See Fig. 9.

Fig. 9 : The magic square

Along both dimensions making progress amounts to supplying more detail but the two axes involve fundamentally different kinds of detail. Proceeding vertically (downwards), one is bringing the system closer o its final form by supplying more information about its implementation, and proceeding horizontally (rightwards), one is fine-tuning the system s performance by providing more information about its behavior. In either case and this explains in part our use of the term “magic square , every line or column amounts to a full, stratified, description of the system along one axis, but at a fixed level of detail along the other.

Ideally, the development process starts at the upper leftmost point, with nothing known about the system’s intended behavior or its desire implementation, and ends at the lower rightmost point with everyth g known about both. The more subtle side of the term “magic: square > rooted in the many possible ways of traversing the square from its initial point to its final one; following any of these correctly should result in the system being fully specified and fully designed.

It seems almost an ac dent that for the easier systems in our dichotomy, i.e. transformational ones, or reactive ones with no implem tational Constraints, this process can actually be linearized by, m essenc , mapping one dimension onto the other relatively easily as discussed ear-lier In our opinion this accident is the heart of many misconceptions and difficulties encountered in the development of complex systems, and some extent also in pure concurrent programming.

We are aware of the fact that even with concrete formalisms in mind any discussion of such a general model for system development is bound to seem naively idealistic when considered for real-world applications, ertheless, we are determined to describe our model m the simplest•P°«'b terms, and for that purpose, besides adopting simple statecharts, free global constraints, for the behavioral axis, we adopt a very simple dec position method for the vertical, implementational axis.

At level 0 of the vertical axis the system resides as an unspecified entity Ml0’, together with its interface set E«». Progressing down the verticalTaxi; is characterised by a step of implementat.onal decompose tion For a typical descent from level i to level t + 1, a subsytem M level i, with interface set E, might be decomposed into its constituent components Mi.......M„, with their interface sets Ei,...,E„;

For this decomposition to be acceptable certain obvmus property must be satisfied For exampie, each element of E, the interface set of M, must a^ar Tn at least »M sd Ej, or at least be refined into more concrete elements, each of which appears in at least one Ej.

Fig. 10: Implementations! decomposition

In addition to interface elements that are external to the whole system, the interface set Ej of Mj may contain additional elements which are external to M.- but internal to M. These dements provide the components ■with the ability to communicate, synchronize, and influence one another. Thus, each element in Ej - E must be tagged with some indication as to its source or target subsystem(s) from among the others. We shall not go into more detail here so as not to detract attention from the underlying issues. Besides, our presentation of this decomposition method is highly simplified anyway, and many standard methods can be readily adopted for a satisfactory treatment of the implementational axis.

In contrast to making progress down the vertical axis by refining the implementational design of the system, progressing along the horizontal axis refines and structures its behavior, and as discussed above can be thought of as adding levels to the appropriate statecharts. Having reached some fixed vertical level t, one has essentially decided upon a set of implementational modules, say and now proceeding horizontally at this vertical level amounts to statifying each of these. The outcome, of course, is a set Si,..., Sk of statecharts whose interface sets are simply those of Mi,, Mk.

As a side remark, note that the magic square is not a square at all. First, there is no reason whatsoever for the levels of implementationa e-tail to be equal in number to those of behavioral detail, so that at the very best the development model should be called a magic rectangle. Secondly, and more significantly, the implementational decomposition, even using the simple model above, forms a tree, and one whose branches are not necessarily of equal length, so that the outcome is more like a tree with 11 Thirdly and most significantly, for any given long sprkes; see Fig. 11. ™ m compOnent) the behavioral denode in the implementation tre ( y is actually a scription itself, even using simple statecharts on th amongst or tree or worse, again with no uniform , actual development within each other. For a fixed. sys em er ultidimensional tangled

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

The dual traversal calls for a complete behavioral specification prior to any implementational decomposition, and was hinted at earlier. Neither of these traversals of the magic square can be particularly recommended for complex systems. Actually, neither of them makes essential use of the available two-dimensionality at all, and as a consequence neither requires that behavioral descriptions be projected in a nontrivial way from one vertical level to the next. This kind of behavioral projection, however, is one of the most crucial aspects of our magic square, as we now set out to show.

## A Consistency Criterion for The Magic Square

In general, we wish to argue, a healthy development process prescribes some horizontal progress prior to each significant progress made on the vertical level. That is, at vertical level i system component M is given a behavioral specification S of certain depth, that is, extending to some horizontal point. One then decomposes M (or is provided with a decomposition of M) into its subcomponents Mi,..., Mn and somehow specifies the behavior of each, to the same horizontal depth, yielding the preliminary S{,..., S’n. The S’. are then refined as discussed above, yielding the final behavioral descriptions S\,..., Sn of vertical level t + 1. Of course, this set of behavioral descriptions of the Mj has to be consistent with behavior

```
Fig. 12: Traversing the magic square
CM
```

the behavioral description & of the higher-level system M, and we define the nature of this consistency below. The general progress can thus be schematically described as in Fig. 12, with the progress arrow aiming and hitting the final point corresponding to the fully-specified, fully-designed system. Each shaded area in Fig. 12 thus represents the collection of behavioral descriptions of all subsystems relevant to level i of the implementation.

At the expense of sounding repetitious we remind the reader of Fig. 11 and its more realistic, hence far more complicated version of our simple “square”, meaning that the S' of each Af on any level is given at the depth of behavioral detail appropriate to it and its “neighbor” subsystems. However, as mentioned earlier, for our purposes the issues can be discussed under the pretensions implicit in Fig. 12.

Three questions come immediately to mind:

(1) What is, or should be, the precise consistency criterion relating SW to
(2) Given a satisfactory answer to (1), can one recommend a recipe for obtaining from the decompositions carried out when progressing downwards from level i to level t 4- 1, together with
(3) Whatever the answers to questions (1) and (2) are, can one recommend a “good curve” for traversing the square?

Question (1) is purely technical, and without answering it satisfactorily the whole magic square model collapses. There must be a firm and precisely defined connection between the specified behavior of a portion of the system and that of its constituent components, one which then transcends to become a global connection between the initial and final stages of the entire development process.

The answer to question (1) can be stated informally as follows:

The external behavior implicit in must be equivalent to that implicit in Sz(,+1\ the preliminary behavioral description on level i 4-1 which is of the same horizontal detail as S(‘).

This simple answer contains some subtlety, since apart from the haziness of “external”, “implicit” and “equivalent”, sW, in our chosen framework of formalisms, is but a collection of statecharts, one for each component on level t, and Sz(,+1) is a different collection, assoc ated with a different level and different components. Nevertheless, the answer can be made precise quite naturally, as ..justrated in Fig. 13.

Take a typical level i component M and its subsystems Mi,..., Mn on level i -I- 1. In SW there will be a statechart S for M and in S^,+1) statecharts S'J,..., S'n for the Mj. As discussed earlier, each pair (Mj, S'.)

## System Components Behoviorol Descriptions

```
LEVEL i. LEVEL i + 1 M 1 decomposition Ej En _ ••• Mfl E S | question (2) E| E„ ♦ [ s; ] ... [ s; J 11 refinement E. E_ \_ 12lj Is" ]
```

## CONSISTENCY CRITERION

external behavioral equivalence

Fig. 13: The consistency criterion for the magic square has an interface set Ej, only part of which is extern^ { by corresponding directly to the £ of (M,\_ of simplicity let ns assume t discussed above, each selves refined in the transition to the S internal to Ei 'Til °f e'eM? Now form a new statechart S’ by simply placing {Ade by^de as orthogona! components. Their inte«ommrtm» via the interna! interface sets Ej - whose chart formalism itself, n whtch are not interna! to the cc «-• •• ’ •• " set of sequences over E.

If this equivalence holds when applied to each and every implemen-tational component on level, we say that ?e latter “t TFnsX^ former, together wi^ the fact that S^, the tri"y a""of deta”to the statecharts therein, thereby refining the behaviors they define.

In the case where E is indeed refi°^ ™^^0^ of consistence, tion, the notion of equivalence and imcor^ S? matching of interface has to be appropriately modifie af.roTnDanied by a set of additional elements. Also, if the sta^ar ’ amentioned earlier, the refinement of I1.?.1?') Ct"must\* adhPere to tJose, and hence might require a^parat^ straints too m the process of ma ing statecharts do, then relativize to the interface sets of each level, just a resulting in a for level 1, and,^^eroiis other possible consistency will have to change to . > the magic square, th:basic model in a natural way' ,-nd with the underlying principles being the same. nr thP definition of local consistency between The mam consequence of that consistency is vertical levels is in its transitivity. By this we m propagated down (or up) the vertical axis, resulting in the following fact:

If a complete development process is carried out in the magic square model, using any desired traversal, while checking local consistency, the final behavioral description of the system, S^), is consistent with the initial one, S(°). In other words, if one constructs the entire system using the “atomic” implementational components prescribed by the final vertical decomposition level f and connects them as prescribed by the interface sets on that level, and if one then convinces oneself that each of these low-level components behaves as prescribed by its behavioral description in then the entire system is correct with respect to its initial specification

This, by the way, should remind the reader of classical methods for program verification, where global correctness follows from the correctness of the consituent modules.

Precisely how one convinces oneself of the behavioral correctness of the ate nic components is of no concern here. It might follow from a manufacturer’s documentation, a programmer’s verification, or be regulated to mere belief. Just as in any typical verification process, the soundness of one’s use of the magic square in this fashion is a doubly-relative concept; it relies on an accepted initial specification, against which one verifies what one has constructed (in this case this is the initial behavioral specification S(0)), and it relies on an “axiomatic” acceptance of the fact that the atomic elements, which constitute the building blocks with which one has carried out that construction, are correctly specified (in this case this amounts to accepting the final vertical level as is).

At this point, one might be tempted to ask the following question: if the S and S* appearing at a certain stage in the process (see Fig. 13) are required to be two equivalent descriptions of the same part of the final system, given in the same formalism, and over the same interface set E, why then is S* not constructed directly? Why was S\* not given as the level i behavioral description of component M, especially since it is already conveniently decomposed in accordance with the decomposition Mi,..., Mn of Ml It goes without saying that this would eliminate any necessity for checking the equivalence of behavioral descriptions. The answer, of course, embodies the main issue here: S\* is not necessarily a natural behavioral description of M because it is composed according to Mi,.., Mn. A good behavioral description of an airline reservation system which uses ten geographically distributed computers and a thousand terminals might be one whfch decomposes in ways that cut across this physical decomposition j^st as a good behavioral description of a VLSI chip need not be given’in terms which even mention its breakup into design-related bloc s. Whatever the case, the “unnatural” S‘, which consists of the behavioral descriptions St.....Si of the components Mi,.. ,, has be prepared somehow; but how? This is precisely question (2) above.

## How to Traverse the Magic Square?

We are in no position to present detailed answers to questions (2) and (3) and even less so to claim that we know of answers that can or should be’used uXersally. Quite to the contrary, different kinds of systems present different kinds of problems in behavioral 8Pec‘^at'on’ entire development process can be regarded as an art, with many and many possibilities.

Moreover, more often than not, a complex development effort does not start at the initial point of a totally blank magic square. It usually starts S ™ OUS portions of the square already filled in. That s, certain system comjxments, and even certain chunks of behavior, are already presented to”he developer in advance, and the development process must accomodate them as it proceeds. Therefore, as far as question (3) is concerned, we can only say that, when viewed as a function that plots honsontal progre s agains/vertical progress, the development curve should be monotonically S (see Fig 12); it makes very little sense to provide subcomponent with less behavioral detail than its parent component. However, other than that, and other than observing that the curve should Pr°bab£ be nontrivial (i.e., not L-shaped or its dual), developers should be free define their own preferred curves for traversing the square.

As to question (2), there is one general point to be made here. Let M be a component on vertical level i, decomposed on level . + 1 into az. . and let S be the behavioral specification of M. If B and Ei ’... En are the interface sets of the components (no refinement in the E’s; as’above), then one can proceed as follows: for each 1 < 3 n, s ar with S itself as a first approximation to Sjt the behavioral specification of Mj on level t + 1.

Now, clearly S is not a legal statification of Sj in general, since it refers to elements from E — Ej. However, this can be fixed as follows. Output elements in E - Ej are simply eliminated, and for each input element e therein one finds a k with e € Ek, and modifies the two copies of S, that of Ek and that of Ej, so that the former, whenever e is sensed, outputs a new item e' to Mj, in whose copy of S each e is replaced by e . In this way Mj can sense the input event e even though it can be directly sensed only by Mk. The resulting statecharts, call them Sf,..., Sn, are now legel behavioral specifications of the Mj, in the sense that their orthogonal product is equivalent to S. Moreover, the Sj are on the same horizontal level of detail as S. These S’!, therefore, conform to the definition of the preliminary description of see Fig. 12, and hence, in principle, we have answered question (2). However, we clearly do not recommend that one stop here; the result will be an exponentially growing behavioral specification, not to mention its complete detachment from any naturalness involved in the implementation refinement of M into the Mj. Rather, one should work on the S", simplifying and changing them to reflect the intended behavior of the Mj. In this sense, the only useful role S'! can play, is that of a starting point leading to the desired Sj, the final behavioral specification of Mj.

Actually, we feel that it is worthwhile to search for good transformations for weeding out portions of S'- not really relevant to Mj, using the difference between E and Ej, and S itself as directives. Such transformations, certain simple examples of which come immediately to mind, should be required to preserve equivalence of the behavior, modulu the transition from E to Ej.

The equivalence problem for reactive behavioral specifications, and in particular equivalence-preserving transformations of Statecharts, seems to be an important area for future research. Satisfactory and useful results in this direction can help turn the magic square from a model of system development, which is the way we have tried to portray it here, into a detailed methodology, or prescription, a line we have not yet tried to pursue.

Acknowledgement

The contents of this paper owe much to many colleagues and authors. In particular, we have been influenced by several ideas found m the work of M. Alford, L. Lamport and D. Parnas.
