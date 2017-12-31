# Behavioral Cloning

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* Read_me_P3_Taketo_Kobayashi.md summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model uses Nvidia's Self-Driving Car Model Architecture.

* Layer 1: Convolutional Layer | 5x5 filter size, stride 2, relu nonlinearity activation
* Layer 2: Convolutional Layer | 5x5 filter size, stride 2, relu activation
* Layer 3: Convolutional Layer | 5x5 filter size, stride 2, relu activation
* Layer 4: Convolutional Layer | 3x3 filter size, relu activation
* Layer 5: Convolutional Layer | 3x3 filter size, relu activation
* Layer 6: Flatten Layer
* Layer 7: Fully Connected Layer size 100
* Layer 8: Dropout 0.5
* Layer 9: Fully Connected Layer size 50
* Layer10: Fully Connected Layer size 20
* Layer11: Fully Connected Layer size 10
* Layer12: Fully Connected Layer size 1

See (model2.py lines 45-60)


Data were preprocessed using the following steps:

1. The data were normalized in the model using a Keras lambda layer (code line 47).
2. The data were augmented by flipping the images to better balance the data (left and right)
3. Top of the images was copped to remove background and focus on the road lanes
4. Bottom of the was cropped to remove hood of the car and focus on the road lanes
5. Removed all 'zero' measurements from the dataset to drive better straight
6. Added a correction factor to the measurements to balance over/under steering

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.py lines 56).
Model was tested by running the simulator in autonomous mode and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 25).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road ...

For details about how I created the training data, see the next section.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the LeNet model. I thought this model might be appropriate as a starting model.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting.

To combat the overfitting, I modified the model so that I selected the Nvidia Convolutional Model and modified the LeNet architecture to match.

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track... to improve the driving behavior in these cases, I collected more data.

Here are training for data collection:

three laps of center lane driving
one lap of recovery driving from the sides

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...
* Layer 1: Convolutional Layer | 5x5 filter size, stride 2, relu nonlinearity activation
* Layer 2: Convolutional Layer | 5x5 filter size, stride 2, relu activation
* Layer 3: Convolutional Layer | 5x5 filter size, stride 2, relu activation
* Layer 4: Convolutional Layer | 3x3 filter size, relu activation
* Layer 5: Convolutional Layer | 3x3 filter size, relu activation
* Layer 6: Flatten Layer
* Layer 7: Fully Connected Layer size 100
* Layer 8: Dropout 0.5
* Layer 9: Fully Connected Layer size 50
* Layer10: Fully Connected Layer size 20
* Layer11: Fully Connected Layer size 10
* Layer12: Fully Connected Layer size 1

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Next I recorded driving counter clockwie because track one s has a left turn bias.Sample images can be found in the my zip file.

I finally randomly shuffled the data set and put 20% of the data into a validation set.
I used this training data for training the model. I ran the model for 5 epochs.
