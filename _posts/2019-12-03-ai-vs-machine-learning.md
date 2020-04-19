---
layout: post
language: en
created: 2019-12-01 16:15:00 (CET)
title: AI vs ML vs robotics
tagline: real differences between AI and ML
description: An AI system imply reasoning, while machine learning just imply correlation.
authors:
  - jeblad
categories :
  - other
tags: robotic process automation, robotics, RPA, machine learning, artificial intelligence, weak AI, strong AI, hard AI, soft AI, wet AI embodied AI
licenses:
  - cc-by-sa-4.0
sources:
  Deloitte:robots-coming-global-business-services:
    publisher: Deloitte United Kingdom
    title: The Robots Are Coming
    access-date: 2019-12-03
    year: 2015
    url: https://www2.deloitte.com/uk/en/pages/finance/articles/robots-coming-global-business-services.html
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
---

The same claim about [artificial intelligence](https://en.wikipedia.org/wiki/Artificial_intelligence) (AI) seems to emerge time and again; we have this system, it has some kind smartness built in, and surely it must be an AI-system. It seems like this misconception is partly from an idea that all machines with smartness must be an AI-system, and partly that sales departments wants to boost the idea that some product is especially smart so they call it an AI-system. It may not be far from the most *common explanation* of “AI”, but it is actually quite far from real “AI”.

<!--more-->

{% include popular.html %}

This explanation that seems to have stuck is that artificial intelligence (AI), is any kind of smart system that has some function that is assumed to be human-like or does human-like things. This has given rise to an idea that for example an app on the cellphone that is able to recognize faces is an AI-system, and an office program in a bank that can make decisions on loans is definitely an AI-system. These assumptions are false. The first system is (often) a [statistical classifier](https://en.wikipedia.org/wiki/Statistical_classification), well-known from [machine learning](https://en.wikipedia.org/wiki/Machine_learning), and the later system is an [expert system](https://en.wikipedia.org/wiki/Expert_system) based on stringent rules, now often called [robotic process automation](https://en.wikipedia.org/wiki/Robotic_process_automation) or simply shorten to *robotics* by {% include cite.html id="Deloitte:robots-coming-global-business-services" %} and others.

Note how the linked articles at Wikipedia keeps describing these technologies as “artificial intelligence”. It is the common explanation that keeps creeping in.

### Weak vs Strong AI

Real artificial intelligence is about building [minds](https://en.wikipedia.org/wiki/Mind), which consists of consciousness, imagination, perception, thinking, judgment, language and memory. Even if each one of these are important, underpinning all of them is [reasoning](https://en.wikipedia.org/wiki/Reason), or *how to make sense of things*. Reasoning is a core trait that divides artificial intelligence from mere machine learning. This is discussed by {% include cite.html id="DBLP:journals/corr/abs-1102-1808" %} and others. To make a real AI the system must not only have a [knowledge base](https://en.wikipedia.org/wiki/Knowledge_base) and some means of running an [inference engine](https://en.wikipedia.org/wiki/Inference_engine) on that, it must also be able to learn new knowledge for the knowledge base and new rules for the inference engine. If the attempt is to build a full mind it is called a *strong AI*, and if the attempt is only to build part of a mind it is *weak AI*.

No one has ever built a strong AI, but from time to time some claim they have built a weak AI. What they have built are usually a narrow AI.

### Narrow AI

Within AI there are some areas that are even more specific than weak AI, it is called *narrow AI*. One definition is that narrow AI is an application of artificial intelligence technologies to enable a high-functioning system that replicates human intelligence for a narrow and dedicated purpose. In this respect it is not concerned with a mind, just to replicate some part of human intelligence or just behavior, it is a virtual lookalike for a human in some very limited respect.

A lookalike may act and behave as the real thing, but it is not the real thing. A narrow AI may do actions and give impressions as if it has human intelligence, but it has not, it is just replicating for the purpose of doing some very narrow and dedicated actions.

It is sometimes said that narrow AI and weak AI is the same, but this author disagree with that.

### Classifier

A classifier has a kind of knowledge base that describes whats being classified, and can make astonishing classification tasks, even surpassing human abilities to classify some images. It can be set up to feed its classifications into an annotator generating text. If that is done for movies you can get annotated films like for Netflix. It looks like some human has annotated the films, but it is a classifier with an annotator. The system is a chain of machine learning tasks that forms a narrow AI – it is a lookalike. Perhaps even more important, the classifier in this case forms a knowledge base and the annotator a kind of inference engine, although they are usually not connected so they act this way.

### Robotics

Robotic process automation (RPA) builds on expert systems, and have a knowledge base and an inference engine. Historically they was hand coded and could not learn. The more modern counterpart, the RPA, has often a limited ability to learn. A system living sort of in between has an inference engine with a local knowledge base that stores knowledge itself. When trained an RPA act like very limited human intelligence on the field for a narrow and dedicated purpose – it is a lookalike. It does not try to implement a part of mind, so it is not a weak AI. Still, it is so tempting to call it an “AI”.

### … and there are more

Artificial intelligence is split in several more subfields. There are hard, soft, and wet AI. The first is an AI implemented in hardware. This is often necessary as the involved computation is quite heavy. The next is soft AI, which is an AI implemented purely in software. It is questionable whether this is possible given the present general hardware. What might be possible is to build some general hardware that are still specialized for AI purposes, and then implement a soft AI for that hardware. The third is an AI implemented in some kind of biological tissue. This is for the time a theoretical endeavor.

Then it is this highly hot topic of embodied AI. Is it necessary for an strong AI to have a body, and to experience the world? Some researchers say so, while other disagree. If it is so, then it will strongly limit what can be called a strong AI. It will also make a question *what is a sufficient body*. Is it necessary for a sentient being to open a fridge, take out a beer, and watch CNN?

Be careful when describing something as an “AI” if it is merely a “narrow AI”. Use other terms like “machine learning”, they are far more descriptive. Calling an RPA or similar systems for intelligent gives a false pretense of real AI, which such systems are not.
