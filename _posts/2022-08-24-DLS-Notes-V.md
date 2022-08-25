---
layout: post
title: (Google ML Bootcamp) Notes on DLS Coursera - V
categories: [coding, ML]
---

# Course V - Sequence Models

# RNNs

* $a^{<l>} = g(w_{ai}*x_i + w_{aa}*a^{<l-1>} + b_a)$
* $y^{<l>} = f(w_{ya}*a^{<l>}+b_y)$
*  $a$ is always related to the previous value before the activation function of the next layer is applied.
* $a^{<t>}$ and $x_i$ can  be joint into a single longer vector, with a matching W matrix.
* The loss function is calculated for the full sequence
