---
title: Face Recognition
---
face recognition - ability to look at someone's face and "recognize" that person

*what are the uses of a service like this?*
- identify verification
- automatically organize raw photo libraries by person
- track specific person
- count unique people
- find people with similar appearance

recognizing face as a multi-step pipeline:
- locate and extract faces
- identify facial features
- align faces using pose (warp it to a template)
- represent face using measurements
- compare it to other faces

1. [[faceDetection|Face Detection]]
2. [[faceLandmarkEstimation|Face Landmark Estimation]]