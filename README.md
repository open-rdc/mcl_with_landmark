# mcl_with_landmark

## Requirement
theta_simple_stitching  
https://github.com/open-rdc/theta_simple_stitching  
yolov5_pytorch_ros  
https://github.com/open-rdc/yolov5_pytorch_ros  
emcl  
https://github.com/open-rdc/emcl  

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

### Example
7) Select `/detections_image_topic/Image` to display the image on rviz
