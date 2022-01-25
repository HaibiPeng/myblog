---
title: Federated Learning and Split Learning Basics
date: 2022-01-25 13:21:14
tags: 'Machine Learning, Deep Learning, Distributed Systems, Security and Privacy'
categories:
- [Machine Learning]
- [Deep Learning]
- [Distributed Systems]
---

# Introduction

Often there needs to be built deep learning applications, that need a lot data, but this data might be available from multiple entities (humans, organizations). And this data might be sensitive, meaning the entities (humans or organizations) from whom we need the data might not want to share this data due to privacy reasons.

Federated learning (FL) and split learning (SL) are two popular distributed machine learning approaches, which can enable collaborative training of distributed machine learning models without any data sharing. Both follow a model-to-data scenario; clients train and test machine learning models without sharing raw data. SL provides better model privacy than FL due to the machine learning model architecture split between clients and the server. Moreover, the split model makes SL a better option for resource-constrained environments.

The blog introduces some basic concepts of FL and SL and it is recommended to check the references/sources at the end.

# Federated Learning

## Concepts

***[Federated learning](https://en.wikipedia.org/wiki/Federated_learning#Definition)*** is a machine learning technique that trains an algorithm **across multiple decentralized edge devices or servers** holding local data samples, **without exchanging them**. 


It aims at training a machine learning algorithm, for instance deep neural networks, **on multiple local datasets contained in local nodes without explicitly exchanging data samples**. The general principle consists in **training local models on local data samples and exchanging parameters** (e.g. the weights and biases of a deep neural network) between these local nodes at some frequency to generate a global model shared by all nodes.

* Data protection, telecommunications, IoT, and pharmaceutics are among the sectors where it's used.

## Categorization of Federated Learning

### Horizontal federated learning

Horizontal federated learning, or sample-based federated learning, is introduced in the scenarios that data sets share the same feature space but different in samples, i.e., the user features ( X1, X2, … ) of the two datasets have a large overlap, while the user ( U1, U2, … ) overlap is small.

<figure>
    <img src="https://media.arxiv-vanity.com/render-output/5547782/HFL.png" alt="Categorization of Federated Learning">
    <figcaption align="center" style="font-size: 12px">(a) Horizontal Federated Learning</figcaption>
</figure>

<figure>
    <img src="https://media.arxiv-vanity.com/render-output/5547782/hfl_arc.png" alt="Architecture for a horizontal federated learning system">
    <figcaption align="center" style="font-size: 12px">Architecture for a horizontal federated learning system</figcaption>
</figure>

### Vertical federated learning

Vertical federated learning, or feature-based federated learning is applicable to the cases that two data sets share the same sample ID space but differ in feature space, i.e., the overlap of users ( U1, U2, … ) of the two datasets is large, while the overlap of user features ( X1, X2, … ) is small;

<figure>
    <img src="https://media.arxiv-vanity.com/render-output/5547782/VFL.png" alt="Categorization of Federated Learning">
    <figcaption align="center" style="font-size: 12px">(b) Vertical Federated Learning</figcaption>
</figure>

<figure>
    <img src="https://media.arxiv-vanity.com/render-output/5547782/3.png" alt="Architecture for a vertical federated learning system">
    <figcaption align="center" style="font-size: 12px">Architecture for a vertical federated learning system</figcaption>
</figure>

### Federated transfer learning

Federated transfer learning applies to the scenarios that the two data sets differ not only in samples but also in feature space, i.e., solves the problem that the overlap between users ( U1, U2, … ) and user features ( X1, X2, … ) of the two datasets is relatively small.

<figure>
    <img src="https://media.arxiv-vanity.com/render-output/5547782/FTL.png" alt="Categorization of Federated Learning">
    <figcaption align="center" style="font-size: 12px">(c) Federated Transfer Learning</figcaption>
</figure>

## Benefits

* FL allows devices such as smartphones to ***learn a shared prediction model collaboratively while maintaining the training data on the devices*** rather than uploading and storing it on a central server.
* Moves model teaching to the edge, including gadgets like smartphones, laptops, IoT, and even "organizations" like hospitals that must work under stringent privacy regulations. It is a ***significant security advantage to keep personal data local***.
* Since prediction takes place on the system itself, ***real-time prediction is feasible***. The time lag caused by sending raw data to a central server and then shipping the results back to the system is reduced by FL.
* The amount of hardware equipment available is reduced by FL. FL versions need very little hardware, and what is available on mobile devices is more than adequate.


# Split Learning

## Motivation

***[Split learning](https://scholar.google.com/scholar?hl=zh-CN&as_sdt=0%2C5&q=split+learning&btnG=)*** naturally allows for various configurations of cooperating entities to train (and infer from) machine learning models without sharing any raw data or detailed information about the model.

## Key idea and steps

In the simplest of configurations of split learning, let's consider a client-server architecture. The steps are as follows.
### Forward Propagation
1. Each client (for example, radiology center) trains a partial deep network up to a specific layer known as the ***cut layer***. 
2. The outputs at the cut layer are sent to another entity (server/another client, for example, computational entity) which completes the rest of the training ***without looking at raw data from any client that holds the raw data***. This completes a round of ***forward propagation*** without sharing raw data. 
### Backward Propagation
3. The gradients are now ***back propagated*** again from its last layer until the cut layer in a similar fashion. 
4. The gradients at the cut layer (and only these gradients) are sent back to radiology client centers. ***The rest of back propagation*** is now completed at the radiology client centers. 
5. This process is continued until the distributed split learning network is trained without looking at each others raw data.

<figure>
    <img src="SL.png" alt="Data flow between the client and the server in Algorithm 1 and 2">
    <figcaption align="center" style="font-size: 12px">Data flow between the client and the server in Algorithm 1 and 2</figcaption>
</figure>

## Versatile plug-and-play configurations of split learning

Versatile configurations of split learning configurations cater to various practical settings of 
i) multiple entities holding different modalities of patient data, 
ii) centralized and local health entities collaborating on multiple tasks, 
iii) learning without sharing labels, 
iv) multi-task split learning, 
v) multi-hop split learning and other hybrid possibilities to name a few as shown below and further detailed in this [paper](https://arxiv.org/pdf/1812.00564.pdf).

<figure>
    <img src="https://dam-prod.media.mit.edu/thumb/2018/12/11/splitConfig_C4njd4y.png.1400x1400.png" alt="Versatile configurations of split learning configurations">
    <figcaption align="center" style="font-size: 12px">Versatile configurations of split learning configurations</figcaption>
</figure>

<figure>
    <img src="https://miro.medium.com/max/1400/1*G70zWOQ8e6YgBsx641Obmw.png" alt="SplitNN Configurations with and without label sharing">
    <figcaption align="center" style="font-size: 12px">SplitNN Configurations with and without label sharing</figcaption>
</figure>

## Benefits

***Client-side communication costs are significantly reduced*** as the data to be transmitted is restricted to initial layers of the split learning network (splitNN) prior to the split. ***The client-side computation costs of learning the weights of the network are also significantly reduced*** for the same reason. In terms of model performance, ***the accuracies of Split NN remained competitive*** to other distributed deep learning methods like federated learning and large batch synchronous SGD with a drastically smaller client side computational burden when training on a larger number of clients.

<figure>
    <img src="https://miro.medium.com/max/1400/1*Jdy8C7tCZHlBFjVz5xKvCA.png" alt="Split Learning advantages">
    <figcaption align="center" style="font-size: 12px">Split Learning advantages</figcaption>
</figure>

## References/Sources

1. https://en.wikipedia.org/wiki/Federated_learning#Definition
2. https://www.xenonstack.com/blog/edge-ai-vs-federated-learning
3. https://blog.csdn.net/weixin_45439861/article/details/100670390
4. https://www.arxiv-vanity.com/papers/1902.04885/
5. https://zhuanlan.zhihu.com/p/79284686?utm_source=wechat_session
6. https://blog.csdn.net/weixin_45439861/article/details/100670390
7. Yang, Qiang, et al. "Federated machine learning: Concept and applications." ACM Transactions on Intelligent Systems and Technology (TIST) 10.2 (2019): 1-19.
8. Liu, Yang, et al. "A secure federated transfer learning framework." IEEE Intelligent Systems 35.4 (2020): 70-82.
9. Chen, Yiqiang, et al. "Fedhealth: A federated transfer learning framework for wearable healthcare." IEEE Intelligent Systems 35.4 (2020): 83-93.
10. Li, Tian, et al. "Federated learning: Challenges, methods, and future directions." IEEE Signal Processing Magazine 37.3 (2020): 50-60.
11. https://www.media.mit.edu/projects/distributed-learning-and-collaborative-learning-1/overview/
12. http://splitlearning.mit.edu/
13. Abuadbba, Sharif, et al. "Can we use split learning on 1d cnn models for privacy preserving training?." Proceedings of the 15th ACM Asia Conference on Computer and Communications Security. 2020.
14. Vepakomma, Praneeth, et al. "Split learning for health: Distributed deep learning without sharing raw patient data." arXiv preprint arXiv:1812.00564 (2018).
15. Vepakomma, Praneeth, et al. "No peek: A survey of private distributed deep learning." arXiv preprint arXiv:1812.03288 (2018).
16. https://liveramp.com/developers/blog/privacy-preserving-split-learning/
17. Gupta, Otkrist, and Ramesh Raskar. "Distributed learning of deep neural network over multiple agents." Journal of Network and Computer Applications 116 (2018): 1-8.
18. Vepakomma, Praneeth, et al. "No peek: A survey of private distributed deep learning." arXiv preprint arXiv:1812.03288 (2018).