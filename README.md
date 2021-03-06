# Traffic Sign Classification

Self-Driving Car Engineer Nanodegree Program

---

[//]: # (Image References)

[image1]: ./writeup/hist_train.png "Visualization Hist Train Data"
[image2]: ./writeup/hist_test.png "Visualization Hist Test Data"
[image3]: ./writeup/hist_valid.png "Visualization Hist Validation Data"
[image4]: ./writeup/AllSignsAndLabels.png "Visualization All Signs"
[image5]: ./writeup/grayscale.png "Grayscale"
[image6]: ./writeup/grayscale_norm.png "Grayscale and Normalization"
[image7]: ./writeup/grayscale_norm_hist.png "Grayscale, Normalization and Histogram"
[image8]: ./writeup/trainprogress.png "Training and Validation Accuracy"
[image9]: ./writeup/newSigns.png "New Signs with label"


## Introduction
In this project a convolutional neural network (CNN) was built to classify traffic signs using TensorFlow. The model was trained and validated with the [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset).


The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

## The Approach

Here is the link to the notebook containing the [project code](https://github.com/JulePralle/SDC_Term1_Project2_TrafficSignClassifier1/blob/master/Traffic_Sign_Classifier.ipynb)

### Load The Data and packages
In the first code cell all needed packages got imported. 
The second code cell loads all the data (training set, testing set, validation set and signalnames).


### Data Set Summary & Exploration

#### 1. Data Set Overview
The code for this step is contained in the third code cell of the IPython notebook.  

Here I calculated an overview  of the traffic signs data set:

* The size of training set is 34799
* The size of test set is 12630
* The size of validation set is 4410
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Exploratory Visualization of the Dataset 

The code for this step is contained in the forth code cell of the IPython notebook.  

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is distributed across the sign labels. There is a chart for every single data set.  

![alt text][image1]
![alt text][image2]
![alt text][image3]

The next chart shows five random choosen examples for every sign label/class id. 

![alt text][image4]



### Design and Test a Model Architecture

#### 1. Pre-Processing
The code for this step is contained in the fith code cell of the IPython notebook.

The prerocessing of the data contains the following steps:

* Converting to grayscale
* Normalization
* Histogram equalization

The grayscale conversion is done here because the exact color information is not an important factor to identify and classify traffic signs. This conversion also reduces the number of dimensions of an image from 3 to 1, which reduces the complexity of calculation and leads to a higher efficiency.

Here an example of grayscaling is shown:

![alt text][image5]

The normalization to the image size is included here to handle arbitrary size image later. The size normalization is necessary because the model is designed to process a fixed size (32x32x1) image.

Here an example of grayscaling and nomalization is shown:

![alt text][image6]


The method of histogram equalization usually increases the global contrast of many images, especially when the usable data of the image is represented by close contrast values. The method is useful in images with backgrounds and foregrounds that are both bright or both dark, which is the case in many images of the data set.

Here an example of grayscaling, normalization and histogram equalization is shown:

![alt text][image7]



#### 2. Set-up Training, Validation and Testing Data

The data had already been splitted into trainig, test and validation sets. Therefore, no changes were done to the data sets. 


#### 3. Final Model Architecture 

The code for my final model is located in the eight cell of the ipython notebook. 

This architecture is based on a LeNet model and to avoid overfitting the dropout technique is applied.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, output 28x28x6 	|
| RELU					|	-											|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5     	| 1x1 stride, valid padding, output 10x10x16 	|
| RELU					| -											|
| Max pooling	      	| 2x2 stride,  output 5x5x16 				|
| Flatten  | output 400
| Fully connected		| output 120  |
| RELU					|			-									|
| Dropout					|		-										|
| Fully connected		| output 84  |
| RELU					|		-										|
| Dropout					|	-											|
| Fully connected		| output 43  |
| Softmax				|    -     									|



#### 4. Train, Validate and Test the Model

The code for the training pipeline is located in the tenth cell of the ipython notebook. To start the training the twelfth cell need to run.

The following parameters were used:

* Learning rate: 0.001
* Number of epochs: 20
* batch size: 100
* keep propability rate of the dropout: 0.5

The learning rate is not changed in a training session. The dropout technique is added to avoid overfitting. The number of epochs and batch size may seem relatively small, but all parameters here are decided by trial-and-error. 
The already implemented Adam optimizer were used.

Here the training and validation accuracy across the epochs is shown:

![alt text][image8]


#### 5. Evaluate the Model

The code for calculating the accuracy of the model is located in the 14th cell of the Ipython notebook.

My final model results are:
* Test Accuracy = 0.929
* Train Accuracy = 0.990
* Validation Accuracy = 0.956


#### 6. Summary
The approach to find a solution was largely trial-and-error until I reached the accuracy on the validation set of 93%. No futher improvements were taken from that moment on. The LeNet model was chosen as a starting model.

The tables below show the proceedure for tuning the hyperparameters, the preprocessing of the data and the architecture of the Lenet model. 

Hypterparameters:

| train accuracy  | valid accuracy  | Batch size  | Epochs | learning rate | 
|:------------:|:------------:|:------------:|:------------:|:------------:| 
| 0.974 | 0.839 | 128 | 10 | 0.001 |
| 0.988 | 0.887 | 128 | 20 | 0.001 |
| 0.989 | 0.872 | 128 | 25 | 0.001 |
| 0.941 | 0.792 | 128 | 20 | 0.0001 |
| 0.991 | 0.850 | 128 | 30 | 0.0001 |
| 0.984 | 0.850 | 200 | 20 | 0.001 |
| 0.990 | 0.898 | 100 | 20 | 0.001 |
| 0.992 | 0.896 | 90 | 20 | 0.001 |

The following parameters were choosen:
* Batch size: 100
* Epochs: 20
* Learning rate: 0.001

Pre-Processing:

| train accuracy  | valid accuracy  | Grayscale  | Nomalization | Hist Equalization | 
|:------------:|:------------:|:------------:|:------------:|:------------:| 
|0.994 | 0.911 | Yes | No | No |
|0.996 | 0.918 | Yes | Yes | No |
|0.994 | 0.931 | Yes | Yes | Yes |

Architecture:
After adding dropouts to Lenet model the training accuracy was 0.991 and the validation accuracy reached 0.957.

### Test a Model on New Images

#### 1. New Images

Here are six German traffic signs with their labels that I found on the web:

![alt text][image9] 

The quality of the images is mostly fine. 

I would assume that the following aspects of the images could cause problems: 
* First image (Ahead only) - there are some branches covering the right corner of the sign. 
* Third image (keep right) - very bright and rotated.
* Fourth image (Speed limit) - very bright.
* Sixth image (Roundabout mandatory) - has a white spot in it which doesn't belong there.

#### 2. Predictions

The code for making predictions on my final model is located in the 16th cell of the Ipython notebook.

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:-------------------------:|:---------------------------------------------:| 
| 35: Ahead only      		| 35: Ahead only  | 
| 14: Stop     			| 14: Stop |
| 38: Keep right					| 38: Keep right |
| 1: Speed limit (30km/h)	      		| 1: Speed limit (30km/h) |
| 11: Right-of-way at the next intersection			| 11: Right-of-way at the next intersection |
| 40: Roundabout mandatory			| 40: Roundabout mandatory |


* actual labels[35, 14, 38, 1, 11, 40]
* predicted labels[35 14 38  1 11 40]
* the model predicted 6 of 6 labels correctly.
* The accurancy for the 6 new images is 100.00%.

This is an expected result after the accuracy of the test set of 93%.

#### 3. Top 5 Softmax Probabilities
The code for making predictions on my final model is located in the 18th cell of the Ipython notebook.


##### For image 1:
* Top 5 Softmax probabilities are: [ 29.93950081  10.01706028   9.59209824   6.27344465   4.57737589].
* Class ids according to the probabilities: [35 12 13  9 33].
* Predicted class in the image is 35.
* Actual class in the image is 35.

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .30         			| 35: Ahead only   									| 
| .10     				| 12: Priority road									|
| .10					| 13: Yield											|
| .06	      			| 9: No passing				 				|
| .05				    | 33: Turn right ahead     							|



##### For image 2:
* Top 5 Softmax probabilities are: [ 24.60022354   9.94486618   5.18482065   3.58972168   3.46426797].
* Class ids according to the probabilities: [14 15 13 17 33].
* Predicted class in the image is 14.
* Actual class in the image is 14.


| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .24         			| 14: Stop   									| 
| .10     				| 15: No vehicles 										|
| .05					| 13: Yield											|
| .04	      			| 17: No entry					 				|
| .03				    | 33: Turn right ahead     							|

##### For image 3:
* Top 5 Softmax probabilities are: [ 33.04686737   4.80756235   1.68317819   1.36036468   1.32535505].
* Class ids according to the probabilities: [38 34  3 15 36].
* Predicted class in the image is 38.
* Actual class in the image is 38.

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .33         			| 38: Keep right   									| 
| .05     				| 34: Turn left ahead										|
| .02					| 3: Speed limit (60km/h)											|
| .01	      			| 15: No vehicles				 				|
| .01				    | 36: Go straight or right     							|

##### For image 4:
* Top 5 Softmax probabilities are: [ 48.57092667  17.88767624  17.1041832    9.36211109   7.19126749].
* Class ids according to the probabilities: [1 0 2 5 4].
* Predicted class in the image is 1.
* Actual class in the image is 1.

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .49         			| 1: Speed limit (30km/h)   									| 
| .18     				| 0: Speed limit (20km/h)										|
| .17					| 2: Speed limit (50km/h)											|
| .09	      			| 5:	Speed limit (80km/h)				 				|
| .07				    | 4: Speed limit (70km/h)     							|


##### For image 5:
* Top 5 Softmax probabilities are: [ 6.99797058  6.69339848  3.21441746  3.21149969  1.74060869].
* Class ids according to the probabilities: [11 30 24 27 23].
* Predicted class in the image is 11.
* Actual class in the image is 11.

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .07         			| 11: Right-of-way at the next intersection   									| 
| .07     				| 30: Beware of ice/snow 										|
| .03					| 24:	Road narrows on the right										|
| .03	      			| 27:	Pedestrians				 				|
| .02				    | 23: Slippery road     							|

##### For image 6:
* Top 5 Softmax probabilities are: [ 16.73239136   3.26947451   0.1359655   -1.86569834  -3.12762356].
* Class ids according to the probabilities: [40 12 37 16  1].
* Predicted class in the image is 40.
* Actual class in the image is 40.

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .17         			| 40: Roundabout mandatory   									| 
| .03     				| 12: Priority road 										|
| .00					| 37: Go straight or left											|
| .00	      			| 16: Vehicles over 3.5 metric tons prohibited				 				|



# Udacity Part
---
The Project

The goals / steps of this project are the following:
* Load the data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

### Dependencies
This lab requires:

* [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit)

The lab enviroment can be created with CarND Term1 Starter Kit. Click [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) for the details.

### Dataset and Repository

1. Download the data set. The classroom has a link to the data set in the "Project Instructions" content. This is a pickled dataset in which we've already resized the images to 32x32. It contains a training, validation and test set.
2. Clone the project, which contains the Ipython notebook and the writeup template.
```sh
git clone https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project
cd CarND-Traffic-Sign-Classifier-Project
jupyter notebook Traffic_Sign_Classifier.ipynb
```

### Requirements for Submission
Follow the instructions in the `Traffic_Sign_Classifier.ipynb` notebook and write the project report using the writeup template as a guide, `writeup_template.md`. Submit the project code and writeup document.
