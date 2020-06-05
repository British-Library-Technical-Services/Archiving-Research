{\rtf1\ansi\ansicpg1252\cocoartf2512
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\paperw11900\paperh16840\margl1440\margr1440\vieww10800\viewh8400\viewkind0
\pard\tx566\tx1133\tx1700\tx2267\tx2834\tx3401\tx3968\tx4535\tx5102\tx5669\tx6236\tx6803\pardirnatural\partightenfactor0

\f0\fs24 \cf0 ![British Library Logo](./assets/BL_Logo_RGB_100pixels_high.jpg)\
\
# Save our Sounds \'96 Unlocking our Sound Heritage\
\
### Phase Meters - A Primer\
_May 15th 2020_\
\
Karl Jenkins\
\
[karl.jenkins@bl.uk](https://webmail.bl.uk/owa/redir.aspx?C=TitieAObABWIfcCP-v0TKNeoRJTLVGApiItwOtdcE4qFiiAS4wbYCA..&URL=mailto%3atom.ruane%40bl.uk)\
\
### What is Phase?\
\
  \
\
We can describe the properties of a sound wave using maths. Usually this is represented on a graph that looks like this:\
\
  \
\
![Sine Wave plotted on a Graph](./assets/phase1.jpg)\
\
This graph shows a simple sine wave. The curve or function shown is blue is periodic, because it repeats its values over regular intervals. One repetition of the function is known as one period, or one cycle.\
\
  \
\
At what point in time we are on the curve, the phase, can be described using an angular unit, like a degree \'b0 or a radian, because trigonometry, but here\'92s a quick illustration:\
\
  \
\
![Relationship between degrees of a circle and sine-wave plot on a graph](./assets/phase2.gif)\
\
What we\'92re really interested in when we talk about phase is the  phase relationship, phase offset, phase difference or phase shift between two wave functions. You can see in the above animation that the arrows move around 360\'b0 of a circle.\
\
  \
\
The green arrow on the circle is rotated 180\'b0 from the blue arrow. Its phase offset is 180\'b0. It is 180\'b0 \'91out of phase\'92.\
\
  \
\
If the green circle\'92s radius was the same as the blue circle, and we added their amplitudes together, the result would be zero at all points along the cycle. The functions would cancel each other out. We can call this phase cancellation.\
\
Here\'92s a graphic illustrating constructive and destructive interference (and at one point, phase cancellation). The green and blue curves are being added together (summed), resulting in the red curve. When the green and blue curves are 180\'b0 out of phase, the red curve is flat, its amplitude is 0.\
\
![An animation demonstrating interference between two sine waves moving in and out of phase](./assets/phase3.gif)\
\
Notice also that the green and blue curves have the same wavelength. When they are half a wavelength apart, they are 180\'b0 out of phase. This is important when discussing tape azimuth and high frequency loss.\
\
This is a graph of a logarithmic frequency sweep from low to high frequency. It\'92s difficult to see the individual curves of the higher frequencies, since they are so close together.\
\
  \
![a plot of a sine wave sweep](./assets/phase4.png)  \
  \
If we add two of these sweeps together in a new sweep, and start to delay one of the sweeps by small millisecond amounts we can observe a few things from the result.\
  \
0ms\
![sweep at 0 seconds](./assets/phase5.png)\
0.05ms\
![sweep at 0.05 seconds](./assets/phase6.png)\
0.5ms\
![sweep at  0.5 seconds](./phase7.png)\
1ms\
![sweep at 1 second](./assets/phase8.png)\
1.5ms\
![sweep at 1.5 seconds](./assets/phase9.png)\
2.5ms\
![sweep at 2.5 seconds](./assets/phase10.png)\
\
  \
\
It only takes a very small delay for short-wavelength frequencies to interfere with each other destructively as seen at 0.05ms, but similarly they interfere constructively and return to normal level not long after at 0.5ms, and continue this pattern over time. You can see at 0.5 and 1ms the point at which wider wavelengths start to destructively interfere. At 2.5ms the middle wavelengths are destructively interfering, all the while the longest wavelengths i.e. the lowest frequencies, are mostly unaffected because the amount of delay isn\'92t close to the half-wavelength of the lowest frequency. This effect is known as comb filtering.\
\
The time delay created between two channels on an analog tape where the playback azimuth is misaligned creates the same interference behaviour. Since the azimuth adjustment effectively applies polar opposite delays to each channel, the range of adjustment isn\'92t wide enough for low frequencies to be affected.\
\
  \
\
Small deviations from optimal azimuth will affect the highest frequencies first, and larger deviations will introduce destructive interference into descending frequencies while the highest frequencies construct and destruct with every half-wavelength of adjustment.\
\
  \
\
Azimuth adjustments have a greater impact across more frequencies at slower tape speeds, and are more sensitive to adjustment for higher frequencies.\
\
  \
\
### What is a Phase Meter?\
\
  \
\
A phase meter is a visual tool that represents the phase relationship between two audio signals. This might be a stereo signal or a two-channel mono recording.\
\
  \
\
This can come in the form of a correlation meter:![example correlation meter interface](./assets/phase11.jpg)\
\
  \
\
Or a goniometer displaying a lissajous pattern (sometimes called a vector scope):\
\
The traditional lissajous display can be styled differently depending on the plugin or application you\'92re working with, but they all represent the same type of information.\
![example goniometer](./assets/phase12.gif)\
![vectorscope](./assets/phase13.png)  \
![180 lissajous](./assets/phase14.png)  \
\
### What do they mean?\
\
  \
\
#### Correlation Meter\
\
  \
\
A correlation meter will provide a reading in the range -1 to +1. This value represents the relative correlation (the degree to which the two signals are the same) between the left and right channels of a two channel signal.\
\
  \
\
A signal where two channels are identical will read +1, and a signal where two channels are identical and exactly 180\'b0 out of phase (i.e. they cancel each other out when summed) will read -1.\
\
  \
\
Most analog two channel recordings should tend to meter in the 0 to 1 range. Since the meter displays a reading which is an average over a set short period (10-100ms), fluctuation between these values is expected.\
\
  \
\
When adjusting playback equipment (azimuth, stylus alignment) with a test tape or disc, or audio program material, it can be useful to work with a correlation meter to find the metered range which tends closest to +1.\
\
#### Goniometer\
\
  \
\
A goniometer, lissajous or vectorscope is a scope displaying a lissajous figure. This can be a handy tool which represents several parameters in a two-channel audio signal at once, including level, phase correlation and signal balance.\
\
  \
\
In a two channel signal, on most lissajous displays, the left channel is a line rotated -45\'b0 from centre, being drawn continuously from the centre of the circle, up towards the top left, down towards the bottom right and back to the centre.\
\
  \
\
Think of this like a ball on the end of a string swinging back and forth over a piece of paper. The right channel is represented in a similar way, only rotated +45\'b0 from centre.\
\
![lissajous animation split](./assets/phase15.gif)\
\
  \
![pendulum sine](./assets/phase16.gif)  \
  \
  \
  \
  \
  \
  \
  \
  \
  \
\
If we put both of these balls on the same string, the line which is drawn will result from the motion of both pendulums. This isn\'92t even an analogy, the maths behind harmonic motion apply to sound waves and pendulums in the same way.\
\
  \
\
![pendulum phase space](./assets/phase17.gif)![sand pendulum](./assets/phase18.gif)\
\
  \
  \
  \
  \
\
If the two signals are identical, when they are added together, the scope will display a straight vertical line. We are adding the motion of both pendulums together, they will draw a line which is the sum of both of their motions. They are moving at the same time, so they are in phase. \'91M\'92, here, represents the Middle component of a stereo recording.\
\
  \
![mono lissajous](./assets/phase19.png)  \
  \
  \
  \
  \
  \
  \
  \
  \
  \
\
When the left and right channels aren\'92t identical, but are strongly correlated (i.e. mostly in phase with each other), the display will show a wider, dispersing line centered across the vertical axis.\
\
  \
![strongly correlated lissajous](./assets/phase20.png)  \
  \
  \
  \
  \
  \
  \
  \
  \
  \
\
The wider the image is across the horizontal axis corresponds to the difference between the two signals. This difference is the stereo field component of a stereo recording.\
\
  \
\
Where the lissajous is wider than it is tall, this indicates poor phase correlation.\
\
  \
![weakly correlated lissajous](./assets/phase21.png)  \
  \
  \
  \
  \
  \
  \
  \
  \
  \
  \
\
Where the major axis of the lissajous is rotated, this indicates a level difference between the channels.\
\
  \
![comparison of lissajous](./assets/phase22.png)\
\
Here\'92s a handy comparison of a \'91vectorscope\'92 and correlation meter side-by-side. Now it\'92s clear how the relationship between the middle and side components on the lissajous correspond to the values on the correlation meter. Note the handy R/L value on the correlation meter indicating the tendency for the combined signal towards L or R in the panorama.\
\
  \
\
Phase meters are useful as a tool to supplement critical listening when calibrating equipment or as a visual aid in diagnosing audio issues which might not be immediately apparent. Plus, lissajous scopes look cool and lend an engineer credibility among the uninitiated. And if you wanted someone to leave your studio you could explain how it works.![lissjous vs corellation meter](./assets/phase23.jpg)\
\
  \
\
When calibrating the azimuth on a tape machine or adjusting the tonearm and stylus of a turntable, the optimum visual representation of any two channel signal on a vectorscope is one whose major axis is closest to vertical with the narrowest possible spread across the horizontal axis (equating to a trend towards +1 on the correlation meter).\
\
### Bibliography\
\
  \
\
How Phase Meters Can Help Your Mixes. [online] Available at: <[https://www.sweetwater.com/insync/phase-meters-can-help-mixes/](https://www.sweetwater.com/insync/phase-meters-can-help-mixes/)> [Accessed 13 May 2020].\
\
Audiomasterclass.com. 2020. Visualizing Stereo Information Using Lissajous Figures. [online] Available at: <[https://www.audiomasterclass.com/newsletter/visualizing-stereo-information-using-lissajous-figures](https://www.audiomasterclass.com/newsletter/visualizing-stereo-information-using-lissajous-figures)> [Accessed 13 May 2020].\
\
Dr-jordan-design.de. 2020. Vector Scope Goniometer Phasemeter. [online] Available at: <[http://www.dr-jordan-design.de/Vectorscope.htm](http://www.dr-jordan-design.de/Vectorscope.htm)> [Accessed 13 May 2020].\
\
En.wikipedia.org. 2020. Lissajous Curve. [online] Available at: <[https://en.wikipedia.org/wiki/Lissajous_curve](https://en.wikipedia.org/wiki/Lissajous_curve)> [Accessed 13 May 2020].\
\
Hess, R., 2020. Azimuth: Hows And Whys \'96 Richard L Hess\'97Audio Tape Restoration Tips & Notes. [online] Richardhess.com. Available at: <[http://richardhess.com/notes/2006/09/27/azimuth-hows-and-whys/](http://richardhess.com/notes/2006/09/27/azimuth-hows-and-whys/)> [Accessed 13 May 2020].\
\
PreSonus Blog. 2020. Friday Tips: What\'92S A Phase Meter-And Why Should I Care? - Presonus Blog. [online] Available at: <[https://blog.presonus.com/index.php/2018/09/28/friday-tips-whats-phase-meter-care/](https://blog.presonus.com/index.php/2018/09/28/friday-tips-whats-phase-meter-care/)> [Accessed 13 May 2020].\
\
Signal Processing Stack Exchange. 2020. Correlation Meter - How Are They Calculated?. [online] Available at: <[https://dsp.stackexchange.com/questions/17098/correlation-meter](https://dsp.stackexchange.com/questions/17098/correlation-meter)> [Accessed 13 May 2020].\
\
Soundonsound.com. 2020. Q. What Are My Phase-Correlation Meters Telling Me?. [online] Available at: <[https://www.soundonsound.com/sound-advice/q-what-are-my-phase-correlation-meters-telling-me](https://www.soundonsound.com/sound-advice/q-what-are-my-phase-correlation-meters-telling-me)> [Accessed 13 May 2020].}