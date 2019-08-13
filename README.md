# Deep-learning-based-human-action-recognition-using-human-skeletons
This repository explains deep learning based human action recognition using Skeleton images. Action recognition is a very well studied problem in the field of computer vision because of its several uses in data augmentation, autonomous robots and self driving cars etc. Human action can be recognized from its appearance, geometrical shape, joint variations and body skeleton. Among all these, Human skeletons carry the most significant amount of information with minimum noise. However, the extraction and modeling of dynamic human skeletons has always been a a challenging work. The dynamic human skeletons can be represented by a time series of human joint locations in the form of 2D or 3D coordinates and human action can be recognized by analyzing the motion pattern of these coordinates.In this project, I using BerkeleyMHAD dataset because it is not a very large or computationally expensive datset to start and it provides video sequences in various modalities. I am only using Kinect v1 rgb data frames. Some preprocessing of the dataset is done by applying [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) COCO model to extract skeleton images, composite images and keypoint locations to avoid overfitting. This preprocessed data is analyzed by various deep learning techniques like Convolutional autoencoders, Convolutional Neural Networks (CNN) and Long Short Term Memory (LSTM) networks.

## Berkeley MHAD Dataset
Berkeley MHAD dataset is available to download for free from the official web page of Teleimmesion lab, University of California (http://tele-immersion.citris-uc.org/berkeley_mhad). The dataset offers several modalities like MoCAP data, depth images, RGB frames, audio recordings etc. But here we only need Kinect RGB data frames. The dataset consists of 12 subjects and each of which performs eleven actions and repeats each action five times. One video sequence of subject 4, action 8 and repetition 5 is missing for Kinect data. rest of the dataset consists of 659 video sequences which are downloaded. The authors of this dataset have suggested a standard protocol to follow for training and testing. According to this protocol, first seven subjects should be used for training and the remaining five subjects should be used for testing. We continue to follow this protocol and move to preprocessing stage.

## Preprocessing of the dataset using OpenPose
Preprocessing of the datset is done by Notebook file 'Main Extract.ipynb'. In this project, OpenPose COCO model is being used to extract keypoints from the video frames. The detailed explanation of using this model have been presented in this blog (https://www.learnopencv.com/multi-person-pose-estimation-in-opencv-using-openpose/). We do not even need to install OpenPose which is a very challenging task for beginner of Ubuntu. In the code, we are providing pretrained caffe model and network architecture of OpenPose to deep neural network module of OpenCV. Pretrained caffe model weights can be downloaded from https://drive.google.com/file/d/1qVU08ZOu0LR8TSjROhOzlugSKebkFfHr/view?usp=sharing and should be placed in the path /pose/coco/. In the 'Main Extract.ipynb' file we first capture frames of each video sequence, resize it, apply pose estimation function 'process_single_image' which returns composite images (keeypoints plotted on the original image), skleton images and keypoint locations. In this project, only skeleton images and keypoint locations have been used to train models.

## Pickel formation of skleton data
The training and test skeleton data is pickled to use on Colab which is a free open source jupyter notebook environment by using the notebook file 'make_pickle.ipynb'. These pickles can be downloaded from .

## Training and Testing of the skeleton data
#### LSTM modelling
LSTM model was choosen based on the idea that activity recognition is a temporal process and time sequence of frames is important. Various LSTM architestures were tried and hyper paramter tuning is done using Grid Optimization. The final best accuracy obtained by applying LSTM on skeleton images is 90.9 % for test case. The trained model weights 'rnn_6.h5' and architecture 'rnn_6.json' have been provided in models folder. <br/>
Another investigation of LSTM model was done on keypoint locations in the notebook file 'keypoint_locations_training.ipynb'. But very low test accuracy of only 50% was obtained even after doing some hyperparameter tuning.

#### Convolutional Neural Network Modelling
Famous AlexNet architecture was choosen as a CNN model to classify skeleton images. After doing some hyper parameter tuning, the final maximum efficieny obtained 90.58% by training with 'AlexNet_train.ipynb' notebook file. Trained model waights and architecture have been uploaded in '/trained_models/'directory. 

#### Convolutional Autoencoder
Famous AlexNet architecture was choosen as a CNN model to classify skeleton images. After doing some hyper parameter tuning, the final maximum efficieny obtained 90.58% by training with 'AlexNet_train.ipynb' notebook file. Trained model waights and architecture have been uploaded in '/trained_models/'directory. 
