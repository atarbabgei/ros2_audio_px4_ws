
# Installation and Workspace Setup

Tested on Ubuntu 22.04 and ROS2 Humble.

## Step 1: Update System Packages
Ensure all packages are up-to-date by running the following commands:
```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install ROS2 Humble (If you haven't installed ROS2)
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
cd ros2_audio_px4_ws
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

## Example Usage for Audio Common

Refer to the usage of ROS audio_common in the main repository: [ROS Audio Common](https://github.com/ros-drivers/audio_common)

For example, to capture audio and publish it to ROS2 topics, make sure to source your workspace installation:
```bash
source ~/ros2_audio_px4_ws/install/setup.bash 
```
Then launch the audio capture package:
```bash
ros2 launch audio_capture capture.launch.py format:=wave device:="hw:1,0" channels:=1 sample_rate:=48000
```
Change the device hw:1,0, sample rate, or other parameters depending on your microphone setting.

To verify the audio is working, open a new terminal:
```bash
source ~/ros2_audio_px4_ws/install/setup.bash
```

Check if the topics are available:
```bash
ros2 topic list
```
you should be able to see something like these:
```bash
/audio/audio
/audio/audio_info
/audio/audio_stamped
```

If they are available, launch the audio player package:
```bash
ros2 launch audio_play play.launch.py format:=wave channels:=1 sample_rate:=48000
```

You should be able to listen the sound from the audio topics.
