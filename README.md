# Knee-Bend-Estimation

Estimated rep count for knee bend exercise. Applied mediapipe library for the detection of the human body landmarks. Added a holding timer limit of 8 seconds. Rep will be counted only when the knee is bended at least for 8 seconds. Included feedback message , which should be triggered only when a person's knee is bended at particular angle & for specific time. The threshold angle considered for the knee bend is 140 degree.
Implemented it on <a href="https://drive.google.com/file/d/1YZRtvpR5PpTXr_nFc5SboIO7RMXLB9Hx/view?usp=share_link">Input Video</a>. 

With the help of mediapipe library got the coordinates of the hip, knee and ankle. Used the below code for the same.

```python

left_hip = [landmarks[mp_pose.PoseLandmark.LEFT_HIP.value].x,landmarks[mp_pose.PoseLandmark.LEFT_HIP.value].y]
left_knee = [landmarks[mp_pose.PoseLandmark.LEFT_KNEE.value].x,landmarks[mp_pose.PoseLandmark.LEFT_KNEE.value].y]
left_ankle = [landmarks[mp_pose.PoseLandmark.LEFT_ANKLE.value].x,landmarks[mp_pose.PoseLandmark.LEFT_ANKLE.value].y]

```
To calulate the angle considered the coordinates of the hip, knee and ankle as an input 

```python

def calculateAngle(a,b,c):
    a = np.array(a) # First
    b = np.array(b) # Mid
    c = np.array(c) # End
    
    radians = np.arctan2(c[1]-b[1], c[0]-b[0]) - np.arctan2(a[1]-b[1], a[0]-b[0])
    angle = np.abs(radians*180.0/np.pi)
    
    if angle >180.0:
        angle = 360-angle
        
    return angle 

```
And to download the output video used videowrite function of cv2 library

```python
video_writer = cv2.VideoWriter(('output.mp4'), cv2.VideoWriter_fourcc(*'XVID'), fps, (w, h))
```
Snapshots of Input Video:

![image](https://user-images.githubusercontent.com/54770758/216779631-feb6be7c-21ba-4ac3-948d-dbc303412899.png)

![image](https://user-images.githubusercontent.com/54770758/216779679-9c3d39c7-03c9-419e-a0fe-791f7a782b1b.png)

Snapshots of the Output Video:

![image](https://user-images.githubusercontent.com/54770758/216779760-2f010880-d641-4cbe-8969-51b7acc42a17.png)

![image](https://user-images.githubusercontent.com/54770758/216779804-66511180-0415-410a-a46b-e1a916fb1bd7.png)

View Full Output video <a href="https://drive.google.com/file/d/1VZ4VDdwEjFsknLYbc8lZFC9a-384GAD-/view?usp=share_link">here</a> .


# **References**

1. https://www.youtube.com/watch?v=06TE_U21FK4&t=2756s
2. https://google.github.io/mediapipe/solutions/pose.html

