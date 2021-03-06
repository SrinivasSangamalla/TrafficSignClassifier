**Project: Build a Traffic Sign Recognition Program**

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

Udacity - Self-Driving Car NanoDegree

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/SrinivasSangamalla/TrafficSignClassifier)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32, 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

The exploration of the data was done by randomly showing pictures from each of the 3 sets. You can 
see this in the 3rd cell of the jupyter notebook.

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because for this exercise, the color of the signs does not make a difference. There is no
point loading the training data with features of colors that are not needed.

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image1]


As a last step, I normalized the image data because normalized data works well with the gradient descent algorithm

No further augmentation of the data was done


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 Grayscale image   							| 
| Convolution 3x3     	| 1x1 stride, same padding, outputs 32x32x64 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 16x16x64 				|
| Convolution 3x3	    | etc.      									|
| Fully connected		| etc.        									|
| Softmax				| etc.        									|
|						|												|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used:

EPOCHS = 90
BATCH_SIZE = 128

and a learning rate of: rate = 0.002

This took the biggest amount of time and I had to fiddle with these parameters quite a lot until I got the training to give 93% accurace

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.999
* validation set accuracy of 0.941
* test set accuracy of 0.922

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image9] ![alt text][image10] ![alt text][image11] 
![alt text][image12] ![alt text][image13]


Some of these images might be harder to classify because they are "printed" images and not photos taken from a car. 
Since the data set is pictures of traffic signs, it might be difficult for the classifier to to classify my images

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed Limit 50      		| Speed Limit 30   							| 
| Stop     					| Stop										|
| Priority Road				| Priority Road								|
| Speed Limit 30	      	| Speed Limit 30					 		|
| Speed Limit 60			| Speed Limit 50      						|


The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. 

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, things are a bit weird actually - it thinks it's a roundabout. This is probably do the image being too clean
['Roundabout mandatory(66.0)', 'Speed limit (80km/h)(27.0)', 'General caution(-9.0)', 'Speed limit (50km/h)(-17.0)', 'Right-of-way at the next intersection(-29.0)']

For the second image, the prediction that is a Stop Sign is correct:
['Stop(67.0)', 'Speed limit (120km/h)(18.0)', 'Speed limit (70km/h)(18.0)', 'Double curve(6.0)', 'Priority road(1.0)']

Third image (Priority road) is also correct:
['Priority road(89.0)', 'Children crossing(27.0)', 'No vehicles(12.0)', 'Keep right(7.0)', 'Roundabout mandatory(-7.0)']

Fourth Image is also correct (30 km /hr)
['Speed limit (30km/h)(171.0)', 'Speed limit (50km/h)(63.0)', 'Speed limit (100km/h)(62.0)', 'Keep right(57.0)', 'Speed limit (80km/h)(27.0)']

Fifth image is wrong - it says 60 km /hr, but it thinks it's 50
['Speed limit (30km/h)(147.0)', 'Speed limit (50km/h)(81.0)', 'Keep right(56.0)', 'Keep left(19.0)', 'Speed limit (100km/h)(16.0)'] 