# Video Stabilization

<p align="center">
  <img src="media/VidStab.gif" width="700"/>
  <br>
<b>A stabilization result using the L1 optimal camera paths technique</b>
</p>

Methods Implemented:
1. **Averaging based method:** The first and simplest method considered is to simply smooth out the camera path using an averaging operation on the camera path. This asks like a low pass filter rejecting high frequency jitter.
2. **L1 Optimal Camera Paths:** This method uses a Linear Programming formulation to smoothen out the camera path. It is successful in removing low frequency movements in addition to the high frequency movement. 
3. **Subspace Video Stabilization:**: An optimization based approach. Under progress.
4. **Deep Video Stabilization**: Under Progress. A recent data driven deep learning based approach.  

Videographers make use of camera stabilization gimbals to prevent physical disturbances from deteriorating their recorded footage. However, these equipment are not perfect in the sense that low frequency disturbances from actions such as walking, running or rolling on bumpy surfaces are not filtered out by such stabilization hardware.
Due to these limitations of optical stabilization tools, and due to the fact that access to such tools is limited to professionals, software based video stabilization is desirable. 
In particular, our project, in collaboration with SysCon ARMS (Autonomous Robots and Multi-robot Systems) Lab at IIT Bombay, aims to stabilize the output video stream from a mobile spherical robot - [Picture of robot](https://www.sc.iitb.ac.in/embeddedLab.html).

The aim of the project is to compare the following strategies for video stabilization
1. Use of L1 optimal camera paths - Grundmann et al. 2011
2. Subspace video stabilization - Liu et al. 2011
3. Deep online video stabilization - Wang et al. 2018

The first two methods employ mathematical techniques to obtain camera trajectories from a cinematographically pleasing family of paths. These methods are completely unsupervised and do not have a training component to them. Both the algorithms are widely used and the L1 optimal path method has been employed in YouTube video stabilization. 
The third method describes a Deep Learning architecture - StabNet - That outputs a Homography matrix which is used to perform a transformation over an entire frame. It does so while by training the network with a loss that trades-off between stabilization from frame to frame, and temporal coherence.
We will be implementing the above three algorithms in python. The inputs to our system will be shaky, unprocessed videos and the outputs will be their stabilized versions. 
Initially we will be testing the efficacy of the methods on a standard video stabilization dataset and later on the output stream from the spherical robot.

### Relevant papers and prior work

[1] Auto directed video stabilization with Robust L1 optimal camera paths
https://smartech.gatech.edu/bitstream/handle/1853/44611/2011-Grundmann-AVSWROCP.pdf?sequence=1&isAllowed=y

[2] SubSpace video stabilization
https://dl.acm.org/doi/pdf/10.1145/1899404.1899408

[3] Deep Online Video Stabilization (CNN Based)
https://arxiv.org/abs/1802.08091

### Datasets
The dataset we would be working with initially is the SIGGRAPH 2013 video stabilization dataset.
http://liushuaicheng.org/SIGGRAPH2013/database.html
Later, if time (and the pandemic situation) permits, we would be evaluating our models on data collected from the ARMS lab spherical robot. 

### Extensions/modifications to the original paper

We plan to deliver the following novel contributions-
1. As mentioned in the problem statement we will be extending the understanding of the algorithms to solve the stabilization problem for a spherical robot where the camera undergoes wavy second-order damped motion.
2. The Deep Learning approach to this problem is quite recent and not much follow up work has been done. Based on our reading of the literature, we plan to add two things to the DL approach. Firstly, in [3], the StabNet architecture only takes historical frames as input to its model for the purpose of predicting a transformation as the output. The authors restrict themselves to prior frames only since they want their application to be online and real time. However, in our application we are willing to allow for a short delay between video recording and rendering and hence we would like to modify the architecture to include a window of frames into the future as well.
Secondly, a more ambitious extension to the reference [3] is to employ GANs to the video stabilization problem. [3] dismisses the use of generative networks on the stabilization problem since as per them there is “severe vibration” in the input video content. We are not quite convinced by this and would like to try for ourselves.

### Frameworks and Libraries
What framework/libraries will you be using for the project. Ex- tensorflow, pytorch, opencv, matlab libraries, etc.
We plan to stick to python in google colab for the deep learning parts of the project and 
Opencv - for data reading, augmentation, rendering etc.
Pytorch - for Deep Learning 
Python PuLP - As a linear programming solver in the implementation of [1]

### Link to existing code or non-trivial APIs

We have referred to the below links for implementation of reference:

[1] https://github.com/ishit/L1Stabilizer

[2] https://github.com/VAIBHAV-2303/VideoStabilization

### Evaluation Metrics

The metrics that we will be using are :
Cropping Ratio: i.e. area of the remaining content after stabilization
Distortion value: it  evaluates the distortion degree introduced by stabilization
Stability Score which uses frequency-domain analysis of camera path to estimate the stability
The computation time of each algorithm
Finally stabilization results on wavy second-order damped motion video.

### Systems and training regimes planned to be used

The total size of the SIGGRAPH 2013 data set is about 2 GB, as the first two algorithms do not require any training they can be either tested on our own systems i.e. laptops but to address the portability issues we will stick to Colab for the implementations of all 3 references. 
As per the training information presented in [3], the model should be trainable in about 10 hours of training on a version of the SIGGRAPH 2013 dataset.

### References

[1] Auto-Directed Video Stabilization with Robust L1 Optimal Camera Paths - Grundmann et al.

[2] Subspace video stabilization  - Liu et al.
