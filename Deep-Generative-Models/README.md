# Topic 2: Deep Generative Models

![](./topic2.png)

## 0. Table of Contents

- [1. Variational Autoencoders](#1-variational-autoencoders)
- [2. Diffusion Models](#2-diffusion-models)
    - [2.1. Case Study: Imagegen](#21-case-study-imagegen)

- [Reference](#reference)


## 1. Variational Autoencoders

![](./vae-latent-approach.png)
![](./vae-latent-approach-without_y.png)

- __Problem__: Marginal likelihood $p(x)$ is intractable. So can’t do maximum likelihood directly.

![](./vae-vae.png)
![](./vae-hierarchical-vae.png)
![](./vae-challenges.png)

- We say a posterior is collapsing, when signal from input $x$ to posterior parameters is either too weak or too noisy, and as a result, decoder starts ignoring $z$ samples drawn from the posterior $q_\phi(z|x)$.
- In various domains, such as text and images, it has been empirically observed that it is difficult to make use of latent variables when coupled with a strong autoregressive decoder.


## 2. Diffusion Models

![](./dfm-denoising-diffusion-model.png)
![](./dfm-forward-diffusion-process.png)

- Usually $\beta$ is very small, E.g. 0.0001. Forward faster using diffusion kernel as each step uses a very simple Gaussian distribution: Proof using induction.

![](./dfm-diffusion-kernel.png)
![](./dfm-generative-learning-by-denoising.png)
![](./dfm-reverse-denoising-process.png)
![](./dfm-learning-denoising-model.png)
![](./dfm-parameterizing-denoising-model.png)
![](./dfm-training-objective-weighting.png)
![](./dfm-summary.png)
![](./dfm-implementation-architecture.png)
![](./dfm-connection-to-vae.png)
![](./dfm-continuous-time.png)
![](./dfm-forward-diffusion-process-sde.png)
![](./dfm-sde.png)
![](./dfm-forward-diffusion-process-sde2.png)
![](./dfm-generative-reverse-sde.png)

- But how to get the score function?

![](./dfm-score-matching.png)
![](./dfm-denoising-score-matching2.png)
![](./dfm-denoising-score-matching.png)

- Why the distribution is tractable:

![](./dfm-variance-preserving-sde.png)

![](./dfm-denoising-score-matching3.png)
![](./dfm-continuous-elbo.png)
![](./dfm-weighted-diffusion-objective.png)
![](./dfm-denoising-score-matching4.png)
![](./dfm-probability-flow-ode.png)
![](./dfm-synthesis-sde-ode.png)
![](./dfm-sampling-continuous-time1.png)
![](./dfm-sampling-continuous-time2.png)
![](./dfm-sampling-problem.png)
![](./dfm-progressive-distillation.png)
![](./dfm-progressive-distillation-algorithm.png)


### 2.1. Case Study: Imagegen

![](./dfm-imagegen1.png)
![](./dfm-imagegen2.png)
![](./dfm-imagegen3.png)
![](./dfm-imagegen4.png)
![](./dfm-imagegen5.png)

- Large classifier-free guidance weights → better text alignment, worse image fidelity
- Larger Text Encoders → Better Alignment, Better Fidelity



## Reference

- [1] [CS231n: Deep Learning for Computer Vision](http://cs231n.stanford.edu/index.html)