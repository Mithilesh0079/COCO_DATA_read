# Object Detection

Requirements
------------
Tensorflow==1.15

To train new Model
---------------------
python3 train.py

To Detect the images
----------------------
python3 image_detect.py

Description
----------------------

1. Image Shape= (416,416,3). 

2. Formate of Bounding Boxes [Xmin, Ymin, Xmax, Ymax] that have been used.

3. No. of Training_data = 1980, No. of validation_data= 220.

4. Total 6 Anchors were Used: ((10,13), (16,30),(33,23),(30,61),(62,45),(59,119)).

Structure of data
------------------
The dataset used to train our deep CNN was of four classes (Bear, Elephant, Giraffe, Zebra), which were downloaded from COCO website with their corresponding bounding Boxes.
Total 2200 labelled images have been downloded with their respective boxes which were from COCO2017 Dataset.

Model training
--------------
We used ResNet-50 pretrained model on imagenet as a base model and then added some convolutional layers followed by prediction layer. There were total two prediction layers one was of (13,13) grid and another was of (26,26) grid. Toatal 6 anchors have been used, 3 for each prediction layers. We used Custom Loss function, which calculate the loss from these two predictions seperately and then add them to get total loss.
There were total 1980 images for training and 220 for validataion. While training the model, We frozen all the layers of ResNet-50 and trained our model for 30 epochs with batch_size=32, and learning rate= 0.0001 and after this We Unfrozen all the layers including ResNet-50 for training and trained our model for 20 epochs with decreasing learning rate(factor=0.1) starting from 0.0001 with batch_size= 8. 


Train/Validation_loss_curve
--------------------------
![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Train_validation_loss_curve.PNG)

Model_Architecture
------------------
![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Model.jpg)

Outputs
---------
![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Output/Bear/b1.PNG)
![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Output.PNG)
![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Output/Elephant/e3.PNG)

Loss Function
----------------------
The loss function composes of:

The classification loss.

The localization loss (errors between the predicted boundary box and the ground truth).

The confidence loss (the objectness of the box).

1.Classification Loss
----------------------
If an object is detected, the classification loss at each cell is the squared error of the class conditional probabilities for each class:

![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Loss_Functions/Classification_loss.PNG)

2.Localization loss
--------------------
The localization loss measures the errors in the predicted boundary box locations and sizes. We only count the box responsible for detecting the object.

![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Loss_Functions/Localization_loss.PNG)


3.Confidence loss
-------------------
If an object is detected in the box, the confidence loss (measuring the objectness of the box) is:

![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Loss_Functions/Confidence_loss.PNG)

If an object is not detected in the box, the confidence loss is:

![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Loss_Functions/confidence_loss1.PNG)

Total Loss
----------
The final loss adds localization, confidence and classification losses together.

![](https://github.com/neuratree/Object_Detection/blob/master/Mithilesh/Loss_Functions/Total_loss.PNG)

