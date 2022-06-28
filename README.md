# Traffic light detection

## Task

The task of detecting traffic lights is needed for self-driving cars or various driver assistance programs. In this task, it is important to detect traffic lights from the camera image, determine the color of the traffic light signal, and most importantly, determine whether each traffic light is relevant to the car.

Another limitation for the model is that the it should be able to process images or video in real time.

## Dataset

I used [DriveU Traffic Light Dataset](https://www.uni-ulm.de/en/in/driveu/projects/driveu-traffic-light-dataset/). Among the data labels, I left only traffic lights for drivers, deleting pedestrians and cyclists traffic lights. 
In addition, I left only traffic lights rotated front to driver and consisting of three segments. Finally, I removed the frames without relevant traffic lights from the training sample.

## Architecture

I take pre-trained FasterRCNN with ResNet-50 and train it for 10 epochs with lr_scheduler decreasing the learning rate by 10 times every 2 epochs. In addition, I do Non Maximum Suppression to get rid of overlapping bounding boxes.

For determining relevance of the traffic light I use heuristics of how the traffic light is located in the image. At least one condition must be fulfilled so that the traffic light is considered relevant to the car:

* 1/3 image width < traffic light location < 2/3 image width
* 1/3 image height < traffic light location < 2/3 image height

## Result

I achieve average FPS equal to 7.5, which means the model can process each 4th frame for a camera shooting 30 frames per second.

![Something went wrong :(](video/prediction_2_25s.gif)