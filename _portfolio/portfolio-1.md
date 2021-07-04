---
title: "ROS2 Navigation"
excerpt: "Obstacle detection from 2D lidar data <br/><img class='resize' src='/images/nav2/least_squares_circle_fitting.png' alt='nav2_work'>"
collection: portfolio
---

This work — which is still ongoing — is for the [navigation2_dynamic](https://github.com/ros-planning/navigation2_dynamic) project, a part of the bigger [Navigation2 stack](https://navigation.ros.org/). I'm specifically developing the obstacle **detector** which takes 2D LIDAR scans as input and outputs positions of obstacles in the neighborhood, and also classifies them into *line*- and *circle*-obstacles (a wall is obviously a line, a car would be better represented by a circle).

This project is being led by [Steve Mackenski](https://www.linkedin.com/in/steve-macenski-41a985101/), the ROS Navigation Working Group Lead.

### Interested in seeing the code?
Head over to my [fork](https://github.com/abhishek47kashyap/navigation2_dynamic) and go into the  package `detection_2d_lidar`.

The `master` branch has my Python code which is mostly complete, but was found to not be fast enough for real-time operations (no surprises there!). So I'm presently porting all that to C++ in the `cpp_detector` branch.

## Description
For a mobile robot to make sense of its surroundings and act accordingly, it needs sensors like LIDAR to keep scanning its surroundings. 

*Shown below is a Turtlebot3 in a hexagonal room with 9 pillars:*
![lidar_scan](../../images/nav2/lidar_scan.png)

**Goal:** algorithmically determine from a LIDAR scan where the obstacles are, what are their approximate sizes, and whether they are *line* or *circle* obstacles.

### Obstacle detection pipeline
Every LIDAR scan provides a bunch of XYZ coordinates along with some more information. The coordinates are fed into the obstacle detection pipeline, which comprises of a series of operations:

1. **Grouping**: points are clustered based on proximity
2. **Splitting**: two separate obstacles might have been gotten clustered into one group
2. **Merging**: achieves the opposite effect of splitting
3. **Line / circle classification**: categorize all detected obstacles into lines and circles


![obstacle_detection](../../images/nav2/turtlebot_circles.gif)

On the left is the **Gazebo** simulation, and on the right is the **Rviz** visualization showing the *line* obstacles in <span style="color:red"> red </span> and *circle* obstacles in <span style="color:blue"> blue </span>, overlayed on top of the LIDAR scan (different colors to show the different groups).

## Further work
As can be clearly seen the "refresh rate" isn't that high. Analysis showed the *splitting* step of the detection pipeline is the bottleneck. This is the kind of thing Python is known to struggle with but hopefully should see some improvement using C++.

Check back later for updated results! 

---
**Testing**

So far all testing has been done in simulation. We are looking for companies or individuals who have actual robots and are willing to test this out.

If you're interested in helping out, please definitely drop me a line.

---
