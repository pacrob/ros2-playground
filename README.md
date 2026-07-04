# ros2-playground

A place to learn the basics of ROS 2 and C++.

## Overview

This is a ROS 2 (Humble) workspace containing a single package, `ros2_learn_pkg`,
built with `ament_cmake`.

The package provides one node:

- **`publisher`** (`hello_world_pub_node`) — publishes a `std_msgs/msg/String`
  message on the `hello_world` topic once per second. Each message contains the
  text `"Hello World<N>"`, where `N` is an incrementing counter.

Source: [src/ros2_learn_pkg/src/publisher.cpp](src/ros2_learn_pkg/src/publisher.cpp)

## Prerequisites

- ROS 2 Humble installed at `/opt/ros/humble`
- `colcon` build tooling

Source the ROS 2 environment in every new shell before building or running:

```bash
source /opt/ros/humble/setup.bash
```

## Build

From the workspace root (`ros2-playground/`):

```bash
colcon build
```

To build only this package:

```bash
colcon build --packages-select ros2_learn_pkg
```

## Run

After building, source the workspace overlay, then run the node:

```bash
source install/setup.bash
ros2 run ros2_learn_pkg publisher
```

The node runs continuously, publishing one message per second. Stop it with
`Ctrl+C`.

## View the output

Open a **second terminal** (source ROS 2 and the workspace overlay there too),
then use the ROS 2 CLI to inspect the topic:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

Echo the messages as they are published:

```bash
ros2 topic echo /hello_world
```

Other useful inspection commands:

```bash
ros2 topic list                # list active topics
ros2 topic info /hello_world   # show message type and pub/sub counts
ros2 topic hz /hello_world     # measure publishing rate (~1 Hz)
ros2 node list                 # list running nodes
ros2 node info /hello_world_pub_node
```
