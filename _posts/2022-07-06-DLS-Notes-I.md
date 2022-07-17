---
layout: post
title: (Google ML Bootcamp) Notes on DLS Coursera - I
categories: [coding, ML]
---


## Course 1: NNs and DL

### Week 1: Introduction to DL.
Geoffrey Hinton proved in the 90s that ReLU is a good approximation for a logistic regression. That's  why ReLU works fine in DNNs.

### Week 2: NNs Basics

* Non-convex loss function minimum when using MSE for logistic
* Python Broadcasting is more powerful than expected haha. 
* Cost/Lost function: On the batch / on a single sample
* Using random init weights is not the meta, it was never the meta.
* Vectorizing even at batch updates? Yeah
* reshape is a constant time operation
* Don't use rank 1 vector in python, i.e (n,), instead use (n,1) or (1,n)
* Use `assert()` wisely to debug
* The use of MLE begins even more into the baby examples! The logistic regression is just a form of MLE using one layer only.
* (size_input, batch_size)

*  Nomenclature:



###  Week 3: Shallow NNs

* (hidden_units, batch_size)
* Avoid sigmoid for hidden layers, except for output for 0-1 output
* - At the beginning there was structured data - Genesis Book

* $n^{[L]}$: neurons in L-layer
* $W^{[L]}$ = $[n^{[L]}, n^{[L-1]}]$ = [next_layer, prev_layer]

* $Z^{[L]} = W^{[L]} A^{[L-1]} + b^{[L]} $
* $A^{[L]} = g^{[L]}(Z^{[L]})$
* $A^{[L]}$ =  $[n^{[L-1]}, batch\_size]$ = [data_len, batch_size], stacked columns of data.

### Week 4: Deep L-Layer Neural Network

* Early layers recognize simple information, the easiest ones to learn. The information extracted from the input is more complex the deeper you go from the first layer into later layers.

* zeros needs shape

* Once you get the dims is easy, this is for 1-Layer
* $ Z <-> A$ is a biyective relation,  

    * $dZ^{[l]} = \frac{\partial{J}}{\partial{Z^{[l]}}} = \frac{\partial{J}}{\partial{A^{[l]}}} * \frac{\partial{A^{[l]}}} {\partial{Z^{[l]}}} $

    * $dZ^{[l]} = dA^{[l]} * g'^{[l]}(Z^{[l]})$
* We can continue with dA or dZ
    * $dA^{[l-1]}_{i,j} = \frac{\partial{J}}{\partial{A^{[l-1]}_{i,j}}} = \frac{\partial{J}}{\partial{Z^{[l]}}_{k,m}}  \frac{\partial{Z^{[l]}}_{k,m}} {\partial{A^{[l-1]}}_{i,j}} $
    * $dA^{[l-1]}_{i,j} = dZ^{[l]}_{k,m} \frac{\partial{Z_{k,m}}}{\partial{A^{[l-1]}_{i,j}}}$

        * $Z_{k,m}^{[l]} = W^{[l]}_{k,l}A_{l,m}^{[l-1]} + \dots$

        * $ \frac{\partial{Z_{k,m}}}{\partial{A^{[l-1]}_{i,j}}} = W^{[l]}_{k,l}\delta_{l,i}\delta_{m,j}$

        * $ \frac{\partial{Z_{k,m}}}{\partial{A^{[l-1]}_{i,j}}} = W^{[l]}_{k,i}\delta_{m,j}$

        * $dA^{[l-1]}_{i,j} = dZ^{[l]}_{k,m} W^{[l]}_{k,i}\delta_{m,j} = dZ^{[l]}_{k,j}W^{[l]}_{k,i}$  

        *  $dA^{[l-1]}_{i,j} = W^{[l]T}_{i,k} dZ^{[l]}_{k,j}$

    Finally: $dA^{[l-1]}_{} = W^{[l]T}_{} dZ^{[l]}_{}$
        
    * $dW^{[l]}_{i,j} = \frac{\partial{J}}{\partial{W^{[l]}}_{i,j}} = \frac{\partial{J}}{\partial{Z^{[l]}}_{k,m}} \frac{\partial{Z^{[l]}}_{k,m}}{\partial{W^{[l]}}_{i,j}} $
        
        * $dW^{[l]}_{i,j} = dZ^{[l]}_{k,m} \frac{\partial{Z^{[l]}}_{k,m}}{\partial{W^{[l]}}_{i,j}} $

        As we have seen before, the matrix in the denominator creates as transpose.

        * $Z_{k,m}^{[l]} = W^{[l]}_{k,l}A_{l,m}^{[l-1]} + \dots$

        * $dW^{[l]}_{i,j} = dZ^{[l]}_{k,m} A^{[l-1]}_{l,m} \delta_{k,i} \delta_{l,j} = dZ^{[l]}_{i,m} A^{[l-1]}_{j,m}  $

        * $dW^{[l]}_{i,j} = dZ^{[l]}_{i,m} A^{[l-1]T}_{m,j} $

    Finally, $dW^{[l]}_{} = dZ^{[l]}_{} A^{[l-1]T}_{}$

* This is all for stochastic gradient descent.       

### Wrapping up:

At the output layer:

* $dA^{[L]} \sim d\hat{Y}=  \frac{\partial{J}}{\partial{\hat{Y}^{}}}$ - Gradient given the output and its target, or whatever the cost function uses to optimize. There is a mean respect the mini-batch samples (m).

* $ dZ^{[L]} = d\hat{Y} * g'^{[L]}(Z^{[L]})$

* $dW^{[L]} = dZ^{[L]}_{} \hat{Y}^{T}/m$, every sample provides a weights update and we take the mean. I still don't understand where this value comes from mathematically. It must be from $\frac{\partial J}{\partial W}$ extracting $1/m$ from the mean.

At the $l$ layer:

 * $dA^{[l-1]} = W^{[l]T}_{} dZ^{[l]}_{}$ .

* $ dZ^{[l]} = dA^{[l]} * g'^{[l]}(Z^{[L]})$

* $dW^{[l]} = dZ^{[l]}_{} A^{[l-1]T}/m$, remember that in this layer we use $A^{[l-1]}$ as input and $A^{[l]}$ as output.



It's all about the Optimization method, that's where the M comes from.