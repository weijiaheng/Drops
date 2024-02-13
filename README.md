## Distributionally Robust Post-hoc Classifiers under Prior Shifts [ICLR 2023]

This repository is the official Tensorflow implementation of [[Distributionally Robust Post-hoc Classifiers under Prior Shifts]](https://openreview.net/forum?id=3KUfbI9_DQE)) accepted by ICLR 2023.

<b>Title</b>: <i>Distributionally Robust Post-hoc Classifiers under Prior Shifts</i> <a href="https://openreview.net/forum?id=3KUfbI9_DQE">[pdf]</a>\
<b>Authors</b>:Jiaheng Wei, Harikrishna Narasimhan, Ehsan Amid, Wensheng Chu, Yang Liu, Abhishek Kumar\
<b>Institute</b>: University of California, Santa Cruz \& Google Research\
<b>One sentence summary</b>: We propose a method for scaling the model predictions at test-time for improved distribution robustness to prior shifts.

**Experimental code for DROPS projects on class-imbalanced learning tasks**

**Example Usage**

(1) Two-step vatriant for training DROPS

Step 1: run synthetic long-tailed cifar experiments with ce loss to get the base model

```
python main_lt.py --dataset 'cifar10' --loss 'ce' --imb_ratio 0.1 --dro_div 'kl'
```

Step 2: perform Distribution RObust PoSthoc on saved model prediction logits obtained from the pre-trained model
```
python drops_test_time.py --dataset 'cifar10' --loss 'drops' --imb_ratio 0.1 --eta_lambda 10 --num_iters 25 --eta_lambda_mult 0.95 --prior_type 'train' --cal_type 'none' --eps 0.9
```

(2) One-step vatriant for training DROPS

To run synthetic long-tailed cifar experiments with ce loss, run

```
python main_lt.py --dataset 'cifar10' --loss 'drops' --imb_ratio 0.1 --dro_div 'kl'
```

<b>Motivation 1:</b>\
How a method performs well under a generic evaluation metric:
<img src="./imgs/metric.png">
When the target distribution r is a uniform vector, such metric covers the mean accuracy and worst accuracy as two extremes.


<b>Motivation 2:</b>\
Deep neural nets could capture represenrations well, we could inherit the learned nice representation and introduce a post-hoc approach to achieve model robustness under prior shifts.
<img src="./imgs/intuition.png">
An example is given as follows:
<img src="./imgs/example.png">


<b>Drops:</b>\
We propose a Distributionally RObust PoSt-hoc method (DROPS), which enablesthe reuse of a pre-trained model for different robustness requirements by simply scaling the modelpredictions. Drops obtains the optimal per-class/group weights for scaling through maximizing the delta-worst accuracy.


<b>Experiments:</b>\
A special case of prior shift is the Class-imbalanced learning.
The code of Drops w.r.t. imbalanced CIFAR-10 and CIFAR-100 datasets will be released soon!

<b>Cite Drops</b>\
If you find the code useful in your research, please consider citing our paper:

<pre>
@inproceedings{
wei2023distributionally,
title={Distributionally Robust Post-hoc Classifiers under Prior Shifts},
author={Jiaheng Wei and Harikrishna Narasimhan and Ehsan Amid and Wen-Sheng Chu and Yang Liu and Abhishek Kumar},
booktitle={International Conference on Learning Representations},
year={2023},
url={https://openreview.net/forum?id=3KUfbI9_DQE}
}</pre>
