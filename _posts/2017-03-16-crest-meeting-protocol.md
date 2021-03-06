---
layout: post
title: CREST-Deep Team Meeting Protocol
excerpt: "Guidlines for CREST-Deep Meetings"
categories: [Meeting]
comments: true
pinned: true
icon: fa-gavel
---

## <i class="fa fa-group"></i> CREST-Deep Meetings

- [2017-05-26](https://net-titech.github.io/articles/2017-05/lowrank-approx-meeting):
Meeting with Yokota lab on the topic of low-rank approximation.
- [2017-05-19](https://net-titech.github.io/articles/2017-05/crest-meeting-may1):
Discuss plan for May and June research. Develop Mobile-Net framework.
- [2017-04-07](https://net-titech.github.io/articles/2017-04/crest-meeting-apr1): Discuss plan for April research.
- 2017-03-30: Short meeting on the organization of April 4th presentation.
- [2017-03-27](https://net-titech.github.io/articles/2017-03/crest-meeting): Deep compression approaches discussion (toward April 4th presentation).
- [2017-03-16](https://net-titech.github.io/articles/2017-03/crest-meeting-protocol): Planning and decide meeting protocol.

## <i class="fa fa-wpforms"></i> Meeting format

We have decided to have a group meeting **once per week** to discuss about
new findings and research progress (flexible date). The content of each meeting
will be recorded as a blog post (like this one). Generally, a meeting has
**three sessions**:

1. *Literature update*. Each member has 5 to 10 minutes to talk about papers
they read within the week. We focus on the main idea only. The list of papers
is listed [here](https://net-titech.github.io/articles/2017-02/deep-compression).
Members are also encouraged to write a short blog post for the paper that
they find interesting.
2. *Reseach update*. We present our difficulty and problems in our research
such as implementation difficulty, new idea, etc.
3. *Discussion*. We spend the last 40 minutes for solution discussion.

Generally, a meeting lasts from 1.5 to 2 hours. It is better for each member
to have a laptop ready in the meeting.

## <i class="fa fa-bullseye"></i> Project objective

Our target for December 2017 is to develop our graph-theoric deep network
compression technique to achieve Compression Ratio of *100*. In this period,
we focus on compressing the Convolutional Neural Network architecture.
Our top-down milestone:

- Dec-Nov 2017: Complete all experiments and comparisions. Finalize paper
drafts and research proposals.
- Sep-Oct 2017: We have our COMNET benchmark fully functional. For each
CNN architecture (mostly image recognition), we can measure their **accuracy**,
**running memory on CPU and GPU**, **storage space on disk**, **training time**,
and **prediction time**.
- Jul-Aug 2017: Implementation of our compressing algorithm.
- May-Jun 2017: Implementation and data collection for other competing algorithms.
- April 2017: Literature research and running existing methods.

## <i class="fa fa-tachometer"></i> Benchmark framework

In order to have a robust testing toolbox for the project, we have decided
to make a benchmark framework in which we can compile **Caffe models**, train
them, and perform various type of measurements:

- Accuracy: Report accuracy on an isolated testing data. The benchmark should
also report f1-score if the classes distribution is skewed.
- Memory: Report the memory required to run the deep model. The benchmark shoud
be able to report memory statistics in both running case: CPU and GPU.
- Time: Report model running time and training time.
- Storage and power consumption: This feature is optional since we focus on
the memory consumption of a model.
- Visualization: This feature is optional, check
[DeepVis](https://github.com/yosinski/deep-visualization-toolbox) for more detail.
