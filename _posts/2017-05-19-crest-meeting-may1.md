---
layout: post
title: CREST-Deep Weekly Meeting
excerpt: "2017-05-19"
categories: [Meeting]
comments: true
pinned: false
icon: fa-clock-o
---

# 2017-05-19 / CREST-Deep Weekly Meeting

## <i class="fa fa-file-text"></i> Literature Update

Since the last (recorded) meeting (April 7th), we have focused on designing a
novel neural network compression scheme, which can be deployed without
specialize hardware and propriety methods. For this reason, we only have a few
update on the literature:

- The effect of parameter robustness and parameter quantization effect is
interesting to investigate. Recently, there are few papers study this problem.
If we can quantify the parameter robustness of a deep neural network, we can
develop a much more effective lossy compressing algorithm.
- Deep neural network distillation is a good idea. However, we wonder if it is
any better than just train a smaller model.
- Song's pruned model can be retrained without the pruning constrain to achieve
better result (AlexNet on ImageNet - ICLR 2017).

## <i class="fa fa-flask"></i> Research Update

We have two main research direction so far:

- Deployment of compressed model on mobile device. We have been able to compress
AlexNet down to 8MB from 240MB (~30 times). The main strong point of our
compression scheme is that we do not need to have a specialized hardware to read
a model in its compressed format. Moreover, our compression scheme enables GPU
to decode the weight matrix on the fly, meaning we do not need to decompress the
model on CPU (less sequential code). On this direction, we are exploring the
lossy compression scheme (potentially achieving 3.5MB compressed size). We are
also working on low rank decomposition and some other engineering methods for
speeding up the computation.

- Besides our engineering effort above, we are working on some other approach
such as network distillation. However, we are having trouble recreating results
from some papers addressing this method. Further investigation will be presented
in later posts.

- (Side note) Since most of the papers addressing neural network
pruning-retraining scheme doesn't provide the pruning threshold. We have created
our own pruning-retraining procedure on our
[Caffe fork](https://github.com/net-titech).

## <i class="fa fa-bullseye"></i> Next Week Objectives

We have set up an independent meeting with Yokota-lab to discuss the possibility
of encoding the low-rank approximation matrices. Since low-rank approximation is
a well-established method, we hope to further increase computational speed while
reducing the storage size of a deep neural network.

Main task list for the next week:

- Write proposals (check [Trello](https://trello.com/deepcrestmuratateam)).
- Paper reading (check [Trello](https://trello.com/deepcrestmuratateam)).
- Unit test for the new pruning module in Caffe (check github).
- Unit test for encoding scheme, fix the prefix sum to adapt with large relative
index.
- Explore smaller models resulting from novel training methods.
- Find out the performance impact of low-rank approximation and the possibility
of compressing low-rank matrices (investigate on both `conv` and `fc` layers).
