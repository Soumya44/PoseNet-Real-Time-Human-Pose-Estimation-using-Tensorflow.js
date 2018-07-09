# PoseNet : Real-Time Human Pose Detection using Tensorflow.js


<img src="https://cdn-images-1.medium.com/max/1000/1*7qDyLpIT-3s4ylULsrnz8A.png" alt="keypoints" style="width: 600px;">

<h3><strong><em>PoseNet can be used to estimate either a single pose or multiple poses, meaning there is a version of the algorithm that can detect only one person in an image and one version that can detect multiple persons in an image.
</em></strong></h3>

## Installation

Clone this Repo and enter to the ```App```directory located inside the cloned directory using CMD/Terminal.

* **To Clone this Repo :**<br>
```$ git clone git@github.com:Soumya44/PoseNet-Real-Time-Human-Pose-Estimation-using-Tensorflow.js.git```

* **After getting inside the ```App``` directory, Run<br>**
```npm install``` <br>
This installs all the dependencies.

* **To run the model :**<br>
```npm run watch```

(Allow the Browser to use the Web Camera of your PC/Laptop)

## Usage

Either a single pose our multiple poses can be estimated from an image.
Each methodology has its own algorithm and set of parameters.

<strong><em>My documentation of the Single Pose Estimation Algorithm can be found <a href="https://drive.google.com/file/d/1kQQ39iKKdlk8oUG8XXDDI0Ylm8g1sElg/view?usp=sharing">here</a>.</em></strong>

### Keypoints

All keypoints are indexed by part id.  The parts and their ids are:

| Id | Part |
| -- | -- |
| 0 | nose |
| 1 | leftEye |
| 2 | rightEye |
| 3 | leftEar |
| 4 | rightEar |
| 5 | leftShoulder |
| 6 | rightShoulder |
| 7 | leftElbow |
| 8 | rightElbow |
| 9 | leftWrist |
| 10 | rightWrist |
| 11 | leftHip |
| 12 | rightHip |
| 13 | leftKnee |
| 14 | rightKnee |
| 15 | leftAnkle |
| 16 | rightAnkle |


### Single-Person Pose Estimation

Single pose estimation is the simpler and faster of the two algorithms. Its ideal use case is for when there is only one person in the image. The disadvantage is that if there are multiple persons in an image, keypoints from both persons will likely be estimated as being part of the same single pose—meaning, for example, that person #1’s left arm and person #2’s right knee might be conflated by the algorithm as belonging to the same pose. <br>
<strong><em><a href="https://drive.google.com/file/d/1kQQ39iKKdlk8oUG8XXDDI0Ylm8g1sElg/view?usp=sharing">Click here For the Detailed Algorithm</a></em></strong>


```javascript
const pose = await poseNet.estimateSinglePose(image, imageScaleFactor, flipHorizontal, outputStride);
```

#### Inputs

* **image** - ImageData|HTMLImageElement|HTMLCanvasElement|HTMLVideoElement
   The input image to feed through the network.
* **imageScaleFactor** - A number between 0.2 and 1.0. Defaults to 0.50.   What to scale the image by before feeding it through the network.  Set this number lower to scale down the image and increase the speed when feeding through the network at the cost of accuracy.
* **flipHorizontal** - Defaults to false.  If the poses should be flipped/mirrored  horizontally.  This should be set to true for videos where the video is by default flipped horizontally (i.e. a webcam), and you want the poses to be returned in the proper orientation.
* **outputStride** - the desired stride for the outputs when feeding the image through the model.  Must be 32, 16, 8.  Defaults to 16.  The higher the number, the faster the performance but slower the accuracy, and visa versa.

#### Returns

It returns a `pose` with a confidence score and an array of keypoints indexed by part id, each with a score and position.



### Multi-Person Pose Estimation

Multiple Pose estimation can decode multiple poses in an image. It is more complex and slightly slower than the single pose-algorithm, but has the advantage that if multiple people appear in an image, their detected keypoints are less likely to be associated with the wrong pose. Even if the use case is to detect a single person’s pose, this algorithm may be more desirable in that the accidental effect of two poses being joined together won’t occur when multiple people appear in the image. It uses the `Fast greedy decoding` algorithm from the research paper [PersonLab: Person Pose Estimation and Instance Segmentation with a Bottom-Up, Part-Based, Geometric Embedding Model](https://arxiv.org/pdf/1803.08225.pdf).

```javascript
const poses = await net.estimateMultiplePoses(image, imageScaleFactor, flipHorizontal, outputStride, maxPoseDetections, scoreThreshold, nmsRadius);
```

#### Inputs

* **image** - ImageData|HTMLImageElement|HTMLCanvasElement|HTMLVideoElement
   The input image to feed through the network.
* **imageScaleFactor** - A number between 0.2 and 1.0. Defaults to 0.50.   What to scale the image by before feeding it through the network.  Set this number lower to scale down the image and increase the speed when feeding through the network at the cost of accuracy.
* **flipHorizontal** - Defaults to false.  If the poses should be flipped/mirrored  horizontally.  This should be set to true for videos where the video is by default flipped horizontally (i.e. a webcam), and you want the poses to be returned in the proper orientation.
* **outputStride** - the desired stride for the outputs when feeding the image through the model.  Must be 32, 16, 8.  Defaults to 16.  The higher the number, the faster the performance but slower the accuracy, and visa versa.
* **maxPoseDetections** (optional) - the maximum number of poses to detect. Defaults to 5.
* **scoreThreshold** (optional) - Only return instance detections that have root part score greater or equal to this value. Defaults to 0.5.
* **nmsRadius** (optional) - Non-maximum suppression part distance. It needs to be strictly positive. Two parts suppress each other if they are less than `nmsRadius` pixels away. Defaults to 20.

#### Returns

It returns a `promise` that resolves with an array of `poses`, each with a confidence score and an array of `keypoints` indexed by part id, each with a score and position.

### Credits
* <a href="https://www.linkedin.com/in/prashant-devadiga-84a05612/">Mr. Prashant Devadiga</a> (AVP - Reliance Industries Limited)<br>
* <a href="https://www.linkedin.com/in/manjusha-mishra-a15648125/">Manjusha Mishra</a><br>
and others.

<br><strong><em>Special Thanks to <a href="http://www.ril.com/">Reliance Industries Limited</a> for this Opportunity.</em></strong>

### Let's Get Connected
* <strong>E-mail</strong> : contact@soumyatechzone.app <br>
* <strong>LinkedIn</strong> : https://www.linkedin.com/in/soumya-ranjan-behera-989a2a151/

### References
* <a href="https://medium.com/tensorflow/real-time-human-pose-estimation-in-the-browser-with-tensorflow-js-7dd0bc881cd5">Real-time Human Pose Estimation in the Browser with TensorFlow.js</a><br>
* <a href="https://github.com/tensorflow/tfjs-models/tree/master/posenet"> Official Tensorflow.js PoseNet Implementation</a><br>
* <a href="https://storage.googleapis.com/tfjs-models/demos/posenet/camera.html">Official Demo of PoseNet</a><br>
* <a href="https://js.tensorflow.org/">Tensorflow.js</a>
