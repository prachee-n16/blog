There are three main types of layers: (1) Convolutional layer, (2) Pooling layer and (3) Fully-connected layer 

**Convolutional Layer**
Requires *input data*, *filter* and *feature map*.
- Input data: e.g. color image which is a matrix of pixels in 3D (corresponds to RGB in image)
- Feature detector; kernel or filter: Perform convolution i.e. moves across the receptive fields of an image and check if a feature is present
	i.e. receptive field: region of the input image that a neuron in network layer sees
	- feature detector is a 2-D array of weights which represents part of an image
		- typically, this is a 3x3 matrix; filter is applied to an area of the image 
		- dot product is calculated between input pixels and filter; this is fed into an output array
		- filter shifts by a stride, repeating until entire image has been considered
		- final output from series of dot products from input and filter = feature map (or activation map; convolved feature)
Related: [[Neural Network]]
