- finding key points in a face like corners of the eye, upper part of mouth
- each point we find in a face that's important is called a "face landmark"
- we start with the set of points we expect to find and then move it around until we find a match for it

We can do this easily with a few tricks
1. Assume all faces are similar
	1. just overlay the points on top of the picture, and then shift it around till it matches the features
2. Limit the movement such that it can not go past it's neighbouring points
3. Train several ML models that do like part of the job

Face alignment - adjusting a raw face image so that key features line up with the template

Affine transformation - linear mapping between sets of points where parallel lines remain parallel.