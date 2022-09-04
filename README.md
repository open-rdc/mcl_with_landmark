# mcl_with_landmark

## Requirement
theta_simple_stitching  
branch: melodic-devel  
https://github.com/open-rdc/theta_simple_stitching  

yolov5_pytorch_ros  
branch: detect_landmark  
https://github.com/open-rdc/yolov5_pytorch_ros  

yolo_to_landmarks  
branch: main  
https://github.com/open-rdc/yolo_to_landmark  

emcl  
branch: mcl_with_landmark  
https://github.com/open-rdc/emcl  

orne_navigation  
https://github.com/open-rdc/orne_navigation  
branch: emcl_with_landmark  

## Execute
for Ubuntu1804

### Execute roscore on docker
1) `docker run -it --net host --name roscore ros:melodic`

### Capture images from Theta
2) Launch Theta in Live mode
Press the power and camera buttons to start

3) Change the authority
`sudo chmod 666 /dev/bus/usb/001/*`
4) `roslaunch theta_simple_stitching theta.launch`
5) Launch rviz
6) Select `/image/mercator/Image` to display the image

### Execute yolo5_pytorch_ros
```
cd ~/catkin_ws/src/yolov5_pytorch_ros/docker
docker-compose up -d
docker exec -it yolo bash
```
```
mkdir -p catkin_ws/src
cd catkin_ws/src
catkin_init_workspace
git clone https://github.com/open-rdc/yolov5_pytorch_ros
cd ..
catkin_make
source ~/catkin_ws/devel/setup.bash
roslaunch yolov5_pytorch_ros landmark_detector.launch
```

7) Select `/detections_image_topic/Image` to display the image on rviz

8) rosrun yolo_to_landmark yolo_to_landmark.py

### simulator
9) roslaunch orne_bringup orne_alpha_sim.launch

10) roslaunch orne_navigation_executor nav_static_map.launch emcl:=true
