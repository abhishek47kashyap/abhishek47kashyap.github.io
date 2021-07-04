---
title: "Stewart platform - inverted"
excerpt: "Keeping top plate steady by rejecting disturbances to base <br/><img class='resize' src='/images/stewart_platform/simulink_stewart_platform.png' alt='simulink_stewart_platform'>"
collection: portfolio
---

This was a semester project for the course Robot Controls when I was at WPI. The project was inspired by a well-known YouTube video of a self-levelling pool table on a cruise ship. Even though the floor that the pool table on is gently rocking, the pool *table top* is steady enough that the balls don't get displaced.

[![self_levelling_pool_table](http://img.youtube.com/vi/N-aE5oszXyQ/0.jpg)](http://www.youtube.com/watch?v=N-aE5oszXyQ)


## Stewart Platform
A traditional Stewart Platform has its base plate fixed while the top plate is moved (translated and/or rotated) by altering the length of one or more of its 6 legs.

![traditional_stewart_platform](https://upload.wikimedia.org/wikipedia/commons/a/a7/Hexapod_general_Anim.gif)

How inverting the concept: **regardless of how the base plate moves, the top plate should be steady**. After all, that's how the self-levelling pool table looks like.


The work was done in simulation only (semester ended too quickly), using [MATLAB's Stewart Platform](https://www.mathworks.com/help/physmod/sm/ug/stewart-platform.html) as the testbed. We stripped off what we didn't need (as fancy the trident is, that had to go) and made modifications to the underlying controller. I had two wonderful teammates to work with.

## Getting technical
Consider 3 frames:

1. `world`: the parent frame with respect to which everything else is defined
2. `base`: frame attached to center of the base plate
3. `top`: frame attached to center of the top plate

In the context of the pool table, table surface would be `top`, and the floor would be `base`.

![reference_frames](../../images/stewart_platform/simulink_stewart_platform.png)

Generally, `base` is fixed with respect to `world`, and `top` moves. But if we want to enjoy a good game of pool, `top` mustn't move.

More concretely, `top` must not be subjected to any *roll* or *pitch* motions. **If the ship has almost-zero acceleration, translation and yaw rotation should not have any effect.** Why: think of Newton's 1st law of motion and the friction between the balls and the table surface.

Now that we have shrunk the problem from 6-DOF to 2-DOF, in that all we need to worry about are *roll* and *pitch*, the objective now becomes: **Z axis of `top` should always be along the gravity vector**.

And that's the problem we solved:

![top_plate_no_rotations](../../images/stewart_platform/top_plate_no_rotations.gif)

Or did we? If this was a pool table, all balls would surely be rolling all over the table surface. However, think back to the requirement established previously: **almost-zero acceleration**. In the gif above extreme accelerations are used to prove the point that the top plate doesn't *roll* or *pitch*, no matter how the base plate moves. In reality, this would be happending in **super slow motion**.

### Let's dive deeper ..

The rotation matrix of `top` with respect to `world` should ideally be an identity matrix.

For this work, base plate disturbance was modelled as a sine wave: 

![formula](https://render.githubusercontent.com/render/math?math=D(t) = 0.15sin(t))

Amplitude was chosen as ![formula](https://render.githubusercontent.com/render/math?math=0.15) but the PID controller can handle any amplitude in the range ![formula](https://render.githubusercontent.com/render/math?math=[-0.25,0.25]). Frequency &omega; was set to ![formula](https://render.githubusercontent.com/render/math?math=1) rad/sec.

To find out if *roll* and *pitch* were maintained at ![formula](https://render.githubusercontent.com/render/math?math=0), let's examine angular velocities of `top` with respect to <span style="color:DarkBlue"> `base` </span> and <span style="color:orange"> `world` </span>:

Roll (rotation about X)             |  Pitch (rotation about Y)
:-------------------------:|:-------------------------:
![roll_angles](../../images/stewart_platform/roll.png)  |  ![pitch_angles](../../images/stewart_platform/pitch.png)

Even though `base` was subjected to disturbances, `top` maintained the same orientation as `world`.

## Implement this yourself

To know more, check out the [project report](https://abhishek47kashyap.github.io/files/StewartPlatformFinalReport.pdf). The full project repository, with the Simulink file, can be found [here](https://github.com/abhishek47kashyap/WPI-RBE-coursework/tree/master/RBE%20502/Stewart%20Platform_Final%20Project).