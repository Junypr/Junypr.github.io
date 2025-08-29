---
author: Alex
category: projects
layout: post
---
Characterizing the uncertainty in a stereophotogrammetry system used by the NASA Ames Unitary Plan Wind Tunnel to measure model angle of attack. Mentored by Ted Garbeff and Lindsey Drone. 

![](/assets/images/UPWT.jpg)
(some of the interns in IR)

I started by getting familiar with Ted's camera and light setup, the hexapod (a platform with 6 degrees of freedom and 0.00001mm accuracy) and OpenCV in Python. I spent some time blazing through computer vision textbooks — I hadn't done anything with computer vision before, so I had to learn a lot. 

I wrote a suite of detection and refinement methods using OpenCV's functions: blob detection, Harris corner detection, convolution, and ellipse fit refinement, centroiding, corner refinement, and a special convolution refinement algorithm Ted devised. I wrote methods to triangulate points and convert from the camera reference frame to the hexapod's. I also experimented with camera calibration — and realized that it was far finickier than expected.

The other interns and I about a dozen targets of different shapes and sizes with an airbrush and Cricut stencils. I started taking my own data. I did experiments to determine the system's accuracy in measuring motion of a few mm with different targets.

I realized that to get a better picture of the error in the system, I wanted a lot of precise data points, that I could take quickly. So I used different calibration boards (checker pattern and dot pattern) and measured the positions of the dots relative to each other with the cameras, then compared the results to the board's specs. I found that the accuracy depended a lot on the calibration I used, and that errors were systematic (some parts of the board all skewing one way, for example) so I used multiple pictures of the same board in the exact same position to determine error from noise, and then dived deeper into calibration.

I took several thousand photos of a checker calibration board in different positions and used that as the raw data to run a Monte Carlo simulation on camera calibration. Combining that with the measured error from noise, I input all the errors into a Monte Carlo simulation on triangulation, and found that error in camera calibration had the largest effect on error in triangulation results. 

I did other experimenting to see the effects of other possible variables: like vibration (I convinced two test engineers, the interns, and Lindsey to jump up and down in sync with me in the lab), binning, and lighting. 

[The presentation I gave to the NASA Ames Aeronautics division at the end of my internship.](https://drive.google.com/file/d/1A-Rncfb17Ya3Z-CIl4nMNU3zIlAfGhYu/view?usp=drive_link) It had cooler animations in powerpoint.

I spent a fair amount of time making sure that the code I wrote was well documented, in the hopes that it'll be used in the future (because it's free! and matlab isn't!). I used multiprocessing with the detection methods so I could process many images in parallel, speeding up my data analysis (the images were each ~50mb, so any speedup helped a lot). I also optimized the original convolution refinement code I wrote to take advantage of arrays, finally getting it to similar speeds as OpenCV's other detection / refinement methods. 

Despite this, my poor intern loaner laptop hit 100% CPU frequently. During some Monte Carlo runs (camera calibration, ahem), I left it running for a few hours to go explore other NASA labs or the wind tunnels!

Cool things I got to see (that I'm allowed to post):
- Schlieren (shadowgraph) — we popped balloons and played a trumpet and watched the sound waves with a high speed camera
- the Vertical Gun Range, which I wouldn't describe as a gun but more like a cannon that simulates asteroid impacts, capsules descending, etc.
- the super computing facility
- the largest wind tunnel in the world
- an anechoic RF chamber
- the lead screw that adjusts the floor of the wind tunnel, changing its mach number

I also had time to take cool photos with the wind tunnel's IR camera and make a 3D music video using the camera setup (see the end of the [presentation](https://drive.google.com/file/d/1A-Rncfb17Ya3Z-CIl4nMNU3zIlAfGhYu/view?usp=drive_link)!). 

