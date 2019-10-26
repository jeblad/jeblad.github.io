---
layout: post
language: en
date: 2019-04-10 03:20:00 (CET)
provision:
  2019-04-10: Created article
  2019-05-01: Added sources
categories:
  - neural nets
title: Minicolumns as a language
tagline: the strange similarities
tags : formal languages, minicolumn
parent: "neural_net"
description: >-
  A formal description of minicolumns as functions connecting an input domain to an output domain
  has striking similarities to formal semantics, and thus what we can do with a neural network.
authors:
  - jeblad
license: cc-by-sa
theorems:
  proposition:
    title: Simple World
    description: >-
      In a simple World a sufficient language can be described as a set of inputs set to
      constant values, processed by functions, which outputs new constant values. The
      constants …
  corollary:
    title: Complex World
    description: >-
      Some description of what this is… $E=mc^2$ And a bit more.
sources:
  DBLP:journals/corr/abs-1803-03067:
    type: journal
    title: Compositional Attention Networks for Machine Reasoning
    authors:
      - Hudson, Drew A.
      - Manning, Christopher D.
    journal: CoRR
    volume: abs/1803.03067
    year: 2018
    url: http://arxiv.org/abs/1803.03067
    archivePrefix: arXiv
    eprint: '1803.03067'
    timestamp: Mon, 13 Aug 2018 16:46:02 +0200
    biburl: https://dblp.org/rec/bib/journals/corr/abs-1803-03067
    bibsource: '[dblp computer science bibliography](https://dblp.org)'
  jpNLp9SnTF8:
    type: conference video
    title: A Neural Network Model That Can Reason
    lecturers:
      - Manning, Christopher D.
    date: 2018-05-04
    url: https://www.youtube.com/watch?v=jpNLp9SnTF8
  DBLP:journals/corr/abs-1102-1808:
    type: article
    authors:
      - Bottou, Léon
    title: From Machine Learning to Machine Reasoning
    journal: CoRR
    volume: abs/1102.1808
    year: 2011
    url: http://arxiv.org/abs/1102.1808
    archivePrefix: arXiv
    eprint: 1102.1808
    timestamp: Mon, 13 Aug 2018 16:48:17 +0200
    biburl: https://dblp.org/rec/bib/journals/corr/abs-1102-1808
    bibsource: '[dblp computer science bibliography](https://dblp.org)'
  DBLP:journals/corr/abs-1802-03691:
    authors:
      - Chen, Xinyun
      - Liu, Chang
      - Song, Dawn
    title: Tree-to-tree Neural Networks for Program Translation
    journal: CoRR
    volume: abs/1802.03691
    year: 2018
    url: http://arxiv.org/abs/1802.03691
    archivePrefix: arXiv
    eprint: 1802.03691
    timestamp: Mon, 13 Aug 2018 16:47:49 +0200
    biburl: https://dblp.org/rec/bib/journals/corr/abs-1802-03691
    bibsource: '[dblp computer science bibliography](https://dblp.org)'
  DBLP:journals/corr/abs-1802-08535:
    authors:
      - Evans, Richard
      - Saxton, David
      - Amos, David
      - Kohli, Pushmeet
      - Grefenstette, Edward
    title: Can Neural Networks Understand Logical Entailment?
    journal: CoRR
    volume: abs/1802.08535
    year: 2018
    url: http://arxiv.org/abs/1802.08535
    archivePrefix: arXiv
    eprint: 1802.08535
    timestamp: Mon, 13 Aug 2018 16:46:10 +0200
    biburl: https://dblp.org/rec/bib/journals/corr/abs-1802-08535
    bibsource: '[dblp computer science bibliography](https://dblp.org)'
  nowiki:
    authors:
      - Jeblad
    title: User:Jeblad/Minicolumns as a language
    collection: Norwegian Bokmål Wikipedia
    url: https://no.wikipedia.org/w/index.php?curid=1663621
    year: 2019
    timestamp: Tue, 12 Feb 2019 12:03‎ +0200
---

