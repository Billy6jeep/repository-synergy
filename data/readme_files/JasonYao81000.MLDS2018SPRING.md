# MLDS2018SPRING

Machine Learning and having it deep and structured (MLDS) at NTU 2018 Spring.

This course has four homeworks, group by group. The four homeworks are as follows:
   1. Deep Learning Theory
   2. Sequence-to-sequence Model
   3. Deep Generative Model
   4. Deep Reinforcement Learning

Browse this [course website](http://speech.ee.ntu.edu.tw/~tlkagk/courses_MLDS18.html) for more details.

# Table of Contents
<!--ts-->
   1. [Deep Learning Theory](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#mlds2018springhw1)
      * [Deep vs Shallow](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#1-deep-vs-shallow)
      * [Optimization](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#2-optimization)
      * [Generalization](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#3-generalization)
   2. [Sequence-to-sequence Model](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw2#mlds2018springhw2)
      * [Video caption generation](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw2/hw2_1#mlds2018springhw2hw2_1)
      * [Chat-bot](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw2/hw2_2#mlds2018springhw2hw2_2)
   3. [Deep Generative Model](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#mlds2018springhw3)
      * [Image Generation](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-1-image-generation)
      * [Text-to-Image Generation](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-2-text-to-image-generation)
      * [Style Transfer](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-3-style-transfer)
   4. [Deep Reinforcement Learning](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#mlds2018springhw4)
      * [Policy Gradient](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-1-policy-gradient)
      * [Deep Q Learning](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-2-deep-q-learning)
      * [Actor-Critic](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-3-actor-critic)
<!--te-->

# Results of Four Homeworks

## 1. Deep Learning Theory
* [Report.pdf](https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw1/Report.pdf)

### 1.1 Deep vs Shallow
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#1-deep-vs-shallow)
   
### 1.2 Optimization
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#2-optimization)
   
### 1.3 Generalization
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw1#3-generalization)

## 2. Sequence-to-sequence Model
   
### 2.1 Video caption generation
   * BLEU@1 = 0.7204
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw2/hw2_1#mlds2018springhw2hw2_1)
   * [hw2_1/report.pdf](https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw2/hw2_1/report.pdf)

### 2.2 Chat-bot
   * Perplexity = 11.83, Correlation Score = 0.53626
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw2/hw2_2#mlds2018springhw2hw2_2)
   * [hw2_2/report.pdf](https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw2/hw2_2/report.pdf)
      
## 3. Deep Generative Model
* [report.pdf](https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw3/reprot.pdf)

### 3.1 Image Generation
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-1-image-generation)
   * Image Generation: 100% (25/25) Pass Baseline

   |./gan-baseline/baseline_result_gan.png|
   |:------------------------------------:|
   |<img src="https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw3/gan-baseline/baseline_result_gan.png" width="100%">|
   
### 3.2 Text-to-Image Generation
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-2-text-to-image-generation)
   * Text-to-Image Generation: 100% (25/25) Pass Baseline

   | Testing Tags |./gan-baseline/baseline_result_cgan.png|
   |:------------:|:-------------------------------------:|
   |blue hair blue eyes<br><br><br>blue hair green eyes<br><br><br>blue hair red eyes<br><br><br>green hair blue eyes<br><br><br>green hair red eyes|<img src="https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw3/gan-baseline/baseline_result_cgan.png" width="100%">|

### 3.3 Style Transfer
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw3#3-3-style-transfer)
     
## 4. Deep Reinforcement Learning
* [report.pdf](https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw4/report.pdf)

### 4.1 Policy Gradient
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-1-policy-gradient)
   * Policy Gradient: Mean Rewards in 30 Episodes = 16.466666666666665

   <img src="https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw4/results/gif/Pong.gif" width="50%">
   
### 4.2 Deep Q Learning
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-2-deep-q-learning)
   * Deep Q Learning: Mean Rewards in 100 Episodes = 73.16

   <img src="https://github.com/JasonYao81000/MLDS2018SPRING/blob/master/hw4/results/gif/Breakout.gif" width="25%">

### 4.3 Actor-Critic
   * [README](https://github.com/JasonYao81000/MLDS2018SPRING/tree/master/hw4#4-3-actor-critic)
