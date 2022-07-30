---
layout: post
title: (Google ML Bootcamp) Notes on DLS Coursera - II
categories: [coding, ML]
---


## Course 2: Improving DNNs: Hyperparameter Tuning, Regularization and Optimization

I am ashamed of these notes, you can use them but sadly they are useful for me only.

### Week 1
* High bias - Underfitting
* High variance - Overfitting
* L1 makes w sparse
* Frobenius Norm, L2 for matrixes, there are different norms for matrixes
* Did you have a proper intuition of what Regularization was?
* Run the network before you add dropouts, as the j vs epochs is not a accurate representation of the training
* Xavier Init : $scaler = \sqrt{\frac{1}{n^{[l-1]}}}$. 
* He Init: $scaler = \sqrt{\frac{2}{n^{[l-1]}}}$

* Which one is $\sqrt{\frac{2}{n^{[l-1]} + n^{[l]}}} $ ?
* weights init is not a good Hyperparameter to start playing with. Fix random  init first, check that everything works then.

### Week 2 - Optimization
 * Bias correction in Exponentially Weighted Averages:
 $v_t = \frac{v_{t-1}*\beta + \theta_t * (1-\beta)}{1-\beta^t}$

 * Bias correction for Gradient Descent with momentum is not necessary. The usual value of $\beta=0.9$ gives a good estimation for the first 10 iterations.

     $v_{t,dw} = v_{t-1, dw}*\beta + dw_t * (1-\beta)$ 

     $w:=  w - \alpha v_{t,dw}$   

* RMSprop:

     $s_{t,dw} = s_{t-1, dw}*\beta + dw_t^2 * (1-\beta)$ - mean of the squares

     $w:=  w - \alpha \frac{dw}{\sqrt{s_{t,dw}}}$   - if the variations where huge, $s_t$ makes the update more stable.

* Adam = RMSprop + momentum

    $v_{t,dw} = v_{t-1, dw}*\beta_1 + dw_t * (1-\beta_1)$ - $\beta_1=0.9$

    $s_{t,dw} = s_{t-1, dw}*\beta_2 + dw_t^2 * (1-\beta_2)$ - mean of the squares - $\beta_2=0.999$

    $v_{t,dw}  :=  \frac{v_{t,dw} }{1-\beta_1^t}$ - first moment

    $s_{t,dw}  :=  \frac{s_{t,dw} }{1-\beta_2^t}$ - second moment
    

    $w:=  w - \alpha \frac{v_{t,dw}}{\sqrt{s_{t,dw}}+\epsilon}$ - $\epsilon = 10^{-8}$


### Week 3 - Tuning

* Order of importance: 
    
    * learning rate
    * betas, hidden units, batch size 
    * learning rate decay

* Use random values for the hyperparameters
* Coarse the zon of good hyperparameters


* Search for  hyperparameters in scale (log for example for the learning rate, or the beta)

* Batch Normalization is applied before the activation function:

    * Normalization if $Z^{[l]}$
    * $\mu = mean(z)$
    * $\sigma = std(z,\mu)$
    * $z_{norm} = \frac{z - \mu}{\sqrt{\sigma +\epsilon}}$
    * $\tilde{z} = \gamma z_{norm} + \beta $
    * Now we use $\tilde{z}$ instead of z.
    * Using BN you don't need the bias, easier to set it to zero.
    * the backprop is similar to having an extra linear activation layer, $d\gamma \sim dW^{[l]}$ and $db^{[l]} \sim d\beta$
    * it decouples the changes between weights of different layers.
    * it has a slight regularization effect
    * At test time, $\mu$ and $\sigma$ are obtained from the training data, as an average or a moving average.

* Why softmax is maximum likehood estimation?

    Similar to Sigmoid, you can provide the following ansatz: $L = \Pi p_i^{y_i}$ where $p_i$ is the probability of being the correct classification $G$ and  $y_i$ is 0 except where $i=G$.

    $J  =  -log(L) = - \sum y_i \log{p_i} $ for maximization.

    What about $p_i$? That's the softmax function, actually is a approximation of argmax! The soft function is differentiable.


### Nice insight 

- Underfitting: when "avoidable bias" is big
- Overfitting: when "variance" is big