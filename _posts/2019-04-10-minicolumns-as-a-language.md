---
layout: post
language: en
date: 2019-04-10 03:20:00 (CET)
category : neural nets
title: Minicolumns as a language
tagline: the strange similarities
tags : formal languages, minicolumn
description: A formal description of minicolumns as functions connecting an input domain to an output domain has striking similarities to formal semantics, and thus what we can do with a neural network.
authors:
  - '[John Erling Blad](/authors/jeblad/)'
license: cc-by-sa
---

There are striking similarities between processing in [cortical minicolumns](https://https://en.wikipedia.org/wiki/Cortical_minicolumn) and representations in [formal languages](https://en.wikipedia.org/wiki/Formal_language) in [logic](https://en.wikipedia.org/wiki/Formal_semantics_(logic)), [linguistics](https://en.wikipedia.org/wiki/Formal_semantics_(linguistics)), the form used in [mathematical logic](https://en.wikipedia.org/wiki/Mathematical_logic), and in particular the [triplets](https://en.wikipedia.org/wiki/Semantic_triple) from [semantic web](https://en.wikipedia.org/wiki/Semantic_Web). There are input vectors representing symbols, functions that relates those input vectors to output vectors, and those output vectors are also symbols. These can be directly compared to the *subject–predicate–object* expression from semantic triples. When trying to implement this in [machine learning](https://en.wikipedia.org/wiki/Machine_learning), and in particular [artificial neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network), it has some very real consequences.

<!--more-->

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

Note that the previous has no natural zero-element. This creates some pretty weird problems, also known from semantic web. It shows up as exceptions, being handled as "[snaks](https://www.wikidata.org/wiki/Wikidata:Glossary#Snak)" with `no value` and `unknown value` in systems like [Wikidata](https://wikidata.org).

In an ideal world a single function, that is a single total learned transfer function for a single neural layer, might take the whole input vector and produce a whole output vector in one fly. That would be a tempting approach, but note that this would also imply adjusting the whole learned function, which is a representation of a training set of $T$ samples. With $T$ being very large the learning rate will be very small to achieve stable learning. Learning from each sample would be $1/T$, thus the learning rate has to be less than this number. (This might be viewed as on-line [transfer learning](https://en.wikipedia.org/wiki/Transfer_learning), but note that $1/T$ is a gross oversimplification.)

A corollary to this is that a small correction in transfer learning should be taken in smaller steps if the previous learning set was large, otherwise learning would step out of the finer manifold defined by the larger training set. The large single function leads to a large training set, which gives small training steps. Together with a large layer this makes the overall processing needs explode. In fully connected neural layer learning is a $O(\alpha TM + \beta NM)$ problem where $N$ being number of input nodes, $M$ being number of output nodes, and $T$ being number of training samples. In general $\alpha$ and $\beta$ are unknown, so both therms should be kept low, that is better keep $M$ low or keep the number of output nodes low.

How can we keep the implemented function simple, without sacrifice precision, and hopefully also limiting the training set?

We can partition the total global world into smaller local worlds. The size of the function is limited (that is the number of nodes) and the necessary training set is also limited. If we spell it out; the function is the predicate in the triplet, and it is obvious that it is a kind of subworld in a larger world, thus its scope is somewhat limited.

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