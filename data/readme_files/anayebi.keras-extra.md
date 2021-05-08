# keras-extra
Extra Layers that I have added to **Keras: Deep Learning library for Theano and TensorFlow**. More information about Keras can be found here: https://github.com/fchollet/keras/

These layers allow you to connect a Convolutional Neural Network (CNN) with a Recurrent Neural Network (RNN) of your choice by allowing the CNN layers to be time distributed.

For an **example** of using these layers, see here: https://github.com/jamesmf/mnistCRNN

Currently, this code works with **Keras v. 0.3.0**.

For versions of these layers that are compatible with earlier versions of Keras, feel free to check out the following prior commits:

b4dc512 will work with Keras v. 0.2.0

fb135ee will work with Keras v. 0.1.0

Supports both **Theano** and **TensorFlow** backends. For simplicity, in this ReadMe, we will adhere to the default Theano dim ordering, but to have the layers work with TensorFlow simply use the TensorFlow ordering specified in Keras.

If you are using TimeDistributedConvolution2D as the first layer of the network, then for the Theano backend, you must specify the input shape with the argument input_shape=(num_time_steps, num_channels, num_rows, num_cols), or if using TensorFlow, supply the argument, batch_input_shape=(batch_num_samples, num_time_steps, num_rows, num_cols, num_channels).

Layers that have been added to the Keras master branch will be noted in the ReadMe and removed from extra.py.

Aran Nayebi, 2016

anayebi@stanford.edu

# Installation Instructions
If you already have Keras installed, for this to work on your current installation, please do the following:

1. Download the appropriate version of Keras (for the current version of these layers, just use Keras 0.3.0):

2. Add extra.py to your Keras installation in the layers directory (keras/layers/), and if you are using the current version of these layers, also add tensorflow_backend.py and theano_backend.py in the backend directory (keras/backend/)

3. Now, cd into the Keras folder and simply run:
    
    python setup.py install

or, if you don't have administrative access, just run:
    
    python setup.py install --user
    
4. Now, to use any layer, just run:
    
    from keras.layers.extra import layername

# Layers

- **TimeDistributedFlatten**

	This layer reshapes input to be flat across timesteps (cannot be used as the first layer of a model)

	Default Input shape (Theano dim ordering): (num_samples, num_timesteps, *)
	
	Default Output shape (Theano dim ordering): (num_samples, num_timesteps, num_input_units)
	
	Potential use case: For stacking after a Time Distributed Convolution/Max Pooling Layer or other Time Distributed Layer
	
- **TimeDistributedConvolution2D**

	This layer performs 2D Convolutions with the extra dimension of time
	
    Default Input shape (Theano dim ordering): (num_samples, num_timesteps, stack_size, num_rows, num_cols)
	
    Default Output shape (Theano dim ordering): (num_samples, num_timesteps, num_filters, num_rows, num_cols), Note: num_rows and num_cols could have changed
	
    Potential use case: For connecting a Convolutional Layer with a Recurrent or other Time Distributed Layer.

- **TimeDistributedMaxPooling2D (and TimeDistributedAveragePooling2D)**

    These layers perform 2D Max Pooling and 2D Average Pooling with the extra dimension of time
	
    Default Input shape (Theano dim ordering): (num_samples, num_timesteps, stack_size, num_rows, num_cols)
	
    Default Output shape (Theano dim ordering): (num_samples, num_timesteps, stack_size, new_num_rows, new_num_cols)
	
    Potential use case: For stacking after a Time Distributed Convolutional Layer or other Time Distributed Layer

# Removed Layers:

- **Permute** (added to keras.layers.core, July 17 2015: https://github.com/fchollet/keras/pull/409)

    Permutes the dimensions of the data according to the given tuple.
    
    Default Input shape (Theano dim ordering): This layer does not assume a specific Default Input shape (Theano dim ordering).
    
    Default Output shape (Theano dim ordering): Same as the Default Input shape (Theano dim ordering), but with the dimensions re-ordered according to the ordering specified by the tuple.

    Arguments: Tuple is a tensor that specifies the ordering of the dimensions of the data.

- **UpSample1D** (added to keras.layers.convolutional, August 16 2015: https://github.com/fchollet/keras/pull/532)

	This layer upsamples input across one dimension (e.g. inverse MaxPooling1D)
	
    Default Input shape (Theano dim ordering): (num_samples, steps, dim)
	
    Default Output shape (Theano dim ordering): (num_samples, upsampled_steps, dim)
	
    Potential use case: For stacking after a MaxPooling1D Layer

- **UpSample2D** (added to keras.layers.convolutional, August 16 2015: https://github.com/fchollet/keras/pull/532)

	This layer upsamples input across two dimensions (e.g. inverse MaxPooling2D)
	
    Default Input shape (Theano dim ordering): (num_samples, stack_size, num_rows, num_cols)
	
    Default Output shape (Theano dim ordering): (num_samples, stack_size, new_num_rows, new_num_cols)
	
    Potential use case: For stacking after a MaxPooling2D Layer
