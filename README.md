# RTAB-Map




```
roscore
cd catkin_ws/src/rtab_map_ksa/src
rosbag play robotic_class.bag robotic_class_essentials.bag --clock

rosrun tf static_transform_publisher 0.15 0.0 0.24 1.570796 3.1415 1.570796 base_link camera_center_imu_optical_frame 100

rosrun tf static_transform_publisher 0.15 0.0 0.24 1.570796 3.1415 1.570796 base_link camera_center_color_optical_frame 100

```

For camera_link:
```
rosrun tf static_transform_publisher 0.15 0.0 0.24 1.570796 3.1415 1.570796 camera_link camera_center_imu_optical_frame 100
rosrun tf static_transform_publisher 0.15 0.0 0.24 1.570796 3.1415 1.570796 camera_link camera_center_color_optical_frame 100


```

```
rosrun imu_filter_madgwick imu_filter_node _use_mag:=false _publish_tf:=false _world_frame:="enu" /imu/data_raw:=/terrasentia/camera_center/imu /imu/data:=/rtabmap/imu

rosrun image_transport republish compressed in:=/terrasentia/camera_center/color/image_raw raw out:=/z/foo/
```

```
roslaunch rtabmap_ros rtabmap.launch \
 rtabmap_args:="--delete_db_on_start --Optimizer/GravitySigma 0.3" \ depth_topic:=/terrasentia/camera_center/aligned_depth_to_color/image_raw \
 rgb_topic:=/z/foo \
 camera_info_topic:=/terrasentia/camera_center/color/camera_info \
 use_sim_time:=True \
 approx_sync:=False \
 wait_imu_to_init:=True \
 imu_topic:=/rtabmap/imu
 
```
