
# Installation and Workspace Setup

Tested on Ubuntu 22.04 and ROS2 Humble.

## Step 1: Update System Packages
Ensure all packages are up-to-date by running the following commands:
```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install ROS2 Humble
Follow the official ROS2 Humble installation guide for your operating system:
[ROS2 Humble Installation Guide](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html)

## Step 3: Update rosdep
Initialize and update `rosdep` by running:
```bash
sudo rosdep init
rosdep update
```

## Step 4: Clone the Repository
Clone the repository with submodules by running:
```bash
git clone https://github.com/atarbabgei/ros2_audio_px4_ws.git --recursive
```

Navigate to the directory:
```bash
cd ros2_audio_ws
```

Update all dependencies:
```bash
rosdep install --from-paths src --ignore-src -r -y
```

## Step 5: Build the Workspace
Build the workspace with `colcon`. Ignore any stderr warnings as long as it works for now. Note that we override the default `ament_cmake` for `audio_common` modules to work.
```bash
colcon build --allow-overriding ament_cmake ament_cmake_auto ament_cmake_core ament_cmake_gmock ament_cmake_gtest ament_cmake_pytest ament_cmake_test
```

## Step 6: Source the Installation
After setting up the workspace, source the installation:
```bash
source install/setup.bash
```
