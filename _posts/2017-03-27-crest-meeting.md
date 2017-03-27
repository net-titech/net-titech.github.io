---
layout: post
title: CREST-Deep Weekly Meeting
excerpt: "2017-03-27"
categories: [Meeting]
comments: true
pinned: false
icon: fa-clock-o
---

# 2017-03-27 / CREST-Deep Weekly Meeting

## <i class="fa fa-file-text"></i> Literature Update

In this week, we have studied several papers regarding techniques and new architectures
for compact deep neural network (especially deep convolutional neural networks).
The list of papers are provided [here](https://net-titech.github.io/articles/2017-02/deep-compression).
We have several observations as follow:

- In the area of deep neural network _compression_, the standard procedure is: _pruning_, _quantization_, then _Huffman coding_. Although the aforementioned procedure yields good compression rate for **storing** a deep convolutional neural network (1/40 to 1/60), we still need to **decompress** a compressed model to its original size in order to run it. None of the proposed models actually run on compressed network. We believe there must be a way to run a compressed network without decompressing it.
- There are some interesting neural network models applying binary weights, block dropout, and discrete cosine transformation to improve theirs speed (training/running) and compressing the model storage space.
- Regarding the benchmark criteria for a deep neural network compression model, not many research actually measure the memory requirement of a DNN model in deployment. We think the exact energy consumption and memory usage of _each layer_ is a very important information to measure the performance of a DNN model.
- The approach from (Ullrich, 2017) read by Choong is similar to the Stochastic Block Model approach. We can generalize such approach.
- Investigate the Determinantal Point Processes on graphs gives some interesting suggestions for graph sampling and neural network summarization.
- SquezeNet is one of the most effective compact deep neural network. It performs particularly well in domain-specific applications. A similar (smaller or higher accuracy) architecture to SquezeNet can be developed.
- Viewing a neural network as a acyclic (multi-partite) network, we can think of each output element (in an output vector) is the result of computation along many _paths_. This view yields some insight about a deep neural network (Kawaguchi, 2016), and also inspired for some other representation of a deep neural network using only one distribution and one matrix.

## <i class="fa fa-flask"></i> Research Update

We have run several DNN compression benchmark provided by (Han, 2016) and (Ullrich, 2017) to recreate their results. As mentioned in the previous session, these models compress the network in term of storage space, not running memory space. On the other hand, we have set up Caffe environment on the new machine (titan-x) and downloaded the full size ImageNet.

## <i class="fa fa-bullseye"></i> Next Week Objectives

We have one presentation on April 4th in the meeting with other labs. The content of this presentation is as follow:

- Present the current situation of deep model compression. (state of the art algorithms and their limitations)
- Present our complex network approaches (Filter compression, DPP, SBM, Submodularity, Network summarization).
- Discuss about the domain-specific constrain.

On the other hand, we will keep exploring and comparing other algorithms and start the benchmark implementation.
