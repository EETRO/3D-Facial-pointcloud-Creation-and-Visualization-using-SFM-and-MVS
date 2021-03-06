# 3D-Facial-pointcloud-Creation-and-Visualization-using-SFM-and-MVS
This repository contains code for creating and visualizing a sparse facial point cloud for 3D reconstruction purposes.
The intrinsic parameters have been customized for facial video capture on iPhone6S' front camera. 

Requirements in the Virtual environment
--------------------------------------------------
cycler==0.10.0
functools32==3.2.3.post2
matplotlib==2.0.2
numpy==1.13.3
opencv-contrib-python==3.3.0.10
pyparsing==2.2.0
python-dateutil==2.6.1
pytz==2017.2
scipy==1.0.0
six==1.11.0
subprocess32==3.2.7

Works on Python 2.7.* also

File descriptions
--------------------------------------------------
sfm_structure.py 
--------------------------------------------------
- Reads two frames 
	(The frames are to be chosen manually for these programs, however, choice of frames is programmable; should be done after surface recontruction to optimize this process.)
- Finds interest points using SIFT detector and a Brute Force Matcher
	(From commercial standpoint, ORB to be used)
- Ratio test to store the top matches
- Apply DLIB's Facial Landmark Detector 
- Initialize SFM pipeline
- K the intrinsic paramters compatible to iPhone 6S. Depending on the phone's version, this has to be taken care of. The requirement of the deliverable was for iPhone, hence the chosen paramters. 
- Triangulation to estimate pose
- Convert to non homogeneous points
- Export the 3D coordinates as a csv file 

--------------------------------------------------
background_sub.py
--------------------------------------------------
- Reads an image
- Gaussian blurring
- Edge detection
- Heirarchical Contour detection
- Background Subtraction

Note: After performing background subtraction, some contours can deliver black frames. To remove those frames from the directory that contains the video's frames, average energy of the frame should be calculated. If it is less than a threshold value, discard that frame. It is advised to make such a provision only after conducting a lot of experiments in different settings, illumination, etc. 

--------------------------------------------------
cannyedge.py
--------------------------------------------------
- Reads an image
- Uses OpenCV's Canny edge detection to output an edge map.


--------------------------------------------------
countframes.py
--------------------------------------------------
- helper python script to count frames
- embedded directly in other scripts
- given just for reference

--------------------------------------------------
facial_landmark.py
--------------------------------------------------
- Entire Facial Landmark detection pipeline
- takes trained model given as a .dat file 
- self-explanatory script


--------------------------------------------------
segmentation.py
--------------------------------------------------
- performs heirarchical contour detection based off of human faces
- imported in background_sub.py


--------------------------------------------------
sparse_cloud_using_vtk.py
--------------------------------------------------
-Uses Visualization Toolkit VTK Library for a good presentation of the point cloud. 

--------------------------------------------------
vid2frames.py
--------------------------------------------------
Takes a video as an input and outputs the frames


===================================================================================
Instructions for running the code:
1. Input video file to vid2frames script and give the directory for storing the output frames. 
2. Perform background subtraction on all the frames in the directory
3. In sfm_structure, choose the frames and get the output 3D points csv file
4ls
. On terminal, run python sparse_cloud_using_vtk.python test.csv 





