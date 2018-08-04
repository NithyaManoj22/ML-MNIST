# ML-MNIST
My student project for machine learning through MNIST exercise.

* The python which comes with MacOS does not have certain packages, so it is best to install the packages through [Anaconda Distribution](https://www.anaconda.com/download/#macos). After that, use ```conda install keras``` which will install the latest version of keras. Though the example does not work with the latest (keras 2.0 is not back compatible with 1.2), I had to use ```pip install keras=1.2.2``` to adjust the version to 1.2.2. 

* Use `conda install theano pygpu` to install theano; someone `pip install theano` would have problem after going into python, it cannot find the installation. 

* Somehow keras by default use tensorflow as its backend, use ```export KERAS_BACKEND=theano``` to switch it to theano. 

* Have to add ```from theano import ifelse``` to solve a "Attribute `ifelse` not found" error. 

* The following plotting command does not show plot ```from matplotlib import pyplot as plt; plt.imshow(X_train[0])```. Need to install jupyter notebook to see whether it solves it. 

* Keras 2.2 does not compile ```model.add(Convolution2D(32, 3, 3, activation='relu', input_shape=(1,28,28)))``` has to revert the keras version back to 1.2.2 using ```pip install keras=1.2.2```.  Use 1.2.2 instead of other version because that is the minimum version that coremltools is compatible with. 

* Somehow it has error "OverflowError: Range exceeds valid bounds" for ```model.add(Dense(128, activation='relu'))```, has to add the following script ```from keras import backend as K;
K.set_image_dim_ordering('th')``` which remove the error. 

* Use ```pip install coremltools``` to install Apple coremltools package. 

* Use the following script to convert .h5 model to .mlmodel using coremltools. Note that coremltools does not support conversion of theano backend to .mlmodel. 
```
import coremltools
coreml_model = coremltools.converters.keras.convert('multi_digits_keras.h5')
coreml_model.save('mnist_cnn_keras.mlmodel')
```

* To update Tensorflow to latest: ```conda install -c conda-forge tensorflow```. Use ```conda install -c derickl coremltools``` to install coremltools seems not be able to force to use a lower version of tensorflow. 

* Currently as of July 2018, coremltools only supports Keras 2.1.3 (no later version like 2.2.2), and Tensorflow up to 1.5.0 (no newer version like 1.10). And it also only support `channel_last` as its data format. Edit keras.json located at ```$HOME/.keras/keras.json``` to change the default data format. 

Note: 
```
WARNING:root:Keras version 2.2.0 detected. Last version known to be fully compatible of Keras is 2.1.3 .
WARNING:root:TensorFlow version 1.9.0 detected. Last version known to be fully compatible is 1.5.0 .
```


### References

* [TUTORIALS
Keras Tutorial: The Ultimate Beginner’s Guide to Deep Learning in Python](https://elitedatascience.com/keras-tutorial-deep-learning-in-python)
* [Saving & Loading Keras Models](https://jovianlin.io/saving-loading-keras-models/)
* [Converting Trained Models to Core ML](https://developer.apple.com/documentation/coreml/converting_trained_models_to_core_ml)
* [Installing Jupyter](https://jupyter.org/install.html)
* [Running the Jupyter Notebook](https://jupyter.readthedocs.io/en/latest/running.html)
