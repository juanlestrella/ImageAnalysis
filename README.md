Introduction:

For my final project I choose to work on a challenge I found in zindi.africa titled "Local Ocean Conversation - Sea Turtle Face Detection." This challenge is created by the organization Local Ocean Conversation (LOC), a not-for-profit committed to protect Kenya's marine environment. LOC's mission is to develop sustainable marine resource management models that utilize sea turtles as flagship species for Kenya's ocean health. For this specific challenge, LOC wants to use the unique fingerprint of tutle's faces to integrate facial image recognication. In order to do this, an algorithm is required to take an image of a sea turtle and output the position of a bounding box around all-important scale pattern.

The Sea Turtle Face Detection challenge provided a csv file called Train.csv. This csv file contains the list of image id and bounding box annotations. The bounding boxes are defined by four numbers: x, y, w (width), and h (height). These are float numbers representing the fractions of the image dimensions in pixels. In addition, the challenge provides two zip files, IMAGES_1024 and IMAGES_512, which contains different pixel version of the images. Finally, we are also provided by a starter notebook to help show how to convert the pixel locations to the input image size and some other functionality that might be useful in developing the algorithm.

Methods:

In order to implement this algorithm, I decided to use a supervised segmentation called active contour. This segmentation method is used to fit a snake on objects to outline its shape. In order to use active contour, we first need to initialize the snake. Since the challenge provided us with a bounding box, we can use this box to create a circle around the turtle's head. We cannot use the coordinates of the bounding box since the coordinates required for the snake is polar coordinate. In order to generate an array that contains the circle, I used the function circle_points provided by in lecture 14. This function requires three arguments: resolution, center, and radius. The resolution is a allows 200, this is not a good general number of points to give for all the images as each images contains different shape of the bounding box. The center is calculated by finding the middle point from two of the diagonal corners' coordinate from the bounding box. The radius is computed by the distance between the center point and one of the bounding box's corners.

Results

The result of the active contour method on each of the images varies. Mostly, the snake does not fit the turtle's head because the background and the turtle's head does not have a good contrast. This can be improved by having a plain one colored background when the images are taken. Moreover, using the dataframe generated from Train.csv, I inserted four more columns in the dataframe:

resolution: points for the snake (all 200)
center: the center of the provided bounding box
radius: the radius of the circle covering the turtles' head
points: array result from circle_points function
Lastly, I generated a simple histogram using matplotlib in order to show the radius used for the circle_points function. The radius indicates the maximum radius of each turtle's head. This shows how far or close the images are usually photographed.

Discussion

The result from active contour could definitely be improved. For example, another user who participated in the challenge used libraries like segmentation_models_pytorch and albumentations to develop an algorithm for this challenge. The result could also be used to generate random forest regression or convolutional neural network to predict how well the algorithm works on detecting turtle's face.
