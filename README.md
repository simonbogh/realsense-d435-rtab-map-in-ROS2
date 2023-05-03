# Intel RealSense D435 and rtab_map with ROS2

This guide will help you use the Intel RealSense D435 camera in ROS2 and visualize the RGB and depth point cloud in RViz2. It also covers using RTAB-Map for mapping and localization with the Intel RealSense D435 camera.

## Prerequisites

You need to have the following packages installed:

```bash
sudo apt install ros-foxy-realsense2-camera
sudo apt install ros-foxy-rtabmap-ros
```

## Usage

1. Launch the camera node by running the following command:

```bash
ros2 launch realsense2_camera rs_launch.py align_depth.enable:=true pointcloud.enable:=true
```

2. Start mapping the environment using RTAB-Map with the command below:

```bash
ros2 launch rtabmap_ros rtabmap.launch.py \
 args:="--delete_db_on_start" \
 depth_topic:=/camera/aligned_depth_to_color/image_raw \
 rgb_topic:=/camera/color/image_raw \
 camera_info_topic:=/camera/color/camera_info \
 approx_sync:=false \
 frame_id:=camera_link
```

3. Launch RViz2:

```bash
rviz2
```

4. Load the RViz configuration file provided in the repository:

- In RViz2, click on "File" in the top left corner.
- Select "Open Config".
- Navigate to the location of the RViz configuration file saved in the repository and open it.

The configuration file will automatically set up RViz2 to display the RGB and depth point cloud from the Intel RealSense D435 camera.

Now you should see the RGB and depth point cloud being visualized in RViz2.

## About RTAB-Map

RTAB-Map (Real-Time Appearance-Based Mapping) is a RGB-D Graph SLAM approach based on an incremental appearance-based loop closure detector. It is designed to be a generic approach applicable to indoor and outdoor environments. For more information, visit the [RTAB-Map website](http://introlab.github.io/rtabmap/).

For ROS1 examples and tutorials, visit the [RTAB-Map ROS Wiki page](http://wiki.ros.org/rtabmap_ros/Tutorials/HandHeldMapping).

## Troubleshooting

If you encounter issues with RViz2, make sure that you have the correct topics and frame_id set in the configuration file. Verify that the topics `/camera/aligned_depth_to_color/image_raw`, `/camera/color/image_raw`, and `/camera/color/camera_info` are properly set and that the frame_id is set to `camera_link`.

## Support

If you need further assistance, feel free to open an issue on this repository or consult the ROS2 and Intel RealSense communities for more information.

