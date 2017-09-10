# **Finding Lane Lines on the Road**

[//]: # (Image References)
[greyScale]: ./examples/greyScale.jpg "Grayscale"
[edges]: ./examples/edges.jpg "Edges"
[lineEdges]: ./examples/lineEdges.jpg "Line Edges"
[lineImage]: ./examples/lineImage.jpg "Line Image"
[maskedEdges]: ./examples/maskedEdges.jpg "Masked Edges"

---

## Methodology

The lane detection pipeline consists of five steps:
### 1. Convert the image to grey scale

![alt text][greyScale]
### 2. Use Canny edge detection to create a new image in which edges are highlighted

![alt text][edges]
### 3. Apply an image mask in order to focus on the portion of the image where lanes could exist

![alt text][maskedEdges]
### 4. Determine Hough Lines based on image mask and draw lines onto blank image

![alt text][lineImage]
### 5. Draw the lines onto the original image

![alt text][lineEdges]

## Reflection

Initially, this pipeline only showed lines that exist in the actual image. For example,
a dashed line on the road would appear as multiple dashes instead of a single lane line.
In order to create the full lane line, I separated lines into "left" and "right" lane lines
and calculated their average coordinates and slopes. I then used this values to determine a
"line of best fit" for all the Hough lines. Since a video is just a sequence of images, I
was able to process each frame in the video using this updated technique to generate the
"full lane detection" video at the bottom of the notebook.

I'd like to acknowledge this model has one major shortcoming: it is highly dependent on the size and
perspective of the image. If the image size were to change significantly or if the camera were to
zoom in, zoom out, or otherwise change perspective, this model would break. A possible improvement
would be to leverage a convolutional neural network (CNN) instead of using Canny edge detection
in conjunction with a mask. CNNs are able to classify image types from various perspectives and
in any location within an image, making them an excellent candidate for making the pipeline less
brittle.
