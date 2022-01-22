---
title: Notes on Neural Network
tags: 'Deep Learning, Neural Network'
date: 2022-01-23 01:20:43
categories:
- [Machine Learning]
- [Deep Learning]
---


# Neural Network

## **Forward Propagation**

***[Forward Propagation](https://www.youtube.com/watch?v=UJwK6jAStmg)*** refers to the calculation and storage of intermediate variables (including outputs) for a neural network in order from the input layer to the output layer.

It is how neural networks make predictions. Input data is “forward propagated” through the network layer by layer to the final layer which outputs a prediction.

### Steps
1. Calculate the weighted input to the hidden layer by multiplying 𝑋 by the hidden weight 𝑊ℎ
2. Apply the input of hidden layer to activation function and pass the result(output of hidden layer) to the final layer
3. Repeat step 2 except this time 𝑋 is replaced by the hidden layer’s output, 𝐻

## **[Cost/Loss/Error Function](https://en.wikipedia.org/wiki/Loss_function)**

A loss function/error function(defined on a data point, prediction and label, and measures the penalty) is ***for a single training example/input***. A cost function, on the other hand, is ***the average loss over the entire training dataset***, which might be a sum of loss functions over your training set plus some model complexity penalty (regularization).
The optimization strategies aim at “minimizing the cost function”.

* [Objective function, cost function, loss function: are they the same thing?](https://stats.stackexchange.com/questions/179026/objective-function-cost-function-loss-function-are-they-the-same-thing)

* A loss function is a part of a cost function which is a type of an objective function.

## **Back Propagation**

***[Back Propagation](https://www.cnblogs.com/charlotte77/p/5629865.html)*** refers to the method of calculating the gradient of neural network parameters. In short, the method traverses the network in reverse order, from the output to the input layer, according to the chain rule from calculus. The algorithm stores any intermediate variables (partial derivatives) required while calculating the gradient with respect to some parameters.

The goals of backpropagation are straightforward: ***adjust each weight in the network in proportion to how much it contributes to overall error***. If we iteratively reduce each weight’s error, eventually we’ll have a series of weights that produce good predictions.

### Steps
1. Compare the actual value output by the forward propagation process to the expected value
2. Moves backward through the network, slightly adjusting each of the weights in a direction that reduces the size of the error by a small degree
3. Both forward and back propagation are re-run thousands of times on each input combination until the network can accurately predict the expected output of the possible inputs using forward propagation.

### Formulas and derivation
1. [反向传播算法（过程及公式推导）](https://blog.csdn.net/u014313009/article/details/51039334?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&utm_relevant_index=2)
2. [Backpropagation](https://brilliant.org/wiki/backpropagation/#)
3. [一文弄懂神经网络中的反向传播法——BackPropagation](https://www.cnblogs.com/charlotte77/p/5629865.html)

## **Stochastic Gradient Descent Algorithm**

***Gradient descent*** is an iterative algorithm, that starts from a random point on a function and travels down its slope in steps until it reaches the lowest point of that function.

Gradient descent **can be slow to run on very large datasets**.

Because one iteration of the gradient descent algorithm requires a prediction for each instance in the training dataset, it can **take a long time when you have many millions of instances**.

***Stochastic Gradient Descent(SGD)*** is a stochastic approximation of gradient descent optimization, since it replaces the actual gradient (calculated from the entire data set) by an estimate thereof (calculated from a randomly selected subset of the data). 

In this variation, the gradient descent procedure is run but the update to the coefficients is performed for each training instance, rather than at the end of the batch of instances.

It is while selecting data points at each step to calculate the derivatives that induces randomness in gradient descent algorithm. SGD randomly picks one data point from the whole data set at each iteration to reduce the computations enormously.


* [How Does the Gradient Descent Algorithm Work in Machine Learning?](https://www.analyticsvidhya.com/blog/2020/10/how-does-the-gradient-descent-algorithm-work-in-machine-learning/)
* [Stochastic Gradient Descent — Clearly Explained !!](https://towardsdatascience.com/stochastic-gradient-descent-clearly-explained-53d239905d31)
* [Gradient Descent For Machine Learning](https://machinelearningmastery.com/gradient-descent-for-machine-learning/)


## **Activation Functions**

* [Linear](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#linear)
* [ELU](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#elu)
* [ReLU](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#relu)
* [LeakyReLU](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#leakyrelu)
* [Sigmoid](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#sigmoid)
* [Tanh](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#tanh)
* [Softmax](https://ml-cheatsheet.readthedocs.io/en/latest/activation_functions.html#softmax)


## References/Sources
1. https://en.wikipedia.org/wiki/Gradient
2. https://en.wikipedia.org/wiki/Gradient_descent
3. [神经网络（全连接）的前向和反向传播](https://zhuanlan.zhihu.com/p/34378516)
4. https://www.youtube.com/watch?v=UJwK6jAStmg
5. https://en.wikipedia.org/wiki/Loss_function
6. https://stats.stackexchange.com/questions/179026/objective-function-cost-function-loss-function-are-they-the-same-thing
7. [反向传播算法（过程及公式推导）](https://blog.csdn.net/u014313009/article/details/51039334?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.pc_relevant_default&utm_relevant_index=2)
8. [Backpropagation](https://brilliant.org/wiki/backpropagation/#)
9. [一文弄懂神经网络中的反向传播法——BackPropagation](https://www.cnblogs.com/charlotte77/p/5629865.html)
10. [How Does the Gradient Descent Algorithm Work in Machine Learning?](https://www.analyticsvidhya.com/blog/2020/10/how-does-the-gradient-descent-algorithm-work-in-machine-learning/)
11. [Stochastic Gradient Descent — Clearly Explained !!](https://towardsdatascience.com/stochastic-gradient-descent-clearly-explained-53d239905d31)
12. [Gradient Descent For Machine Learning](https://machinelearningmastery.com/gradient-descent-for-machine-learning/)