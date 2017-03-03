# Nature...Or Not?
I've trained a convolutional neural network to discern between natural & and man-made structures in satellite images from around the globe (and extra-terrestrial globes).

## Table of Contents
[Motivation](#motivation)
[Dataset](#dataset)
[Pre-Processing](#pre-processing)
[Architecture](#architecture)
[Scores](#scores)
[Fun Tests!](#fun tests!)
[Next Steps](#next steps)


## Motivation
Viewing the world from above can give us an amazing and very different perspective on the changes going on in the world. We can monitor land use, reconnoiter areas of conflict, and survey natural disaster areas to find the best ways to bring in assistance...and, in the future, explore new planets for signs of life.

## Dataset
I gleaned 6,700 images from Googlemaps, manually and using the Google API with some scripting.  The images in my training and test sets come from around the world and contain a variety of natural settings, including forests, rivers, mountains, deserts, beaches, and ice and snow.

The original saved out images were quite large, 1152x864x3, which requires more memory than most GPUs can handle, so they were cut down to 124x124x3 using python's PIL library.

The labeling for these images was done by hand, labeled 0 for images containing only nature and 1 for images containing any man-made object. I've included plowed fields as man-made objects, as the patterns rendered by the plow are more closely related to other man-made objects than to that of nature. And technically, these shapes are man-made.

I was able to augment the 6,700 labeled images by taking the 90, 180, and 270 degree rotations of the image, as well as creating mirror images of these 4 rotations.  This created 8 total sets of usable data, for a total of 53,600 images.

## Pre-Processing
The feature (X) values in my dataset are the RGB values of the pixels.  Thus, X is a 124x124x3 array of RGB pixel values.

The data was broken into a Training and a Test set, consisting of 80% and 20% of the data, respectively.

Next, the RGB pixel values were normalized from 1-255 to 0-1 by dividing by 255, and centered around 0, by subtracting the mean of the X training data pixel values.  The mean pixel values for the R, G, & B components were consistent with each other, so the decision was made to use the mean of all 3 channels together to subtract from the data.

The labels (y) values also need some preperation before being fed into the neural net.  The labeled y data is read into the Python script as 1D array (vector) of 0's and 1's.  Keras, the neural networks library used, running on top of Theano for this network, required the labels to be converted to binary class matrices.<br>
    For example, the entry [0] becomes [1, 0] and the entry [1] becomes [0, 1]. 
    

## Architecture
The convolutional neural network (CNN) can learn that hard fixed lines and shapes, discerned from greater pixel differentiation, are more likely to be man-made objects, whereas images with less pixel differentiation, hence softer edges, are more likely to come from a natural setting. Brighter and more uniform colors are generally more likely to come from man-made objects. And very regular patterns, some that may be indiscernable to the human eye, are more likely to be manufactured by mankind.

Here's the CNN I've built to detect these features in my extracted images:


My final model contained:
<ul>
  3 Convolutional Layers

</ul>

Check Out Galvanize -->
