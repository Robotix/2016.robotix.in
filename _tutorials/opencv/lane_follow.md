---
layout: post
title: "Lane Following"
categories:
  - opencv
redirect_from: "/tutorials/category/opencv/lane_follow/"
---

#### Introduction

Before proceeding with this module, we would request you to go through the set of general tutorials for image processing found on our website. It is quite extensive, and we will assume that a working knowledge, as put forward there, is in the grasp of the reader of this tutorial.  
(Please note that among the IP modules, of particular importance is the ubiquitous noise reduction, which will always be required to give clearer smoother images from the hazy video feed, which are easier to process)

#### Traversing the Corridors

The pictures and the 3D model of the simulated indoor arena give a good idea of what kind of corridors the robot will be traversing.

The first step would be to reduce the image of the corridor to the essential features. By applying Canny Edge detection and then excluding a certain upper portion of the image, the following transformations can be obtained:  
(The sample coloured image is an estimated view of the corridor in front of the robot, from the 3D model of the arena)

![][1]

 

![][2]

 

![][3]

As you can see, the transformations on the image received have made the video feed of the image considerably easier to analyse. Now the corridor essentially consists of two sloping lines on either side of the robot. We can use this information effectively to determine how the robot should move along the corridor.

#### Using Angles

To successfully implement this, you will need to be comfortable with the Hough Transform for lines, which will need to be implemented on the image. You may refer to our tutorial or to any other on the website for how to do this.

Applying the polar line transform will give you the major lines in the image and their angles, with algebraic sign. Visualising it very simply, one sees that if the sum of the angles of the two major lines is nearly zero, then the robot is placed between the two lines, and in the correct direction. At this point of time, it can move forward. Otherwise the robot must turn accordingly, such that the sum of the slopes becomes zero. A combination of these two techniques should allow the robot to make its way along the corridor while following it.

Given below is a code snippet which implements this part of the problem statement, in the manner described.

#### Generating a Middle Path

Another method to understand and follow the lane would also require the use of this type of reduction. Thereafter, it would require the generation of two lines that are parallel to each other and perpendicular (almost) to the direction of the two lines. The transformation is shown here:

![][4]

The above transformation can be done simply by taking two pairs of nearly equidistant points on the two lines, and computing their mid-points, and then comparing the relative positions of the mid-points.  
If the two mid-points are almost along the same vertical line, then the robot is in the correct orientation and should move forward. Otherwise, it should turn accordingly.

The above two methods can be used to allow the robot to follow a corridor. Now, we go to the next sub-problem to be solved by image processing – that of recognising the signs and symbols.

[1]: https://lh4.googleusercontent.com/NLPqv6Br-fXBConpONTDqFG__ELyMvcaMIRK2mzE1KH8MtHhc3tG93jM_M5lZ3Vzjgmp5N5ukgM9fuAtxtlCUTgBh3yoKN3yw_XGmcfar_YTgbtUwKWsOe0G
[2]: https://lh5.googleusercontent.com/PezFfQ4Z-JIUVFgEiXPFobyxDRxqMdbv52rAkE0l6mbkR2MuFhVcZp3EA4ZZAwpVJssVJyY97rkdcMyKY2uyEmhVVAc5uC0B-FfeSjWDtc5d2bGoaoyyiwYW
[3]: https://lh4.googleusercontent.com/0xC-I56RuHWvB5F0V0Bz9P0niOX8Riv39xypLiY4GfmUQqGr8SrM9Pl9zohENfBKkXuKeHI9epUM9rHNIMfKn4KEtNmNiD9bMDL2oBA0gCR2FHiIUco
[4]: https://lh4.googleusercontent.com/DIk2tHbzRJdiHM8pkNT58shLTtNUG-ZXkPFnVMHMCvs2XdiPH_pnSQ9fY4f95t9Boi0I68Orwj3JwnMhHy0BwMm1eGjsxOFaxAGqD7ltkxzMEkrpyW8
