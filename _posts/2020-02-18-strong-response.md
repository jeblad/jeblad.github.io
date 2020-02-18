---
layout: post
language: en
created: 2020-01-25 22:15:00 (CET)
title: Strong EPSP
tagline: strong synaptic response and multimodality
categories :
  - neural nets
tags :
  - epsp
  - strong epsp
  - chemical synapse
  - excitatory synapse
description: When a synapse responds strongly to an excitatory postsynaptic potential (EPSP) it fundamentally changes properties.
authors:
  - jeblad
licenses:
  - ccbyncnd
---

Some time ago I read a story on how an [excitatory synapse](https://en.wikipedia.org/wiki/Excitatory_synapse) could fire a much stronger [excitatory postsynaptic potential](https://en.wikipedia.org/wiki/Excitatory_postsynaptic_potential) (EPSP) if the local [dendrite](https://en.wikipedia.org/wiki/Dendrite) already was sufficiently excited. The response in this case was of the order 200 times stronger. This radically changes the behavior of the [neuron](https://en.wikipedia.org/wiki/Neuron), it does not anymore have an [unimodal response](https://en.wikipedia.org/wiki/Unimodality), it has a [multimodal response](https://en.wikipedia.org/wiki/Multimodal_distribution).

<!--more-->

It took some time before I realized the consequences this has for what a neuron can learn, and in the mean time I had forgotten where I found the article in the first place. If I find it again I post it here!

Assume the neuron has some base input, and some synapses gives a normal EPSP, but the total activation isn't enough for synapses to fire a strong EPSP. This is how a node in an artificial neural net operates. Now increase the input and activate more synapses, then synapses starts to give strong EPSP, and only a few synapses are enough for the neuron to reach threshold and fire a spike. This is not how an artificial node operate.

### Perceptron

An artificial node sums over all $k$ weighted inputs, and runs the sum through some kind of [activation function](https://en.wikipedia.org/wiki/Activation_function)

$$
\begin{equation}
y\left(t\right) = \operatorname{g}\left(\sum_k {w_{k} x_{k} \left(t\right)}\right)
\end{equation}
$$

- $\operatorname{g} \left( \cdot \right)$ is the activation function
- $w_{k}$ is the weights for each artificial synapse, similar to those used when EPSPs are fired

This kind of node is more commonly known as a [perceptron](https://en.wikipedia.org/wiki/Perceptron), especially if the activation function $\operatorname{g} \left( \cdot \right)$ is a [threshold function](https://en.wikipedia.org/wiki/Linear_classifier#Definition).

### Spiking neuron

If the node use a “spiking” function, then we could rewrite the previous as a simple integrating leaky bag

$$
\begin{align}
h \left( t \right) & \gets \sum_k {w_{k} x_{k} \left( t \right)} \\
y \left( t \right) & \gets
\begin{cases}
\left(1 - \beta \right) \left( y \left( t \right) + h \left( t \right) \right) & \mbox{if } y \left( t \right) < \alpha, \\
\left(1 + \gamma \right) \left( y \left( t \right) + h \left( t \right) \right) & \mbox{if } \alpha \le y \left( t \right) < 1, \\
0 & \mbox{if } 1 \le y \left( t \right)
\end{cases}
\end{align}
$$

- $\alpha$ – constant representing the spike threshold level, it slowly accumulates below and runaway above this level
- $\beta$ – constant representing the constant outflow from the leaky bag
- $\gamma$ – constant representing accumulation of the runaway spike

The activation function in this case is a resetting threshold function. Such a node will ramp up and spike as expected, even if it does it in an overly simplistic way. For our purpose it is although good enough.

### Strong spiking neuron

While the previous neuron does what's expected according to common conception, it is not quite what goes on when the synapses start to fire strong EPSPs.

$$
\begin{align}
h \left( t \right) & \gets
\begin{cases}
\sum_k {w _{k} x _{k} \left( t \right)} & \mbox{if } y \left( t \right) < \eta, \\
\sum_k {\hat{w} _{k} x _{k} \left( t \right)} & \mbox{otherwise}
\end{cases} \\
y \left( t \right) & \gets
\begin{cases}
\left(1 - \beta \right) \left( y \left( t \right) + h \left( t \right) \right) & \mbox{if } y \left( t \right) < \alpha, \\
\left(1 + \gamma \right) \left( y \left( t \right) + h \left( t \right) \right) & \mbox{if } \alpha \le y \left( t \right) < 1, \\
0 & \mbox{if } 1 \le y \left( t \right)
\end{cases}
\end{align}
$$

- $\hat{w}_{k}$ is the weights used when the strong EPSPs are fired
- $\eta$ the constant representing the strong EPSP threshold level

The normal EPSPs will now accumulate up to a strong EPSP threshold level, and after that level is reached strong EPSPs will be triggered. The normal EPSPs are fired in response to $w_{k}$, and then strong EPSPs in response to $\hat{w}_{k}$. That gives a pretty long first delay, and then a rush of strong EPSPs before the spike is fired.

### Discussion

So, what goes on here? The if-case in (eq. 4) are used as long as the strong EPSP threshold level is not reached. This is almost like a linear node (aka dendrite) in front of the soma. The otherwise-case in (eq. 4) are used when the strong EPSP threshold level is reached. This is like having a threshold on some kind of activation function in the otherwise linear node.

One interpretation is that the activity must up and above the background noise before strong EPSPs materialize, but then activation is fast if an input approximates known patterns of active synapses. This is somewhat similar to a [leaky rectified linear unit](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)#Leaky_ReLUs) (Leaky ReLU), where a base activity must be present before it gives any large changes in output, and a delayed spike could be interpreted as a linearly rising value reflecting the decreased delay. High activity gives short delay before the threshold is reached, a spike is fired, while low activity gives a long delay before the threshold is reached.

The strong EPSP will be triggered if the local area in the neuron, or the whole dendrite as such, is sufficiently depolarized. That mean it is rather non-discriminating to the cause of the depolarization. The depolarization will although diffuse and leak over time, so a local depolarization may go away before a strong EPSP is fired. It is also worth noting that the neuron is compartmentalized, as one apical and several basal dendrites, and it is not clear whether a strong depolarization in one dendrite will trigger strong responses in other dendrites. However, it is unlikely that a round trip down one dendrite and up another will happen without a spike, and if that happen then the depolarization will be reset.

It seems like strong EPSPs would allow synaptic base activity to exist before a spike is fired, and it will prime the neuron for a final pattern. This will create a multimodal response, not a unimodal response as in an artificial neuron. This can be approximated with a two-layer neural net where each node in the first layer represents a specific pattern. As a consequence, a biological neural net could be several order more complex than a simple count of neurons could lead us to believe.

Another consequence is that a biological neuron could repurpose prior knowledge quite effectively, without forgetting what it has already learned. It would also be able to use one pattern for priming and fire according to some other pattern. “It walks like a duck, but it is [Sid](https://www.youtube.com/watch?v=uMuJxd2Gpxo)!”
