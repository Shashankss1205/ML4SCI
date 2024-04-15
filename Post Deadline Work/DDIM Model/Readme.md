## Specific Test IV. Diffusion Models 

| Title                                | Layout        | Project                | Project Size | Year | Organization            |
|--------------------------------------|---------------|------------------------|--------------|------|-------------------------|
| Diffusion Models for Gravitational Lensing Simulation | gsoc_proposal | DEEPLENSE | 175hr | 2023 | Alabama, Brown, BITS Pilani Hyderabad, Paris, RWTH |

## Link to Colab Notebook:
https://colab.research.google.com/drive/18wk4uXAbwsumcfPFzzKyO15pUkkNkKI6?usp=sharing

## Link to Model weights:
https://drive.google.com/file/d/1jj1dtD16EYjuW2r3WlSPl6ocEOLuA6nv/view?usp=sharing

## Approaching the Task: 

1) Having an academic background in Mechanical Engineering and thermodynamics helped me better understand the working of the implicit denosing of the images.
2) My first step was to take a look over all the references provided in the problem statement and gather the relevant data.
3) Secondly, I went onto study and analyse the model architecture from the research paper.
4) Lastly, I started implementing the research paper in my notebook taking reference from the implementations of diffusion models on MNIST & Fashion dataset.

## Introduction to DDIM(Denoising Diffusion Implicit Model):

[Diffusion models](https://arxiv.org/pdf/2006.11239.pdf) are inspired by non-equilibrium thermodynamics, and they learn to generate by denoising. Learning by denoising consists of two processes,
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

The paper describes two algorithms, one for training the model, and the other for sampling from the trained model. Training is performed by optimizing the usual variational bound on negative log-likelihood. The objective function is further simplified, and the network is treated as a noise prediction network. Once optimized, we can sample from the network to generate new images from noise samples. 

## Model Architecture:

I designed a U-Net architecture for denoising, integrating noise variances with sinusoidal embeddings for sensitivity to noise levels. By leveraging Keras Functional API and closures for consistent layer building, the model ensures efficient gradient flow and avoids representation bottlenecks. 

Unlike diffusion models, I opted for noise level functions over diffusion process indices for flexibility in sampling schedules. Though diffusion models embed noise at each convolution block, I simplified by inputting it only at the network start, relying on skip and residual connections for information propagation. 

To maintain simplicity, I omitted attention layers for global coherence and disabled learnable parameters in batch normalization layers. Lastly, initializing the last convolution's kernel to zeros enhances initial training behavior, starting the mean squared error loss at precisely 1.


## Working Methodology:

Implementing a DDIM model is simple. I define a model that takes two inputs: Images and the randomly sampled time steps. At each training step, we perform the following operations to train our model:

1) Sample random noise to be added to the inputs.
2) Apply the forward process to diffuse the inputs with the sampled noise.
3) The model takes these noisy samples as inputs and outputs the noise prediction for each time step implicitally.
4) Given true noise and predicted noise, the loss values are calculated
5) The gradients are calculated and the model weights updated.

## Evaluation Metrics: 

1) By visual inspection, we can qualitatively see the images closesly resemble the original images.
![Generated Images](https://github.com/Shashankss1205/ML4SCI/blob/main/Post%20Deadline%20Work/DDIM%20Model/trained.png)

2) On a quantitative aspect, the KID loss variation with each epoch showcases how it is decreasing with increasing number of epochs.
![MSE losses vs epochs](https://github.com/Shashankss1205/ML4SCI/blob/main/Post%20Deadline%20Work/DDIM%20Model/epochsError.png)

## Possible Improvisations:

There are a few things that I can try to improve the model:

1) Increasing the width of each block. A bigger model can learn to denoise in fewer epochs, though I may have to take care of overfitting.

2) We implemented the model without the attention layer to reduce the complexity and resource consumption. I can also add attention layer based on the model scores.

## References:

1. [DDIM Implementation](https://keras.io/examples/generative/ddim/)
2. [DDIM in-depth modeling](https://github.com/beresandras/clear-diffusion-keras)
3. [What are diffusion models?](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/)
