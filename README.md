# Training-Error

## Loss = nan

### 问题可能原因：

1. 如果在迭代的100轮以内，出现NaN，一般情况下的原因是因为学习率过高，需要降低学习率。我们可以不断降低学习率直至不出现NaN为止，一般来说低于现有学习率1→10倍即可。  
2. 如果当前的网络是类似于RNN的循环神经网络的话，出现NaN可能是因为梯度爆炸的原因，一个有效的方式是增加“gradient clipping”（梯度截断来解决）。  
3. 可能用0作为了除数。    
4. 计算loss 的时候中间值出现了0，导致算对数熵结果为NA，解决办法是加上很小的数(epsilon )，比如log(x + 1e-8)。   
5. 需要计算loss的数组越界（尤其是自定义了一个新的网络时，可能出现这种情况）。   
6. 在某些涉及指数计算，可能最后算得值为INF（比如不做其他处理的softmax中分子分母需要计算exp(x)，值过大，最后可能为INF/INF，得到NaN，此时需要确认我们使用的softmax中计算exp(x)时做了相关处理（比如减去最大值等等））。  
7. 第一层激活函数不要使用relu，使用tanh甚至sigmoid ？？？

![Activation Functions](https://github.com/wonniu/Training-Error/raw/master/image/activations.png)
From: https://blog.csdn.net/u013555719/article/details/77863953
