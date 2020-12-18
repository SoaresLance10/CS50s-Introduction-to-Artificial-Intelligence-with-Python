# Traffic
Write an AI to identify which traffic sign appears in a photograph

As research continues in the development of self-driving cars, one of the key challenges is computer vision, allowing these cars to develop an understanding of their environment from digital images. In particular, this involves the ability to recognize and distinguish road signs – stop signs, speed limit signs, yield signs, and more.

In this project, you’ll use TensorFlow to build a neural network to classify road signs based on an image of those signs. To do so, you’ll need a labeled dataset: a collection of images that have already been categorized by the road sign represented in them.

Several such data sets exist, but for this project, we’ll use the German Traffic Sign Recognition Benchmark (GTSRB) dataset, which contains thousands of images of 43 different kinds of road signs.

The **specifications** for the project as mentioned at: https://cs50.harvard.edu/ai/2020/projects/4/traffic/
### Specification

Complete the implementation of **load_data** and **get_model** in traffic.py.

•	The **load_data** function should accept as an argument data_dir, representing the path to a directory where the data is stored, and return image arrays and labels for each image in the data set.
1. You may assume that data_dir will contain one directory named after each category, numbered 0 through NUM_CATEGORIES - 1. Inside each category directory will be some number of image files.
2. Use the OpenCV-Python module (cv2) to read each image as a numpy.ndarray (a numpy multidimensional array). To pass these images into a neural network, the images will need to be the same size, so be sure to resize each image to have width IMG_WIDTH and height IMG_HEIGHT.
3. The function should return a tuple (images, labels). images should be a list of all of the images in the data set, where each image is represented as a numpy.ndarray of the appropriate size. labels should be a list of integers, representing the category number for each of the corresponding images in the images list.
4. Your function should be platform-independent: that is to say, it should work regardless of operating system. Note that on macOS, the / character is used to separate path components, while the \ character is used on Windows. Use os.sep and os.path.join as needed instead of using your platform’s specific separator character.

•	The **get_model** function should return a compiled neural network model.
1. You may assume that the input to the neural network will be of the shape (IMG_WIDTH, IMG_HEIGHT, 3) (that is, an array representing an image of width IMG_WIDTH, height IMG_HEIGHT, and 3 values for each pixel for red, green, and blue).
2. The output layer of the neural network should have NUM_CATEGORIES units, one for each of the traffic sign categories.
3. The number of layers and the types of layers you include in between are up to you. You may wish to experiment with:
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	different numbers of convolutional and pooling layers
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	different numbers and sizes of filters for convolutional layers
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	different pool sizes for pooling layers
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	different numbers and sizes of hidden layers
<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•	dropout

•	In a separate file called README.md, document (in at least a paragraph or two) your experimentation process. What did you try? What worked well? What didn’t work well? What did you notice?

Ultimately, much of this project is about exploring documentation and investigating different options in cv2 and tensorflow and seeing what results you get when you try them!

# **Experimentation:**

Started with a base model using:

- 1 convolutional layer, learning 32 filters using a 3x3 kernel
- 1 max-pooling layer, using a 2x2 pool size
- Output layer with output units for all traffic sign categories

| **SR No.** | **Modification** | **Accuracy** |
| --- | --- | --- |
| 1 | Base model | 0.9344 |
| 2 | In base model, Changed Convolution Kernel to (5,5) | 0.9379 |
| 3 | To base model added 2nd Convolution layer | 0.9469 |
| 4 | In base model, Changed Pooling size to (5,5) | 0.9008 |
| 5 | To base model added 2nd Max-Pooling layer | 0.7009 |

After this testing I concluded that a model with 2 Convolution layers, learning 32 filters using (3x3) kernel and 1 Max-Pooling layer gave best results. Let&#39;s call this Model 2.

| **SR No.** | **Modification** | **Accuracy** |
| --- | --- | --- |
| 1 | Added Dropout of 0.2 to Model 2 | 0.9764 |
| 2 | Added 1 Hidden layer with 32 nodes per category | 0.9599 |
| 3 | Added Dropout of 0.2 to the hidden layer | 0.9779 |
| 4 | Added another Hidden layer with 16 nodes per category | 0.9634 |
| 5 | Added another hidden layer with 8 nodes per category | 0.9708 |

# **Final Results:**

Thus, a Model with: with 2 Convolution layers, learning 32 filters using (3x3) kernel, 1 Max-Pooling layer, dropout of 0.2 and Hidden layer with 32 nodes per category and dropout 0.2 gave best results.

However, The Final model: with 2 Convolution layers, learning 32 filters using (3x3) kernel, 1 Max-Pooling layer, dropout of 0.2, 1 Hidden layer with 32 nodes per category and dropout 0.2, 1 Hidden layer with 16 nodes per category and a last hidden layer with 8 nodes per category followed by an output layer with output units for each traffic label gave good results (Accuracy: 0.9708) and is well fitted to validate external data.

A video Demonstrating the Functionality of this Project and be found at: https://youtu.be/OVKCUJDmEXY
