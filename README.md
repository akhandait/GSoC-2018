<p align="center">
  <img width="556" height="112" src="https://github.com/akhandait/GSoC-2018/blob/master/src/logo.png">
</p>

#### Organisation: [mlpack](https://github.com/mlpack) 

#### Project: Variational Autoencoders

#### Mentor: [Sumedh Ghaisas](https://github.com/sumedhghaisas)

**mlpack** is a C++ machine learning library with emphasis on scalability, speed, and ease-of-use. Its aim is to make machine learning possible for novice users by means of a simple, consistent API, while simultaneously exploiting C++ language features to provide maximum performance and maximum flexibility for expert users. This is done by providing a set of *command-line executables* which can be used as black boxes, and a *modular C++ API* for expert users and researchers to easily make changes to the internals of the algorithms. In addition to its powerful C++ interface, **mlpack** also provides *Python bindings*.

### Objectives:

The objective of this project was to add *complete support* for **Variational Autoencoders(VAEs)** and all its derivatives to the library, construct *models* and *reproduce results* given in particular *research papers*.

During the proposal period, I had planned to implement an independent class for VAEs. However, Sumedh suggested that to make it truly generic and to allow all sorts of hierarchical models, it will be better if we implemented the extra components needed and allow them to integrate seamlessly with the rest of the codebase. We went ahead with that plan and now **mlpack** can be used to implement almost all VAE architectures.

Support for **conditional VAEs** needs a new layer for which I have opened a PR. I had also planned to test some **recurrent** VAE models which I will continue to do after GSoC.

### Overview:

The project can now be broken down into **3 major tasks:**

1. Implemented a **Reparametrization**(Sampling) layer which includes **Kullback Leibler** loss. A **visitor** was added to collect extra losses(in this case KL) from all the layers. It supports **beta**-VAEs.
2. Implemented a **ReconstructionLoss** class. Along with it, two model distributions were implemented. **Bernoulli** distribution has been merged. **Normal** distribution, though tested rigorously, couldn't model the  **MNIST** dataset well, so the PR has been kept on hold.
3. Implemented *multilayer perceptron* and *convolutional* VAE models(in the [mlpack/models](https://github.com/mlpack/models) repository) and trained them on **MNIST** and **Binary MNIST**. Wrote some generation scripts and experimented with the learned distribution. Tested beta-VAEs. While training it on a much bigger **CelebA** dataset, ran into performance issues. Opened a PR improving the **TransposedConvolution** layer. For conditional VAEs, implemented a new **Concatenate** layer.

[Weekly updates](http://www.mlpack.org/gsocblog/AtharvaKhandaitPage.html) I made on **mlpack's** blog.

### Code:

_The pull requests opened in the GSoC period that have been **merged** :_

[Extend support of Softplus function to matrices, cubes](https://github.com/mlpack/mlpack/pull/1414)

[Add a Sampling layer, implement KL divergence in it](https://github.com/mlpack/mlpack/pull/1420)

[Remove redundant data members, move NegativeLogLikelihood to loss folder](https://github.com/mlpack/mlpack/pull/1434)

[Add ReconstructionLoss](https://github.com/mlpack/mlpack/pull/1441)

[Make changes suggested in sampling PR](https://github.com/mlpack/mlpack/pull/1452)

[Overload Forward() function](https://github.com/mlpack/mlpack/pull/1468)

[Add Bernoulli distribution and support for beta-VAEs](https://github.com/mlpack/mlpack/pull/1479)

[**Commits**](https://github.com/mlpack/mlpack/commits?author=akhandait)(Includes commits to the library before GSoC started)

_The pull requests opened in the GSoC period that are currently **being reviewed**:_

[Add NormalDistribution class](https://github.com/mlpack/mlpack/pull/1439)

[[WIP] Add Variational Autoencoder model for MNIST](https://github.com/mlpack/models/pull/14) (in the mlpack/models repository)

[Improve TransposedConvolution layer](https://github.com/mlpack/mlpack/pull/1493)

[[WIP] Add Concatenate layer.](https://github.com/mlpack/mlpack/pull/1495)

### Results:

Here are some results that have been generated after training on the **MNIST** dataset:

<p align="center">
<img width="500" height="300" src="https://github.com/akhandait/GSoC-2018/blob/master/src/allLatent.png">
</p>

The above samples are the result of modifying each of the 10 latent variables independently.

<p align="center">
<img width="500" height="500" src="https://github.com/akhandait/GSoC-2018/blob/master/src/2dLatent.png">
</p>

The above samples are the result of varying 2 latent variables in 2D. 

Sampling from the model trained on **Binary MNIST**:

<p align="center">
<img width="550" height="30" src="https://github.com/akhandait/GSoC-2018/blob/master/src/priorBinary.png">
</p>

The above samples are from the **prior**.

<p align="center">
<img width="550" height="30" src="https://github.com/akhandait/GSoC-2018/blob/master/src/posteriorBinary.png">
</p>

The above samples are from the **posterior**.

### Conclusion:

I can't believe how much I learned in the last 3 months. It has been an awesome experience working on this project. There isn't a better way to learn machine learning algorithms than to implement them from the ground up. Huge thanks to Sumedh for the help and guidance, I got to learn a lot from him. He always gave enough time to clear my doubts and helped me when I was stuck. Also, he gave a better direction to the project than what I was planning to go for. I also thank Marcus([github](https://github.com/zoq)) and Ryan([github](https://github.com/rcurtin)) for all the prompt help and always clearing whatever doubts I had. This project would have been a lot tougher and longer without you all to guide me. 

I strongly intend to continue contributing to **mlpack** in all the ways I can, because it's just too much fun. 

Also, thanks to **Google** for this amazing opportunity and the generous funding.