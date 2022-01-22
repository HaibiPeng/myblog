---
title: Notes on Transfer Learning
tags: 'Transfer Learning, Machine Learning, Deep Learning'
date: 2022-01-23 01:21:34
categories:
- [Machine Learning]
- [Deep Learning]
---


# Transfer Learning

## Concepts

### 1. Definition

[Transfer learning (TL)](https://en.wikipedia.org/wiki/Transfer_learning) is a research problem in machine learning (ML) that focuses on **storing knowledge gained while solving one problem and applying it to a different but related problem**.

It is a machine-learning method where the application of knowledge **obtained from a model used in one task** can be **reused as a foundation point** for another task.

* Ability of a system to recognize and apply knowledge and skills learned in previous domains/tasks to novel domains/tasks.

### 2. Domain and Task 

* Domain: consists of: a [feature space](https://en.wikipedia.org/wiki/Feature_space) X and a [marginal probability distribution](https://en.wikipedia.org/wiki/Marginal_distribution) P(X)

* Task: consists of two components: a label space Y and an objective predictive function f: X → Y

## Different Types of Transfer Learning

(1) **Inductive Transfer Learning (归纳式迁移学习).** The source and target ***domains are the same(domains一样)***, however, their ***tasks are still different(tasks不一样)*** from each another. The model will use ***inductive biases*** from the source domain to help improve the performance of the target task. The source task ***may or may not contain labeled data***, further leading onto the model using multitask learning and self-taught learning.

* **multitask learning（多任务学习）**：source domain的labeled数据可得。
* **self-taught learning（自学习）**：source domain的labeled数据不可得。

(2) **Transductive Transfer Learning (直推式迁移学习).** The source and target ***tasks share similarities(tasks类似)***, however, the ***domains are different(domains不一样)***. The source domain contains a lot of ***labeled data***, whereas there is ***an absence of labeled*** data in the target domain, further leading onto the model using domain adaptation.

Based on the number of domains and tasks, it can also be further divided into two types:
* **Domain Adaptation（域适配）**：不同的domains+single task
* **Sample Selection Bias（样本选择偏差 / Covariance Shift（协方差转变）**：single domain+single task

(3) **Unsupervised Transfer Learning (无监督迁移学习).** Unsupervised learning is when an algorithm is ***subjected to being able to identify patterns in data sets that have not been labeled or classified***. In this case, the source and target ***domains are similar(domains类似)***, however, ***the tasks are different***, where ***data is unlabeled in both source and target(都不可得)***. Techniques such as dimensionality reduction and clustering are well known in unsupervised learning.

Summarization the different settings and scenarios for each of the above techniques in the following table.

<figure>
    <img src="https://miro.medium.com/max/2000/1*ZEJeJS06czdyPwov5EbCuQ.png" alt="Types of Transfer Learning Strategies and their Settings">
    <figcaption align="center" style="font-size: 12px">Types of Transfer Learning Strategies and their Settings</figcaption>
</figure>


## What to transfer

### 1. **Homogeneous Transfer Learning** (同构迁移学习)

Homogeneous Transfer learning approaches are developed and proposed to handle situations where ***the domains are of the same feature space***.

In Homogeneous Transfer learning, ***domains have only a slight difference in marginal distributions***. These approaches adapt the domains by ***correcting the sample selection bias or covariate shift***.

(1) **Instance-based transfer**（样本迁移）

It covers a simple scenario in which there is ***a large amount of labeled data in the source domain and a limited number in the target domain***. Both the domains and feature spaces ***differ only in marginal distributions***.

In this scenario, it is natural to consider ***adapting the marginal distributions***. Instance-based Transfer learning ***reassigns weights to the source domain instances in the loss function***.

Instance reweighting（样本重新调整权重） and importance sampling（重要性采样）are two main approaches used in instance-based TL.

(2) **Feature-representation transfer**（特征迁移）

Feature-based approaches transform the original features to create a new feature representation. This approach can further be divided into two subcategories, i.e., asymmetric and symmetric Feature-based Transfer Learning.

* **Asymmetric approaches** transform the source features to match the target ones. In other words, we ***take the features from the source domain and fit them into the target feature space***. There can be some information loss in this process due to the marginal difference in the feature distribution.
* **Symmetric approaches** find a common latent feature space and then transform both the source and the target features into this new feature representation.

(3) **Parameter transfer**（参数/模型迁移）

The parameter-based transfer learning approaches transfer the knowledge at the ***model/parameter level***.

This approach involves transferring knowledge through the shared parameters of the source and target domain learner models. One way to transfer the learned knowledge can be ***by creating multiple source learner models and optimally combining the re-weighted learners similar to ensemble learners to form an improved target learner***.

The idea behind parameter-based methods is that ***a well-trained model on the source domain has learned a well-defined structure, and if two tasks are related, this structure can be transferred to the target model***. In general, there are two ways to share the weights in deep learning models: 

* **Soft weight sharing**. The model is expected to be close to the already learned features and is usually penalized if its weights deviate significantly from a given set of weights.
* **Hard weight sharing**. We share the exact weights among different models.

(4) **Relational-knowledge transfer**（关系迁移）

Relational-based transfer learning approaches mainly focus on ***learning the relations between the source and a target domain*** and ***using this knowledge to derive past knowledge and use it in the current context***.

Such approaches transfer ***the logical relationship or rules learned in the source domain to the target domain***.

For example, if we learn the relationship between different elements of the speech in a male voice, it can help significantly to analyze the sentence in another voice.

### 2. **Heterogeneous Transfer Learning** (异构迁移学习)

It is often challenging to collect labeled source domain data with the same feature space as the target domain, and Heterogeneous Transfer learning methods are developed to address such limitations.  

This technique aims to ***solve the issue of source and target domains having differing feature spaces and other concerns like differing data distributions and label spaces***. Heterogeneous Transfer Learning is applied in cross-domain tasks such as cross-language text categorization, text-to-image classification, and many others.

The following table clearly summarizes the relationship between different transfer learning strategies and what to transfer.

<figure>
    <img src="https://miro.medium.com/max/700/1*xK81ohzG-tLRKVexowUvgw.png" alt="Transfer Learning Strategies and Types of Transferable Components">
    <figcaption align="center" style="font-size: 12px">Transfer Learning Strategies and Types of Transferable Components</figcaption>
</figure>

<figure>
    <img src="https://miro.medium.com/max/611/1*mEHO0-LifV7MgwXSpY9wyQ.png" alt="An overview of different settings of transfer">
    <figcaption align="center" style="font-size: 12px">An overview of different settings of transfer</figcaption>
</figure>

## Models

### For computer vision
1. Xception
2. VGG16
3. VGG19
4. ResNet50
5. InceptionV3
6. InceptionResNetV2
7. MobileNet
8. MobileNetV2
9. DenseNetV2
10. DenseNet121
11. DenseNet169
12. DenseNet201
13. NASNetMobile
14. NASNetLarge

### For natural language processing
1. Universal Sentence Encoder by Google
2. Bidirectional Encoder Representations from Transformers (BERT) by Google

### For sound recognition
1. AudioSet
2. FreeSound
3. SoundWatch


# References/sources
1. [A Comprehensive Hands-on Guide to Transfer Learning with Real-World Applications in Deep Learning](https://towardsdatascience.com/a-comprehensive-hands-on-guide-to-transfer-learning-with-real-world-applications-in-deep-learning-212bf3b2f27a)
2. [A Newbie-Friendly Guide to Transfer Learning](https://www.v7labs.com/blog/transfer-learning-guide)
3. [迁移学习--综述](https://blog.csdn.net/vvnzhang2095/article/details/79882013?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&utm_relevant_index=2)
4. Pan S J, Yang Q. A survey on transfer learning[J]. IEEE Transactions on knowledge and data engineering, 2009, 22(10): 1345-1359.
5. Weiss K, Khoshgoftaar T M, Wang D D. A survey of transfer learning[J]. Journal of Big data, 2016, 3(1): 1-40.
6. Zhuang F, Qi Z, Duan K, et al. A comprehensive survey on transfer learning[J]. Proceedings of the IEEE, 2020, 109(1): 43-76.
7. Carney M, Webster B, Alvarado I, et al. Teachable machine: Approachable Web-based tool for exploring machine learning classification[C]//Extended abstracts of the 2020 CHI conference on human factors in computing systems. 2020: 1-8.
8. Goodman S M, Liu P, Jain D, et al. Toward user-driven sound recognizer personalization with people who are d/deaf or hard of hearing[J]. Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies, 2021, 5(2): 1-23.
9. Laput G, Ahuja K, Goel M, et al. Ubicoustics: Plug-and-play acoustic activity recognition[C]//Proceedings of the 31st Annual ACM Symposium on User Interface Software and Technology. 2018: 213-224.
10. https://github.com/jindongwang/transferlearning
11. https://github.com/googlecreativelab/teachable-machine-boilerplate