# Post-Training Quantization of Machine Learning models with TensorFlow Lite
This project is the practical implementation of the Bachelor's Thesis's topic. 
## Task
The task of the topic is using TensorFlow Lite to optimize two machine learning models focused on image classification and semantic segmentation, respectively using the post-training quantization technique provided by TensorFlow Lite. After the model was quantized/optimized, inference was ran using the unoptimized and optimized models on a laptop (Intel-processor based) and on a Raspberry Pi 4 (ARM-processor based). Inference results were compared after running inference with both models in their quantized/unquantized formats.

The image classification model was trained on the [MNIST dataset](http://yann.lecun.com/exdb/mnist/) and the semantic segmentation model was trained on the [Cityscapes](https://www.cityscapes-dataset.com/) dataset.
## Structure
In the ```../jars```