There are some striking similarities between [reasoning systems](https://en.wikipedia.org/wiki/Reasoning_system). Processing in [cortical minicolumns](https://https://en.wikipedia.org/wiki/Cortical_minicolumn) and representations in [formal languages](https://en.wikipedia.org/wiki/Formal_language), both as [logic](https://en.wikipedia.org/wiki/Formal_semantics_(logic)) and [linguistics](https://en.wikipedia.org/wiki/Formal_semantics_(linguistics)), and the form used in [mathematical logic](https://en.wikipedia.org/wiki/Mathematical_logic). In particular the [triplets](https://en.wikipedia.org/wiki/Semantic_triple) from [semantic web](https://en.wikipedia.org/wiki/Semantic_Web) has some striking similarities. There are input vectors representing symbols, functions that relates those input vectors to output vectors, and those output vectors are also symbols. These can be directly compared to the *subject–predicate–object* expression used in a semantic triple. When trying to implement this in [machine learning](https://en.wikipedia.org/wiki/Machine_learning), and in particular [artificial neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network), the similarities has some very real consequences.

<!--more-->

These similarities are apparent when neural nets are used in inference engines, and not merely as correlation engines. Many of the current high-profile use cases are for correlation engines, such as image classifiers and shallow query answering engines often known as chat bots. In inference engines a number of simple claims formed by single triplets are stringed together to form composite statements by composition rules. Such statements can then be used both as questions to the engine and answers from the engine.

{% include theorems.html id="proposition" %}

A single triplet can be viewed as the quite simple language $\mathcal{L}$

$$
\begin{equation}
\mathcal{L} = \left \{
  \underbrace{ x _i } _{ \text{subject} },
  \underbrace{ f (\cdot) } _{ \text{predicate} },
  \underbrace{ y  _j } _{ \text{object} }
\right \}
\end{equation}
$$

We have symbols $x$ and $y$, and a function transferring symbols from  $f(x) \to y$. The sets $x _i$ and $y _j$ would be subsets of a larger common set to be formally correct. Generalizing the symbols into vectors should not be a big leap of faith, and likewise the function into being a vector function.

A neural net trained as a typical correlation engine has no natural zero-element. It learns to classify known states, it does not learn to distinguish whats unknown. This creates some pretty weird problems. These often shows up in semantic web as exceptions. In [Wikidata](https://wikidata.org) they are handled as part of [snaks](https://www.wikidata.org/wiki/Wikidata:Glossary#Snak), given as `no value` and `unknown value`. The problem is also known from [natural language processing](https://https://en.wikipedia.org/wiki/Natural_language_processing), with words marked as `<unk>`.

The concept of “weak classifications”, the less probable states, could be interpreted as a zero-element. If all possible classifications goes towards zero, then that will approximate a zero-element. Thus we may have a rather exact zero-element for the output $y_i$, but for the input $x_i$ there might be large subspace that acts as a zero value.

A rather brilliant description of reasoning is “algebraically manipulating previously acquired knowledge in order to answer a new question” given by {% include cite.html id="DBLP:journals/corr/abs-1102-1808" %}. The previously acquired knowledge is what we used for training the neural net, the question is new inputs, the answer is new outputs, and the algebraic manipulation is how we string together functions. The algebraic manipulations can be strict logical expressions, but it can be a lot more.

To even further obfuscate the problem the inputs live at a manifold in one World, while the outputs live at a manifold in another World. If we can make the input manifold equal to the output manifold, then partial answers given as outputs can be feed back as reformulated questions to the input.

Some current attempts on building inference engines are tree-graphs for program translation by {% include cite.html id="DBLP:journals/corr/abs-1802-03691" %}, and for logical entailment {% include cite.html id="DBLP:journals/corr/abs-1802-08535" %}. These work quite well for unambiguous three structures. Another alternative is reasoning by composition of attention by {% include cite.html id="DBLP:journals/corr/abs-1803-03067" %}.

In an ideal world a single function, that is a single total learned transfer function for a single neural layer, might take the whole input vector and produce a whole output vector in one fly. That would be a tempting approach, but note that this would also imply adjusting the whole learned function, which is a representation of a training set of $T$ samples. With $T$ being very large the learning rate will be very small to achieve stable learning. Learning from each sample would be $1/T$, thus the learning rate has to be less than this number. (This might be viewed as on-line [transfer learning](https://en.wikipedia.org/wiki/Transfer_learning), but note that $1/T$ is a gross oversimplification.)

A corollary to this is that a small correction in transfer learning should be taken in smaller steps if the previous learning set was large, otherwise learning would step out of the finer manifold defined by the larger training set. The large single function leads to a large training set, which gives small training steps. Together with a large layer this makes the overall processing needs explode. In fully connected neural layer learning is a $O(\alpha TM + \beta NM)$ problem where $N$ being number of input nodes, $M$ being number of output nodes, and $T$ being number of training samples. In general $\alpha$ and $\beta$ are unknown, so both therms should be kept low, that is better keep $M$ low or keep the number of output nodes low.

How can we keep the implemented function simple, without sacrifice precision, and hopefully also limiting the training set?

We can partition the total global world into smaller local worlds. The size of the function is limited (that is the number of nodes) and the necessary training set is also limited. If we spell it out; the function is the predicate in the triplet, and it is obvious that it is a kind of subworld in a larger world, thus its scope is somewhat limited.

{% include theorems.html id="corollary" %}

Assume there is a language $\mathcal{L}$, organized as a 2-dimensional map, indexed by $i$ and $j$, such that

$$
\begin{equation}
\mathcal{L} = \left \{
  \underbrace{ \mathbf{x} ^{[i,j]} _k } _{ \text{subject} },
  \underbrace{ f ^{[i,j]}(\cdot) } _{ \text{predicate} },
  \underbrace{ \mathbf{y} ^{[i,j] } _k } _{ \text{object} }
\right \}
\end{equation}
$$

where $f^{[i,j]}(\cdot)$ is a function that takes an input $\mathbf{x}^{[i,j]}$ representing a symbol and transforms it into an output $\mathbf{y}^{[i,j]}$ that represents a new symbol, like $f(x) \to y$. Except for the superscript there isn't anything new from eq. 1 above.

The two symbols $\mathbf{x} ^{ [i, j] } _{k}$ and $\mathbf{y} ^{[i, j]} _{k}$ are high-dimensional vectors, organized as a set indexed by $k$. The indexes $i$ and $j$ are 2-dimensional indexes over a map of subworlds. This does not have to be 2-dimensional, it is just nice and it fits well with the minicolumn analogy.

### Consequences

The consequence of this is that when the brain adjusts weights in a minicolumn it has fewer nodes in a smaller world and needs less training. The processing complexity the minicolumn face can be several orders lower, and thus be much less demanding. Compare this to a digital neural network where input vectors with thousands of entries are processed. That makes the brain tick faster than a similar computer, even if the processing elements in the brain are quite slow. It is not because the brain is in any way inferior to a digital computer, it is because nature has found a better [paradigm](https://en.wikipedia.org/wiki/Paradigm) for computing these relations.
