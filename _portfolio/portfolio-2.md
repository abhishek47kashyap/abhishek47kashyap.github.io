---
title: "Molcure: HAIVE robots"
excerpt: "Parallel robots for automating bio-tech experiments <br/><img class='resize' src='/images/molcure/haive_robots.png' alt='haive_robots'>"
collection: portfolio
---

Since all IP is owned by [Molcure Inc.](https://molcure.com/), I can only share limited information. That being said, we present at a number of exhibitions in and around Tokyo every year, and you're very welcome to stop by (I'll put up information on our next exhibition whenever I come to know of it).

---
Here's a fun clip from a few months ago when I was testing out an **IMU** (inertial measurement unit):

![imu_test](../../images/molcure/imu.gif)

---
Here's another clip when I was using **computer-vision** to detect [pipetting tips](https://images.app.goo.gl/8t1EvFER6j9X9goUA):

![circle_detection](../../images/molcure/circle_detection.gif)

## Software tech stack
Our tech stack has broadly 3 levels / layers:

1. **User interface (UI)**: allows creating biological experiments; converts user inputs to instructions that our robots can understand
2. **Robot Operation System (ROS)**: getting those instructions to the robots
3. **Firmware**: code that runs the robots

*I work in layers 2 and 3: ROS and firmware.*

### ROS
I'm the **primary developer** of this layer. My work is related to scheduling the send-out of instructions to the robots, and listening for any kind of response from the robots. Based on the response, appropriate actions are taken. This layer is the bridge between the higher software layers and the lowermost firmware layer.

### Firmware
I'm **one of the developers** of this layer. Since we build our own robots, there's quite a bit of work to do once the mechanical and electrical teams are done with assembling the robots. I work on implementing the various robot instructions, which sometimes requires synchronizing multiple microcontrollers to make different parts of the robot move concurrently.