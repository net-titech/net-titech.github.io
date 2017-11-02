---
layout: post
title: Deep Compression Reading List
excerpt: Deep neural network compression literature research organized chronologically.
categories:
  - Deep Neural Networks
comments: true
pinned: true
published: true
icon: fa-list
---

## Approaches

To compress a neural network, currently there are several approaches:

1. Stochastic Block Models.
2. Tensor Factorization (incl. all decompression techniques).
3. Determinantal Point Processes and Submodularity Models.
4. Network Distillation and Prunning (incl. fine tuning, etc.)
5. Graph Embedding (incl. graph summarization).
6. Small or new architectures.

## <i class="fa fa-calendar"></i> November 2017

**Variational Boosting: Iteratively Refining Posterior Approximation** Andrew C. Miller et al. ICML 2017 - _Hoang_
{: .notice}
> By applying the concept of boosting to variational method of posterior
approximation, the author proposed to iteratively add new terms into the
variational objective. This idea can be understood as using a mixture of
distribution to increase the flexibility of the approximator. As we add more
terms, the appoximation gets more accurate. Note that we can allow the 
appoximator to be artitarily flexible without worring about overfitting 
(Bishop book). The paper also provide discussion on how to perform the
_reparameterization trick_ under the new model. Due to the changes in the
objective fucntions themselves, the authors only provide experimental 
results on some conjugate models and a simple Bayesian Neural Network.
The dataset in use is the baseball dataset and some other high dimensional
distribtion. The future work includes approximation guarantees of VBoost
and applying natural gradient updates to VBoost.

## <i class="fa fa-calendar"></i> September 2017

**Do Deep Convolutional Nets Really Need to be Deep and Convolutional?** Gregor Urban et al. ICLR 2017 - _Kaushalya_
{: .notice}
> This can be considered as a response to the NIPS 2014 paper "Do deep nets really need to be deep?" (Ba and Caruana, 2014). They train shallowe Colnvolutional Neural Networks using network distillation on an ensemble of state-of-the-art CNNs on CIFAR-10 dataset. Their results suggest that to achieve similar accuracy with a shallow student model, it should possess much more parameters than the deep teacher model (can be 30 times larger than the deep teacher model). Still the accuracy may not reach the level of the teacher model.

**Understanding Deep Learning Requires Re-Thinking Generalization** Chiyuan Zhang et al. ICLR 2016 - _Hoang_
{: .notice}
> Experimental results and insight for generalization error in deep neural networks.
The results from this paper suggested that we can train a neural network with
noise (input noise and/or label noise) and still obtain an extremely high accuracy
on the training set. The paper (kind of) criticizes the missuse the term 
"regularization" in the deep neural network literature. Experimental results (in this
paper) showed that although regularization techniques can help with test accuracy,
their contribution are minor when generalization error is taken into account.

**Variational Dropout Sparsify Deep Neural Networks** Dmitry Molchanov et al.  ICML 2017 - _Hoang_
{: .notice}
> Based on the literature of Sparse Bayesian Learning and the recent work on
Variational Dropout (Kingma, 2015), the authors proposed a method to set the dropout
parameter alpha at a high value (~1000) without destablizing the stochastic 
gradient of the variational lower bound term. Previously, in Variational Dropout
paper, Kingma et al. discussed that setting the dropout parapeter alpha at 
a high value poses a difficulty in training due to the multiplicative nature
of noise term with alpha in the gradient leading to unstability in learning. 
Therefore, they only consider alpha less than one (equivalent with binary dropout
probability less than 0.5). Molchanov et al. discarded this multiplicative noise 
term and treat it as an independent variable during training. Their method
preserve the posterior distribution while stablizing the gradient. The reason
why they desire alpha to be large is that weights associated with large alpha
can be set to zero without affecting the performance of the neural network.
Furthermore, alpha now can be a parameter, not a hyperparameter any more.
Their implementation showed that Sparse Variational Dropout leads to high
sparsity with minor decrease in performance (CIFAR-10, CIFAR-100 datasets
under VGG and LeNet architectures).

## <i class="fa fa-calendar"></i> May 2017

**Overcoming challenges in fixed point training of deep convolutional networks.** Lin, Darryl D., and Sachin S. Talathi. (Qualcomm Research) arXiv preprint arXiv:1607.02241 (2016). - _Kaushalya_
{: .notice}
> The stochastic gradient algorithm becomes unstable when the weights and activations are constrained to a limited numerical precision, due to the presence of noisy gradient updates. This paper proposes iterative fine-tuning of bottom-to-top layers as a method to alleviate the instability in SGD training.  

## <i class="fa fa-calendar"></i> Apr 2017

**MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications**. Howard et al. (Google Inc.) Arxiv preprint [27th April 2017] - _Kaushalya_
{: .notice}
> This paper introduces a smaller and faster convolutional neural network achitecture by replacing convolutions by depthwise separable convolutions and a 1x1 pointwise convolution to combine the outputs of depthwise convolutions. Additionally this paper introduces two more parameters, width multiplier and resolution multiplier to reduce the number of hyperparameters further.      

**Deep Model Compression: Distilling Knowledge from Noisy Teachers**. Sau & Balasubramanian. ArXiv. 2016 - _Arie_
{: .notice}
> This paper addressed the storage, train time and runtime complexity. Based on the network distillation idea by Hinton et al (NIPS 2014 Workshop). Two main ideas: First, Training shallow neural networks (called the student nets) to mimic trained deep neural nets (called the teacher nets) using logit regression; Second, the student can learn from multiple teachers using noise-based regularization.


