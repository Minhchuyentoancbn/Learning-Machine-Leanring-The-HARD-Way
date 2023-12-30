# Deep Generative Models

![](./image/topic2.png)

## 0. Table of Contents

- [1. Variational Autoencoders](#1-variational-autoencoders)
- [2. Diffusion Models](#2-diffusion-models)
    - [2.1. Case Study: Imagegen](#21-case-study-imagegen)
- [3. Generative Adversarial Networks](#3-generative-adversarial-networks)
    - [3.1. GANs](#31-gans)
    - [3.2. Conditional GANs](#32-conditional-gans)
    - [3.3. Super-Resolution GANs](#33-super-resolution-gans)

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


## 3. Generative Adversarial Networks

### 3.1. GANs

- Problems: the difficulty of approximating many intractable probabilistic computations that arise in maximum likelihood estimation
- A generative model $G$ that captures the data distribution, and a discriminative model $D$ that estimates the probability that a sample came from the training data rather than $G$. The training procedure for $G$ is to maximize the probability of $D$ making a mistake.
- This framework corresponds to a minimax two-player game. There is no need for any Markov chains or unrolled approximate inference networks during either training or generation of samples.
- Define a prior on input noise variables $p(z)$. We alternate between $k$ steps of optimizing $D$ and one step of optimizing $G$. This results in $D$ being maintained near its optimal solution, so long as $G$ changes slowly enough.

![](./image/gan-1.png)
![](./image/gan-2.png)

### 3.2. Conditional GANs

- A general-purpose solution to image-to-image translation problems. These networks not only learn the mapping from input image to output image, but also learn a loss function to train this mapping.
- Effective at synthesizing photos from label maps, reconstructing objects from edge maps, and colorizing images, among other tasks.

__Objective__

- We condition on an input image and generate a corresponding output image. Conditional GANs learn a mapping from observed image $x$ and random noise vector $z$, to $y$. Unlike an unconditional GAN, both the generator and discriminator observe the input edge map.

![](./image/gan-3.png)
![](./image/gan-4.png)

- Past conditional GANs have acknowledged this and provided Gaussian noise $z$ as an input to the generator, in addition to x. => Not effective as  the generator simply learned to ignore the noise. For our final models, we provide noise only in the form of dropout, applied on several layers of our generator at both training and test time.

__Network architectures__

- Structure in the input is roughly aligned with structure in the output, low-level information shared between the input and output
- To give the generator a means to circumvent the bottleneck for information like this, we add skip connections, following the general shape of a `U-Net`. Specifically, we add skip connections between each layer $i$ and layer $n − i$, where $n$ is the total number of layers. Each skip connection simply concatenates all channels at layer $i$ with those at layer $n − i$. 
- $L2$ loss – and $L1$, produces blurry results on image generation problems. Although these losses fail to encourage high- frequency crispness, in many cases they nonetheless accurately capture the low frequencies. For problems where this is the case, we do not need an entirely new framework to enforce correctness at the low frequencies. L1 will already do.
- Restricting the GAN discriminator to only model high-frequency structure => restrict our attention to the structure in local image patches 
=> a discriminator architecture – which we term a PatchGAN – that only penalizes structure at the scale of patches. This discriminator tries to classify if each $N x N$ patch in an image is real or fake. We run this discriminator convolutionally across the image, averaging all responses to provide the ultimate output of $D$. 
- $N$ can be much smaller than the full size of the image and still produce high quality results
- Such a discriminator effectively models the image as a Markov random field, assuming independence between pixels separated by more than a patch diameter.

__Optimization and inference__

- We train to maximize $logD(x, G(x, z))$. In addition, we divide the objective by 2 while optimizing $D$, which slows down the rate at which $D$ learns relative to $G$.
- At inference time, we run the generator net in exactly the same manner as during the training phase. We apply dropout at test time, and we apply batch normalization using the statistics of the test batch


### 3.3. Super-Resolution GANs

- Problem: recover the finer texture details when we super-resolve at large upscaling factors.
- Solution:  a perceptual loss function which consists of an adversarial loss and a content loss. A content loss motivated by perceptual similarity instead of similarity in pixel space.
- Employ a deep residual network with skip-connection and diverge from MSE as the sole optimization target. 
- We define a novel perceptual loss using high-level feature maps of the VGG network combined with a discriminator that encourages solutions perceptually hard to distinguish from the HR reference images.

![](./image/gan-5.png)
![](./image/gan-6.png)

__Adversarial network architecture__

![](./image/gan-7.png)

__Perceptual loss function__

![](./image/gan-8.png)

- For high frequency content:

![](./image/gan-9.png)
![](./image/gan-10.png)


## Reference

- [1] [CS231n: Deep Learning for Computer Vision](http://cs231n.stanford.edu/index.html)
- [2] Goodfellow, I. J., Pouget-Abadie, J., Mirza, M., Xu, B., Warde-Farley, D., Ozair, S., … Bengio, Y. (2014). Generative Adversarial Networks. Retrieved from https://arxiv.org/abs/1406.2661
- [3] Isola, P., Zhu, J.-Y., Zhou, T., & Efros, A. A. (2018). Image-to-Image Translation with Conditional Adversarial Networks. Retrieved from https://arxiv.org/abs/1611.07004
- [4] Ledig, C., Theis, L., Huszar, F., Caballero, J., Cunningham, A., Acosta, A., … Shi, W. (2017). Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network. Retrieved from https://arxiv.org/abs/1609.04802