---
layout: post
category: projects
author: Alex
---
My team observed near earth asteroid 2002 MQ3, reduced images, found right ascension and declination, and determined its orbit using the Method of Gauss. 

![](/assets/images/SSP.png)

I wrote several more times code at SSP than I ever have. Much of it was translating equations that we had gone over during lecture into python, which was theoretically simple but very hard to debug. 

[Least squares plate reduction](https://drive.google.com/file/d/1D2KQCqI7DquNSFY8Y0MveyJNwI-0xAIG/view?usp=drive_link) (LSPR) was the first program we wrote specifically for processing our data. It turns x, y coordinates on a .fits image into right ascensions and declinations using known stars. Compared to the others it wasn’t too complicated; the hardest part was translating the sums into for loops.

[Aperture photometry](https://drive.google.com/drive/folders/1sx6ubxOH76AOT62bse6_UbrpQUU0Q5Ok) compares the signal of our asteroid to that of known reference stars to find its apparent magnitude. It was difficult because of centroiding — it was riddled with off-by-one errors and difficult to debug because wrong results seemed accurate. I also accidentally swapped x and y when slicing out the region of interest, and spent an hour wondering why my signal was negative, until our TA Kathryn explained. The actual mathematics to calculate signal and noise wasn’t difficult, though I had to be careful when selecting my stars to create the line of best fit; here’s one of my [write-ups of the results](https://docs.google.com/document/d/15xx77QHa-d-DKdPKiT9Yj9c3IzwNIaQ4XkDESzsG3FM/edit?usp=sharing). 

Programming the Method of Gauss to determine our asteroid’s orbit started with a [long pseudocode](https://drive.google.com/file/d/1LKMg0kuV8ZurVbsU6ZWHPlsD24l0pTT_/view?usp=drive_link), then extensive debugging. In my first few attempts I converted from Gaussian time into regular time at the wrong step, which resulted in my orbital elements being slightly off and my f & g functions not working for some inputs. Our asteroid converged after over 60 iterations (which would be really, really annoying to have to calculate by hand). 

After writing the Method of Gauss, I attempted orbit improvement, which was actually successful as it decreased the root mean square of the predicted orbit — interesting, since the other group observing 2002 MQ3 didn’t find orbit improvement helpful. I also chose to use multiprocessing via Python’s multiprocessing library to create a monte carlo program estimating the error on our orbital elements given the error on our original right ascensions and declinations. With 1 million runs, I got some [nice bell curves of each of the orbital elements](https://drive.google.com/file/d/1pV1RmBW9W_AV3_Z2CPPUs6xSGnZNXvff/view?usp=drive_link). 

[Final Monte Carlo method on the Method of Gauss with multiprocessing and orbit improvement](https://drive.google.com/file/d/1dCCt31AL9HNcmQ-BGcFvC0et0yPqoGnH/view?usp=drive_link)

[Final orbit determination report](https://docs.google.com/document/d/1IEa5u4rfKcvwZofLpTXpwqClvEkHZFVTPYuy8kCcpEQ/edit?usp=sharing)