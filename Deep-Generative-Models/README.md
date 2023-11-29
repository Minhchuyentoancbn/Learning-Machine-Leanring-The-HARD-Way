# Topic 2: Deep Generative Models

![](./image/topic2.png)

## 0. Table of Contents

- [1. Variational Autoencoders](#1-variational-autoencoders)
- [2. Diffusion Models](#2-diffusion-models)
    - [2.1. Case Study: Imagegen](#21-case-study-imagegen)

- [Reference](#reference)


## 1. Variational Autoencoders

![](./image/vae-latent-approach.png)
![](./image/vae-latent-approach-without_y.png)

- __Problem__: Marginal likelihood $p(x)$ is intractable. So can’t do maximum likelihood directly.

![](./image/vae-vae.png)
![](./image/vae-hierarchical-vae.png)
![](./image/vae-challenges.png)

- We say a posterior is collapsing, when signal from input $x$ to posterior parameters is either too weak or too noisy, and as a result, decoder starts ignoring $z$ samples drawn from the posterior $q_\phi(z|x)$.
- In various domains, such as text and images, it has been empirically observed that it is difficult to make use of latent variables when coupled with a strong autoregressive decoder.


## 2. Diffusion Models

![](./image/dfm-denoising-diffusion-model.png)
![](./image/dfm-forward-diffusion-process.png)

- Usually $\beta$ is very small, E.g. 0.0001. Forward faster using diffusion kernel as each step uses a very simple Gaussian distribution: Proof using induction.

![](./image/dfm-diffusion-kernel.png)
![](./image/dfm-generative-learning-by-denoising.png)
![](./image/dfm-reverse-denoising-process.png)
![](./image/dfm-learning-denoising-model.png)
![](./image/dfm-parameterizing-denoising-model.png)
![](./image/dfm-training-objective-weighting.png)
![](./image/dfm-summary.png)
![](./image/dfm-implementation-architecture.png)
![](./image/dfm-connection-to-vae.png)
![](./image/dfm-continuous-time.png)
![](./image/dfm-forward-diffusion-process-sde.png)
![](./image/dfm-sde.png)
![](./image/dfm-forward-diffusion-process-sde2.png)
![](./image/dfm-generative-reverse-sde.png)

- But how to get the score function?

![](./image/dfm-score-matching.png)
![](./image/dfm-denoising-score-matching2.png)
![](./image/dfm-denoising-score-matching.png)

- Why the distribution is tractable:

![](./image/dfm-variance-preserving-sde.png)

![](./image/dfm-denoising-score-matching3.png)
![](./image/dfm-continuous-elbo.png)
![](./image/dfm-weighted-diffusion-objective.png)
![](./image/dfm-denoising-score-matching4.png)
![](./image/dfm-probability-flow-ode.png)
![](./image/dfm-synthesis-sde-ode.png)
![](./image/dfm-sampling-continuous-time1.png)
![](./image/dfm-sampling-continuous-time2.png)
![](./image/dfm-sampling-problem.png)
![](./image/dfm-progressive-distillation.png)
![](./image/dfm-progressive-distillation-algorithm.png)


### 2.1. Case Study: Imagegen

![](./image/dfm-imagegen1.png)
![](./image/dfm-imagegen2.png)
![](./image/dfm-imagegen3.png)
![](./image/dfm-imagegen4.png)
![](./image/dfm-imagegen5.png)

- Large classifier-free guidance weights → better text alignment, worse image fidelity
- Larger Text Encoders → Better Alignment, Better Fidelity



## Reference

- [1] [CS231n: Deep Learning for Computer Vision](http://cs231n.stanford.edu/index.html)