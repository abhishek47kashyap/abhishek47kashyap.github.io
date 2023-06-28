---
title: "Virtual Manipulation Challenge ICRA 2023"
excerpt: "Keeping top plate steady by rejecting disturbances to base <br/><img src='/images/vmc_icra_2023/vmc_assembly.png' alt='vmc_assembly_competition_pic' style=\"width: 500px; height: auto;\">"
collection: portfolio
---

This page shows my work from my participation in the Assembly track of the [ICRA 2023 Virtual Manipulation Challenge](https://www.sim4dexterity.de/en/icra-2023-competition/competition-assembly.html).


This task had 3 difficulty levels, more information on which can be found [here](https://github.com/DavidPL1/assembly_example/wiki/screwing).

**Objective**:

> For this task, a screw, a nut, and a fixture are placed on the workspace table. The goal is to thread the screw into the nut. This requires solving the following sub tasks: pick up the nut, place the nut into the fixture, pick up the screw, align screw into nut, and tighten the screw.

---
**Manipulation** (at 10x speed)

![screwing_onto_nut_10x](../../images/vmc_icra_2023/screwing_onto_nut_10x.gif)

---
**Object detection** for the 3 objects (nut, screw, fixture)

Top row shows actual scene as observed through the 3 cameras: 2 fixed workspace cameras, and 1 camera mounted on gripper. Bottom row shows the results of the object detection (done using `YOLOv5`).

![object_detections](../../images/vmc_icra_2023/object_detections.gif)

The workspace cameras are used to get an approximate location of the 3 objects on the table, following which the gripper camera is used to refine the locations.
