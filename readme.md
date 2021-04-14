# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/dataset_visualization.jpg "Visualization"
[image4]: ./internet%20signs/sign1.jpg "Traffic Sign 1"
[image5]: ./internet%20signs/sign2.jpg "Traffic Sign 2"
[image6]: ./internet%20signs/sign3.jpg "Traffic Sign 3"
[image7]: ./internet%20signs/sign4.jpg "Traffic Sign 4"
[image8]: ./internet%20signs/sign5.jpg "Traffic Sign 5"
[image9]: ./examples/model_results.jpg "model results"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799?
* The size of the validation set is 4410?
* The size of test set is 12630?
* The shape of a traffic sign image is (32, 32)?
* The number of unique classes/labels in the data set is 43?

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. Here we can find that in all subsets we have unbalanced classes.

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Preprocessing

I have multiplied the dataset by adding some random noise and random rotating degrees. Also, I have normalized data(according to the project specifications). For details you should look to the 'get_warped_images', 'get_noised_images' and 'normalize' functions.


#### 2. Model architecture.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x18 	|
| Batchnorm				|												|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x19 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x54	|
| Batchnorm				|												|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x54 					|
| Fully connected		| 												|
| Dropout				| 												|
| Fully connected		| 												|
| Softmax				| 												|
|						|												|
|						|												|
 


#### 3. Training process.

To train the model, I used an RMSPropOptimizer with 0.001 learning rate, 0.001 weight decay, and 0.7 momentum. Also, still I found and some unbalance in test set labels, I have balanced them by multiplying losses by their inverted testset ratio.  
I have used 30 epochs with 128 items per batch.

#### 4. Results.

My final model results were:
* training set accuracy of 0.997298772953
* validation set accuracy of 0.947
* test set accuracy of 0.939984164536

My architecture was like the Lenet  2 layers convolution network, with some modern adjustments like relu, dropout and batch-norm. I chose it cause it was simple, easy to check, and its original purpose was the same. The difference between these sets can be explained by the regularization technics that I have used, and by the difference in labels distribution in these sets.
 

### Test a Model on New Images


#### 1. Random signs.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]


#### 2. Real world predictions


Here are the results of the prediction:

| Image			        		|     Prediction	        					| 
|:-----------------------------:|:---------------------------------------------:| 
| Traffic lights   				| Speed limit (20km/h)							| 
| Road work    					| Road work										|
| No vehicles					| No vehicles									|
| Stop							| Stop					 						|
| Road narrows on the right		| Road narrows on the right						|



The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This less than validation set aacurasy, but cause we are using only 5 examples, we can't make any conclusions based on this results, we need them only to check the ability of model to work.

#### 3. Top5 probabilities

All 5 predictions(after softmax) of my model looks like this:
[ 1.,  0.,  0.,  0.,  0.]

![image9]


I think this means that model pretty sure in first option in all 5 cases(including the wrong one).


