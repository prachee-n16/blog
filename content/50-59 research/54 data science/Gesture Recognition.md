
Hand gesture recognition is challenging because 
	  (1) no easy way to know when a gesture starts and ends
	  (2) we need to recognize a gesture once
	  (3) model needs to be memory and power efficient
	  
This [paper](https://arxiv.org/pdf/1901.10323v3) proposes an offline-working (i.e. no internet connection needed) convolutional neural network using sliding window approach. 
- The architecture has two models
	- Detector: lightweight CNN architecture to detect hand gestures
	- Classifier: Deep CNN to classify detected gestures
- Since we want to evaluate the single-time activations of detected hand gestures, we want to use Levenshtein distance (measures misclassifications, multiple detections, and missing detections)
- gesture recognition can be practiced with: 
  (i) glove-based wearable devices - requires additional hardware 
  (ii) 3-D locations of hand keypoints - extra step of hand keypoints extraction
  (iii) raw visual data - most optimal method

- real-time gesture recognition applications need to satisfy 
	- fast reaction time
	- acceptable classification accuracy
	- resource efficiency
	- single-time activation per gesture
- This system has a classifier i.e. offline-trained deep 3D CNN for gesture classification and detector i.e. light weight, shallow 3D CNN for gesture detection
	- Classifier only becomes active when the detector has detected a hand gesture (saves memory and power)
	- Early detection thresholds exist because scores of similar classes become high at same time
- Evaluation metric: [[Levenshtein distance]] "... measure misclassifications, multiple detections and missing detections at the same time"
Related: [[Convolutional neural network]]

From [Developer's Google Guide on MediaPipe](https://developers.google.com/mediapipe/solutions/vision/gesture_recognizer),
With MediaPipe Gesture Recognizer,
- Recognize hand gestures in real time
- Provide landmarks of the detected hands (21 key points that it tracks)
- Handedness - which hand is being used to make gesture? This provides more options for keybinds.

There are two model bundles - Hand Landmark and Gesture Classification.

 Hand Landmark model has both, palm detection and hand landmarks detection. 
 - Palm detection will localize the region of hands from input image.
 - Hand landmark finds landmarks on localized region and marks them

With gesture classification, it can recognize 7 common hand gestures. This can serve as a default keybind option. So, when the app opens, these 7 will be a pre-set selection but users should still have the ability to enter a custom gesture. 

How does it do it?
- Encode the image features into a feature vector to feed into the model
- Lightweight gesture classifier i.e. classification model will classify it into predefined categories
