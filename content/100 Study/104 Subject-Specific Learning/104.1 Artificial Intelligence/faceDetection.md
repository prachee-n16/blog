---
title: Face Detection
---

**face detection** - ability to detect and locate human faces in a photo
`STEP_1` check if face exists
- build a small model which just says if there is a face or not
`STEP_2` sliding window classifier
- go through parts of the photo and find the face

Face-detection algorithms
- Viola Jones - **Lowest accuracy**
	- decision trees to detect faces based on dark/light areas
- HOG *Histogram of oriented gradients*
	- looks for shifts from light to dark areas in an image
- CNN *Convolution Neural Networks - **Highest accuracy**
	- uses deep neural network (runs very slowly with slow hardware)

HOG algorithm (how to do this?)
- convert the input to b/w image
- check every pixel one at a time
	- find the surrounding pixels (vertical and horizontal) and find in which direction does the biggest change in color exists
	- movement of lighting basically
- okay maybe 16x16

How to train a face detection model with HOG?
1. collect training data
2. convert to HOG representation
3. train model classifier on HOG faces
4. slide window classifier on HOG faces
HOG isn't affected by lighting levels, or small changes in object



