## Specific Test IV. Diffusion Models 

---
title: Diffusion Models for Gravitational Lensing Simulation
layout: gsoc_proposal
project: DEEPLENSE
project size: 175hr
year: 2023
organization:
  - Alabama
  - Brown
  - BITS Pilani Hyderabad
  - Paris
  - RWTH
---

## Approaching the Task: 

1) My first step was to take a look over all the refernces provided in the problem statement and gather the relevant data.
2) Secondly, I went onto study and analyse the model architecture from the research paper.
3) Lastly, I started implementing the research paper in my notebook taking reference from the implementations of diffusion models on CIFAR10 dataset.

## Introduction to DDPM(Denoising Diffusion Probabilistic Model):

![Diffusion models](https://arxiv.org/pdf/2006.11239.pdf) are inspired by non-equilibrium thermodynamics, and they learn to generate by denoising. Learning by denoising consists of two processes,
each of which is a Markov Chain. These are:

1. The forward process: In the forward process, we slowly add random noise to the data
in a series of time steps `(t1, t2, ..., tn )`. Samples at the current time step are
drawn from a Gaussian distribution where the mean of the distribution is conditioned
on the sample at the previous time step, and the variance of the distribution follows
a fixed schedule. At the end of the forward process, the samples end up with a pure
noise distribution.

2. The reverse process: During the reverse process, we try to undo the added noise at
every time step. We start with the pure noise distribution (the last step of the
forward process) and try to denoise the samples in the backward direction
`(tn, tn-1, ..., t1)`.

The paper describes two algorithms, one for training the model, and the other for sampling from the trained model. Training is performed by optimizing the usual variational bound on negative log-likelihood. The objective function is further simplified, and the network is treated as a noise prediction network. Once optimized, we can sample from the network to generate new images from noise samples. Here is an overview of both algorithms as presented in the paper:
![Algorithms Used](https://github.com/Shashankss1205/ML4SCI/blob/main/Specific%20Test%204/Images%20Folder/Algorithms.png)

## Model Architecture:

U-Net, originally developed for semantic segmentation, is an architecture that is widely used for implementing diffusion models but with some slight modifications:

1) The network accepts two inputs: Image and time step
2) Self-attention between the convolution blocks once we reach a specific resolution (16x16 in the paper)
3) Group Normalization instead of weight normalization

## Working Methodology:

Implementing a DDPM model is simple. We define a model that takes two inputs: Images and the randomly sampled time steps. At each training step, we perform the following operations to train our model:

1) Sample random noise to be added to the inputs.
2) Apply the forward process to diffuse the inputs with the sampled noise.
3) Your model takes these noisy samples as inputs and outputs the noise prediction for each time step.
4) Given true noise and predicted noise, we calculate the loss values
5) We then calculate the gradients and update the model weights.

## Evaluation Metrics: 

1) By visual inspection, we can qualitatively see the images closesly resemble the original images.
![Original Images](https://github.com/Shashankss1205/ML4SCI/blob/main/Specific%20Test%204/Images%20Folder/GeneratedImages.png)
![Generated Images](https://github.com/Shashankss1205/ML4SCI/blob/main/Specific%20Test%204/Images%20Folder/GeneratedImages.png)

2) On a quantitative aspect, the loss vs epoch graph plot showcases how the MSE(Mean Squared Error) is decreasing with increasing number of epochs.
![MSE losses vs epochs](https://github.com/Shashankss1205/ML4SCI/blob/main/Specific%20Test%204/Images%20Folder/TrainingLoss.png)

## Possible Improvisations:

There are a few things that I can try to improve the model:

1) Increasing the width of each block. A bigger model can learn to denoise in fewer epochs, though you may have to take care of overfitting.

2) We implemented the linear schedule for variance scheduling. You can implement other schemes like cosine scheduling and compare the performance.

## References:

1. [Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2006.11239)
2. [Author's implementation](https://github.com/hojonathanho/diffusion)
3. [A deep dive into DDPMs](https://magic-with-latents.github.io/latent/posts/ddpms/part3/)

