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

## <i class="fa fa-calendar"></i> Mar 2017

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