**Do Deep Nets Really Need to be Deep?**. Ba & Caruana. NIPS. 2014 - _Arie_
{: .notice}
> This paper proposed teacher-student strategy: shallow neural networks learn from deeper nets and achieve similar accuracy. The shallower nets mimicking the deeper ones based on the [Model Compression](http://dl.acm.org/citation.cfm?id=1150464). The steps are: Mimic learning via L2 regression on logits, then using a linear bottleneck layer to speed up training. 

## <i class="fa fa-calendar"></i> Mar 2017

**Towards Convolutional Neural Networks Compression via Global Error Reconstruction**. Lin et al., IJCAI. 2016 - _Arie_
{: .notice}
> This paper proposed 2 compression steps: First, utilized SVD-based Low-Rank Approximation to compress the parameters in fully connected layer (layer wise). Then, make a cross-layer compression via back-propagation by minimizing the reconstruction error between the outputs of both the original and the compressed.

**Dynamic Network Surgery for Efficient DNNs**. Guo et al., NIPS. 2016 - _Kaushalya_
{: .notice}
> This paper was [presented](https://papers.nips.cc/paper/6165-dynamic-network-surgery-for-efficient-dnns) as a poster at NIPS 2016. Two operations: pruning and splicing (recovery of pruned connections) are performed in a continuous manner. Connections are pruned based on the magnitude of their weights. Authors claim a 17.7X compression rate for AlexNet.

**Compressing Convolutional Neural Networks in the Frequency Domain**. Chen et al., KDD. 2016 - _Hoang_
{: .notice}
> This paper employs the DCT transformation and hashing trick to compress a convolutional neural network. The content of (Wang, 2016) is quite similar to this paper. Note: KDD'16 is in August, while NIPS'16 is in December.

**CNNpack: Packing Convolutional Neural Networks in the Frequency Domain**. Yunhe Wang et al., NIPS. 2016 - _Hoang_
{: .notice}
> This paper applies the JPEG image compression algorithm to compress the convolutional filters of a deep convolutional neural network. The main difference between this paper and other DNN compression paper is that it uses discrete cosine transformation (DCT) as the pruning procedure (instead of threshold). The author claimed 39x compression rate and 25x speed-up rate while maintaining similar top-1 and top-5 accuracy to the original networks (AlexNet). Also, the author stated that the speed of convolution operation can be improved in the frequency domain. This paper also addressed the problem of memory saving in neural network compression. There is no github repository to be found.

**Learning Structured Sparsity in Deep Neural Networks**. Wen et al., NIPS. 2016 - _Kaushalya_
{: .notice}
> This paper was [presented](http://papers.nips.cc/paper/6504-learning-structured-sparsity-in-deep-neural-networks) a poster at NIPS 2016. This paper introduces group lasso based sparsity regularization to zero out all weights in some structures (filters, channels, and layers) without a significant drop of classification accuracy.

**Deep Learning without Poor Local Minima**. Kenji Kawaguchi. NIPS. 2016 - _Hoang_
{: .notice}
> The author [presented](https://channel9.msdn.com/Events/Neural-Information-Processing-Systems-Conference/Neural-Information-Processing-Systems-Conference-NIPS-2016/Deep-Learning-without-Poor-Local-Minima) his paper at NIPS 2016. This paper provides a better theoretical understanding about a *deep* neural network's loss surface.

**ENet: A Deep Neural Network Architecture for Real-Time Semantic Segmentation**. Paszke et al. ArXiv. 2016 - _Arie_
{: .notice}
> We can include ENet architecture for compression comparision.

**An Analysis of Deep Neural Networks Model for Practical Applications**. Canziani et al. ArXiv. 2017 - _Arie_
{: .notice}

**Soft Weight-Sharing for Neural Network Compression**. Ullrich et al. ICLR. 2017 - _Choong, Kaushalya_
{: .notice}

**Deep Compression: Compressing Deep Neural Networks with Pruning, Trained Quantization and Huffman Coding**. Han et al. ICLR. 2016 - _Choong, Kaushalya_
{: .notice}
> The best paper award in ICLR 2016. The approach of this paper leverages on pruning, quantization and huffman coding. Source code can be found at [https://github.com/songhan/Deep-Compression-AlexNet](https://github.com/songhan/Deep-Compression-AlexNet). Note that the code only provides 'Decompression'.

**Learning both Weights and Connections for Efficient
Neural Networks**. Han et al. NIPS. 2015 - _Choong, Kaushalya_
{: .notice}
> This paper performs pruning when given a threshold (hyperparamter) on deciding weights that are useful or otherwise. The network is then retrained.

**Sparse Convolutional Neural Networks**. Liu et al. CVPR. 2015 - _Hoang_
{: .notice}

## <i class="fa fa-calendar"></i> Feb 2017

**Distilling the knowledge in a neural network**. Hinton et al. arXiv preprint arXiv:1503.02531. 2015 - _Kaushalya_
{: .notice}

**BinaryConnect: Training Deep Neural Networks with binary weights during propagations**. Courbariaux et al. NIPS 2015 - _Arie_
{: .notice}

**Binarized Neural Networks**. Hubara et al. NIPS 2016 - _Arie_
{: .notice}

**Neural Networks with Few Multiplications**. Lin et al. ICLR 2016 - _Arie_
{: .notice}
