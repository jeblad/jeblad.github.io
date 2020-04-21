---
layout: post
language: en
created: 2019-03-03 22:00:00 (CET)
modified:
  - 2019-03-21 22:00:00 (CET)
  - 2019-03-23 22:00:00 (CET)
  - 2019-10-29 22:00:00 (CET)
title: Rate encoded location
tagline: place encode like a brain
description: Outline of rate encoded locations, how the brain might do it, and a possible approximation for an artificial neural net.
authors:
  - jeblad
categories:
  - neural nets
tags:
  - place encode
  - rate encode
parent: "neural_net"
# sources: [ ["This link is just an example", "https://github.com/jeblad/brain/some-place/some-place-deep.pdf"], ["This link is just an example", "https://github.com/jeblad/brain/some-place/some-other-place/"] ]
paper_url: https://github.com/jeblad/brain/some-place/some-place-deep.pdf
paper_title: Title of the article
repo_url: https://github.com/jeblad/brain/some-place
repo_title: Deep into the repository
licenses:
  - cc-by-nc-nd-4.0
---

It is known from [grid cells](https://en.wikipedia.org/wiki/grid_cells) that the place can be encoded as an $N$-tuple of neuronal activities, where the activity of each neuron approximate a cosine function. The set of neurons encode the location over several orders, and forms a reference grid for recall of the location. We can hypothesize that something similar happen in other neural networks, but we don't really know for sure.

<!--more-->

{% include reworked.html %}

In [cerebral cortex](https://en.wikipedia.org/wiki/cerebral_cortex) there are structures called [cortical columns](https://en.wikipedia.org/wiki/cortical_column) consisting of smaller [cortical minicolumns](https://en.wikipedia.org/wiki/cortical_minicolumn). These are sometimes called cortical macro and micro columns. The consensus is that a cortical column is a set of features that somehow are grouped together, and that a cortical minicolumn form a specific kind of feature extractor. One interpretation is that as a minicolumn gets activated, and as long as the extracted feature stays inside the [receptive field](https://en.wikipedia.org/wiki/receptive field) of a minicolumn it stays active. It will although try to rate encode the location inside that receptive field, going from low to high over some interval.

If we assume there is a kind of reference grid overlaid the receptive field, then the actual input can be added to the set of neuronal activities in this reference grid. If the neurons in the reference grid has [burst firing](https://en.wikipedia.org/wiki/burst_firing) as modus operandi, and the neuron is viewed as a leaky bag, then the input together with the bursts will give rise to a [pulse position modulated](https://en.wikipedia.org/wiki/Pulse-position_modulation) spike train. This happen if the input value (represented by the spikes) arrive rather sparingly compared to the grid values (represented by the bursts) and the neuron has time to integrate over a whole burst. The silent time must also be long enough for the rest charge to leak out of the neuron. The input signal can then be viewed as a set value, where the neuron slowly integrates the grid values, ramping them up until they reach threshold value, and then a spike is fired. The outgoing spike could then be interpreted as a pulse position encoded location.

Let the signal inputs be $x_j(t)$ with weights $v_j$, and positional inputs be $p_i(t)$ with weights $w_i$, then the output $y_j$ will be

$$
\begin{equation}
y_j = \operatorname{q} \left ( t, v_j \int_{t+\Delta t_1}^{t+\Delta t_2} x_j(t)\, dt + \sum_i \left ( w_i \int_{t+\Delta t_1}^{t+\Delta t_2} p_i(t)\, dt \right ) \right )
\end{equation}
$$

$$
\begin{equation}
t \gets
\begin{cases}
t+\Delta t & \text{if} \, y_j \lt k \\
0 & \text{otherwise} \\
\end{cases}
\end{equation}
$$

where $\operatorname{q}$ is some spiking transfer function, that somehow resets the variable $t$ when the transfer function has spiked and thus restarts integration over a new interval $t_2 - t_1$. It should have a rest time $t_1$ after spiking before it starts integrating again. This can also be modeled as a set of differential equations, but it gives a computationally somewhat harder implementation.

The spike will trigger sooner when the input signal is high and later when the input signal is low. Likewise, it will trigger sooner when the grid signal is high and later when the grid signal is low. At the same time the spike can be assumed to reset the cycle, and even if there are no input signal the grid will still generate a background spike chatter. Still note that this is not a strictly [deterministic algorithm](https://en.wikipedia.org/wiki/Deterministic_algorithm) with a linear representation, as it is a good bit of randomness in the spiking behavior.

By inspecting the equation it is obvious that if the inputs are continuous, or close to continuous, and there are no kind of external reference, then the observed pulse position modulation turns into a plain [rate encoding](https://en.wikipedia.org/wiki/Rate_coding) with some random behavior. This rate encoded spiking is typically what would be observed downstream along the axon.

$$
\begin{equation}
y_j = \operatorname{q} \left ( t, v_j \int_{t+\Delta t_1}^{t+\Delta t_2} x_j(t)\, dt + \sum_i \left ( w_i \int_{t+\Delta t_1}^{t+\Delta t_2} p_i(t)\, dt \right ) \right )
\end{equation}
$$

$$
\begin{equation}
t = t
\end{equation}
$$

If a minicolumn consists of about 100 neurons, and they are divided over about six layers, then there are about 16-17 neurons in each layer. That gives approximate four times four neurons in the input layer, forming 16 patches, or about four neurons to form a two times two grid with sufficient resolution. If the encoding isn't completely binary, then the number of encoding neurons in the grid could be slightly more or less. A base of 1.6 gives about three to form the same grid. The number of neurons that has this role would be rather few and interspersed with other neurons.

It is also plausible that the receptive field could be somewhat larger than the minicolumn itself, which has a rather sharp border to neighboring minicolumns. That is even more plausible if the column does [principal component analysis](https://en.wikipedia.org/wiki/principal_component_analysis) or [independent component analysis](https://en.wikipedia.org/wiki/principal_component_analysis).
