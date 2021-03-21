# Cassava-Leaf-Disease-Classification

## Table of contents
* [Goal](#Goal)
* [Challenges](#challenges)
* [Summary](#summary)
* [Lesson](#Lesson learned)
* 

My learning journey of Cassava Leaf Diseases competition. I spent around 3 full weeks on this competition. 

## Goal
To classify types of disease that presented on a Cassava Leaf. There five different labels: Cassava Bacterial Blight (CBB), Cassava Brown Streak Disease (CBSD), Cassava Green Mottle (CGM), Cassava Mosaic Disease (CMD) and Healthy.

## Challenges 
There are a few challenges in this competition.
1. Imbalanced distribution between each class. There is a huge difference between the label 3 CMD to other classes. This may create a bias to the prediction. Hence, a weighted loss function or oversampling must be adopted. 
2. Noisy label. There are quite a few of mislabelled images and multiple diseases within one image, which can affect the model prediction. To deal with this problem, there are several techniques that can be implemented such as label smoothing, mix-up, cut-mix augmentations.

## Summary
I joined the competition towards the end of the competition, so there were lots of discussion going on regarding how to deal with noisy label and what models work best in this competition. Majority of the competitors adopted the Efficientnet and Vision Transformer (ViT), so I began to build a solid Efficientnet model before trying other models such as ViT, DeiT, Hybrid Resnet and ViT. 

To tackle the first challenge of imbalanced distribution, I used the external data from previous year Cassava Leaf competition by sampling all the classes except CMD. Although the imbalanced distribution still exists, it improves my local CV. 
In terms of noisy label, I read several papers to understand how to tackle this issue. 
First paper: Image classification with deep learning in the presence of noisy labels.
https://arxiv.org/abs/1912.05170

Second paper: Normalized loss functions for deep learning with noisy labels.
https://arxiv.org/abs/2006.13554

I tried many different mixes of normalised loss functions (active and passive loss functions). However, none of them worked well in this competition. I  used a common label smoothing loss function with beta of 0.3 that worked best in my model. In addition, bi-tempered loss function was also popular among other competitors. However, I found it hardly to select the right b1 and b2 coefficient, so I did not use it in the final model.
This is a good link to Bi-tempered logistic loss function
https://ai.googleblog.com/2019/08/bi-tempered-logistic-loss-for-training.html

In addition, I read the paper on "Pseudo-Labeling and Confirmation Bias in Deep Semi-Supervised Learning"
https://arxiv.org/abs/1908.02983?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%253A+arxiv%252FQSXk+%2528ExcitingAds%2521+cs+updates+on+arXiv.org%2529

I did try to do pseudo labelling in this competition, but my model did not have high confidence level in the prediction due to the effect of label smoothing. Therefore, I think it is too risky to use low threshold in selecting the samples, so I did not use pseudo labelling in the end. 

In my final submission, it is an ensemble of ViT and efficientnet models with a simple weight averaging. Deit and hybrid model did not have good CV compared to ViT and Efficientnet. 

**My final ranking: Private LB 25/3900 teams 0.9011 (Top 1% silver medal) SOLO**

## Lesson learned, 
It is my first competition in the Kaggle competition and also as a solo. I learned a lot in this competition including new architectures such ViT, Deit and hybrid. Moreover, dealing with noisy label is relatively new topic for me although it is very common in the real world data. 
