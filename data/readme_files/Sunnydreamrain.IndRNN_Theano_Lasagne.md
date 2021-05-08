# Independently Recurrent Neural Networks
This code is to implement the [IndRNN](https://arxiv.org/abs/1803.04831). It is based on Theano and Lasagne. Please refer to [this one](https://github.com/Sunnydreamrain/IndRNN_pytorch) for pytorch.

Please cite the following paper if you find it useful.  
[Shuai Li, Wanqing Li, Chris Cook, Ce Zhu, and Yanbo Gao. "Independently Recurrent Neural Network (IndRNN): Building A Longer and Deeper RNN." CVPR 2018.](https://arxiv.org/abs/1803.04831)

@inproceedings{li2018independently,  
  title={Independently recurrent neural network (indrnn): Building A longer and deeper RNN},  
  author={Li, Shuai and Li, Wanqing and Cook, Chris and Zhu, Ce and Gao, Yanbo},  
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},  
  pages={5457--5466},  
  year={2018}  
} 

# Summary  
In IndRNNs, neurons in each layer are independent from each other, and the cross-channel information is obtained through stacking multiple layers.  
Advantages over the RNN and/or LSTM:  
- The gradient backpropagation through time can be regulated to effectively address the gradient vanishing and exploding problems.  
- Long-term memory can be kept with IndRNNs to process long sequences. Experiments have demonstrated that an IndRNN can well process sequences over 5000 steps.  
- An IndRNN can work well with non-saturated function such as relu as activation function and be trained robustly.  
- Multiple layers of IndRNNs can be efficiently stacked, especially with residual connections over layers, to increase the depth of the network. An example of 21 layer-IndRNN is demonstrated in the experiments.  
- Behaviour of IndRNN neurons in each layer are easy to interpret due to the independence of neurons in each layer.  

Experiments have demonstrated that IndRNN performs much better than the traditional RNN and LSTM models on various tasks such as the adding problem, sequential MNIST classification, language modelling and action recognition.

# Usage 
`IndRNN.py` provides the IndRNN function as described in the paper.  
`IndRNN_onlyrecurrent.py` provides only the recurrent+activation of the IndRNN function. Therefore, processing of the input with dense connection or convolution operation is needed. This is usedful for adding batch normalization (BN) between the processing of input and activation function.

### Requirements  
[Theano](http://deeplearning.net/software/theano/install.html) and [Lasagne](https://lasagne.readthedocs.io/en/latest/user/installation.html) need to be installed first.  
```
pip install --upgrade https://github.com/Theano/Theano/archive/master.zip
pip install --upgrade https://github.com/Lasagne/Lasagne/archive/master.zip
```

## For the adding example   
`python -u adding.py`  
Different options are available in adding.py.  
Example: `python -u adding.py --model indrnn --seq_len 100`  
Example of using GPU: `THEANO_FLAGS='floatX=float32,device=cuda0,mode=FAST_RUN' python -u adding.py --model indrnn --seq_len 100`  

## For the Sequential MNIST example  
`python -u pixelmnist.py --use_bn_afterrnn`   
or with options: 
`python -u adding.py --model indrnn --num_layers 6 --hidden_units 128 --use_bn_afterrnn`  
Example of using GPU: `THEANO_FLAGS='floatX=float32,device=cuda0,mode=FAST_RUN' python -u adding.py --model indrnn --num_layers 6 --hidden_units 128 --use_bn_afterrnn`  

For this task, the batch normalization (BN) is used. It can be used before the activation function (relu) or after it. In our experiments, it converges faster by putting BN after the activation function.  

## For the language modeling example using character-level Penn Treebank (PTB-c)   
`python -u penntree_charlevel_rernn.py --data_aug --hidden_units 2000 --use_dropout --num_layers 6 --droprate 0.25 --seq_len 150 --use_weightdecay_nohiddenW`  
`data_aug` here only provides different start for each training epoch to provide stable statistics for BN.  
or using the residual model:  
`python -u penntree_charlevel_rernn.py --data_aug --hidden_units 2000 --use_residual --num_layers 11 --use_dropout --droprate 0.3 --seq_len 150 --use_weightdecay_nohiddenW`  
The example code provides the very basic implementation of residual IndRNN where the number of units in all the IndRNN layers are the same and the left branch is fixed to be 1 without further using weight processing. Other network architectures can be explored which may provide better results.

For this task, output is provided at each time step and can only use the information before the current time step. Therefore, the statistics (mean and variance) of the batch normalization (BN) are obtained for each time step. It is used before the activation which is more robust than putting it after the activation. The main reason is that the outputs of all the IndRNN layers at the last time step is further used as initialization of the next batch. By putting BN before the activation (which is also before the recurrent accumulation), the statistics of BN is more stable than putting BN after the activation.    

## For the language modeling example using word-level Penn Treebank      
Please find details in the directoy [wordPTB](https://github.com/Sunnydreamrain/IndRNN_Theano_Lasagne/tree/master/wordPTB).  

## For the skeleton-based Action Recognition example  
Please find details in the directoy [action recognition](https://github.com/Sunnydreamrain/IndRNN_Theano_Lasagne/tree/master/action%20recognition).  

# Considerations in implementation  
### 1, Initialization of the recurrent weights
For relu, `Uniform(0,1)` is used to make different neurons keep different kinds of memory. But for problems that only use the output of the last time step such as the adding problem, MNIST classification problem, and action recognition problem, the recurrent weights for the last IndRNN layer (caution: only the last one not all) can be initialized to be all `1` or a proper range `(1-epsilon, 1+epsilon)` where `epsilon` is a small number, since only long-term memory is needed for the output of this layer. Examples are shown in [adding.py](https://github.com/Sunnydreamrain/IndRNN_Theano_Lasagne/blob/master/adding/adding.py#L49).  

### 2, Constraint of the recurrent weights  
For relu, generally it can be set to `[-U_bound, U_bound]` where `U_bound=pow(args.MAG, 1.0 / seq_len)` and `MAG` can be 2 or 10 or others. If the sequence is very long, it can be `[-1, 1]` since it is very close to 1 and the precision of GPU is limited. If the sequence is short such as 20, no constraint is needed. Example of the constraint is shown at [adding.py](https://github.com/Sunnydreamrain/IndRNN_Theano_Lasagne/blob/master/adding/adding.py#L150). By the way, this constraint can also be implemented as a weight decay of ||max(0,|U|-U_bound)||.  
For simplicity, the constraint can always set to `[-1, 1]` as it can keep long-term memory already and the difference in performance is small.

### 3, Usage of batch normalization (BN)  
Generally, over 3 layers, BN can help accelerate the training. BN can be used before the activation function or after it. In our experiments, we find it converges faster by putting BN after the activation function. However, for tasks such as PTB_c where the output of one batch is further used as the initialization of the next batch, it is better to put BN before activation as mentioned at the above example.  

### 4, Learning rate  
In our experiments, ADAM with a learning rate of 2e-4 works well.  

### 5, Weight decay  
If weight decay is used, no need to add the recurrent weights.  

### 6, Usage of dropout  
Dropout (if used) is applied with the same mask over time.  

### Note  
The above considerations are just suggestions. I did not explore lots of training techniques such as training methods, initialization techniques. So better results may be achieved with other options.  

# Other implementations
Tensorflow:  
[https://github.com/batzner/indrnn](https://github.com/batzner/indrnn)  
Keras:  
[https://github.com/titu1994/Keras-IndRNN](https://github.com/titu1994/Keras-IndRNN)  
Pytorch:  
[https://github.com/Sunnydreamrain/IndRNN_pytorch](https://github.com/Sunnydreamrain/IndRNN_pytorch)  
[https://github.com/StefOe/indrnn-pytorch](https://github.com/StefOe/indrnn-pytorch)  
[https://github.com/theSage21/IndRNN](https://github.com/theSage21/IndRNN)  
[https://github.com/zhangxu0307/Ind-RNN](https://github.com/zhangxu0307/Ind-RNN)  
CNTK:  
[https://github.com/delzac/cntkx](https://github.com/delzac/cntkx)  
Chainer:  
[https://github.com/0shimax/chainer-IndRNN](https://github.com/0shimax/chainer-IndRNN)  
