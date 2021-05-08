Chainer example code for NLP
============================

**This repository is out of date and rough. I do not guarantee that these code works correctly.**

**I am developing a new NMT toolkit [NMTKit](https://github.com/odashi/nmtkit) and strongly recommend to use it instead of these samples to train neural translation models.**

This repository contains some neural network examples
for natural language processing (NLP)
using **Chainer** framework.

[Chainer Official](http://chainer.org/ "Chainer official") ([GitHub](https://github.com/pfnet/chainer "Github"))

Making Local Client
-------------------

Before running these scripts, making a local python client using `pyenv` is
reccomended, like:

    $ pyenv install 3.5.0
    $ pyenv virtualenv 3.5.0 example
    $ pyenv shell example
    $ pip install chainer

Contents
--------

* **Machine Translation**
    * `mt_s2s_encdec.py` - Using encoder-decoder style recurrent neural network
    * `mt_s2s_attention.py` - Using attentional neural network

* **Word Segmentation (Tokenization)**
    * `seg_ffnn.py` - Using feedforward neural network
    * `seg_rnn.py` - Using recurrent neural network

* **Language Model**
    * `lm_rnn.py` - Using recurrent neural network (RNNLM)

Contact
-------

If you find an issue or have some questions, please contact Yusuke Oda:
* @odashi_t on Twitter (faster than other methods)
* yus.takara (at) gmail.com

