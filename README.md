# Lab-exercise-3

## Overview
The objective of this set of exercises is to compute hillslope profiles assuming hillslope evolution is a diffusive process. As discussed in lecture, the hillslope diffusion model is based on the principal of conservation of mass, which states that the changes in surface elevation are proportional to the sediment flux along the hillslope.

## Getting started
1. You can start by making a folder to store files for this week's exercises.

    ```bash
    $ cd Desktop
    $ mkdir Lab-3
    $ cd Lab-3
    ```
**Reminder**: the `$` symbol above represents the command prompt in the Terminal window.
2. Now you can open Spyder.

    ```bash
    spyder
    ```

Now we are ready to start.

## Problem 1 - Steady-state diffusive hillslope profiles
In this exercise, you will be plotting a diffusive hillslope profile and exploring the effect of various parameters on the hillslope geometry. Like last time, you are given [a broken Python script](hillslope_profile_ex1.py) that must be modified to complete this problem. Download a [copy of the script](hillslope_profile_ex1.py) to your `Lab-3` directory and open it in Spyder to start. Your tasks are to:

1. Modify the file to include a `for` loop that calculates the surface elevation of the hillslope (variable `h`) as a function of horizontal distance (variable `x`). Your *x*-values should be in one-meter increments and the *x*-value range should be large enough to include one complete interfluve (ridge) from valley to valley. The equation for calculating the elevation as a function of horizontal distance (*x*) was presented in lecture and is already in the Python script. Your job is to make it calculate the elevation at each *x*-value.
2. Two channels are located 100 m apart and incise into a landscape being uplifted at a rate of 0.5 mm/a producing an interfluve with two symmetrical hillslopes. Calculate the profile of the hillslope system, assuming the erosion is a diffusive process with a diffusion coefficient of 50 × 10<sup>-3</sup> m<sup>2</sup>/a. Using the Python script you just modified, you should do this calculation using the solution for the diffusion equation, which is parabolic in form.
3. Add some calculated values for this hillslope geometry to the plot.
  - **At what value of *x* (distance from the divide) is the maximum hillslope gradient?** Add lines of code to the bottom of the Python program to calculate the maximum hillslope gradient and add it to the plot with the `text()` function (see `help(plt.text)` for help using this function). You can find the equation for the hillslope gradient (*dh*/*dx*) in the notes from Lecture 6, where the diffusion equation was solved. **Where is the maximum slope angle in relation to the crest of the interfluve and the river channel?**
  - What is the maximum slope angle in degrees? Add this to your plot using the `text()` function below the maximum hillslope gradient.
  - What is the maximum relief of the hillslope? The maximum relief of the hillslope is the difference in elevation between the hillcrest and the adjacent valley bottom. Add lines of code to the bottom of the Python script to calculate the maximum relief and display it on the plot with the `text()` function.
  - Diffusive problems have a characteristic timescale τ. **What does a characteristic timescale mean?** You may want to use [Google](https://www.google.fi) to look up the characteristic timescale of diffusion. Mathematically, the characteristic time scale for diffusion is simply the length scale of the problem squared, divided by the diffusivity. Convert the previous sentence to and equation in Python and add lines of code to the bottom of the Python script to calculate the characteristic timescale and display this information on your plot using the `text()` function. **What is the value for the characteristic timescale? Does it seem reasonable? Why or why not?**

    :heavy_exclamation_mark: This is a good point to stop and save a copy of your plot with the values calculated in questions 3 displayed as text on the plot.

4. Explore the effect of different parameters on the hillslope geometry. Starting with the initial plot you made for question 2 above, make an additional plot for each of the four variations to the following parameters. In each case be sure you only vary a single parameter from the original values in question 2.
  - Change `L` to 100 m
  - Double the uplift rate
  - Double the diffusivity
  - Reduce the diffusivity by half

**For questions 2-4 of this exercise, you should modify the end of this document to include**

1. One plot with the values from question 3 displayed as text on the plot
2. One plot for **each** of the four modifications in question 4
3. A figure caption beneath **each** plot explaining what it shows as if it was in a scientific publication
4. Answers to the questions in bold for question 3 below all of the plots and captions

**You should also save a copy of your modified code in your Github repository**.

## Problem 2 - Mountain hillslope profiles
Active mountain ranges typically have poorly developed soils and abundant exposed bedrock.

### Part 1 - Mountain hillslope profiles
For this question, you can use your modified Python script from Problem 1. Assuming an interfluve width of 20 km, an uplift rate of 0.5 mm/a, and an appropriate diffusivity for rock of 10 m<sup>2</sup>/a, calculate a hillslope profile. Again calculate the maximum slope and its value in degrees, the maximum relief, and the characteristic timescale just as you did for Problem 1.

### Part 2 - Incision history of the western Sierra Nevada mountains, California, USA 
For this section we will apply our model equation to a real landscape, the western Sierra Nevada mountains in California, USA. We will use [a topographic profile](sierras_profile.txt) extracted across an interfluve between two streams draining into the Yuba River and change the landscape uplift rate in the equation until we get a reasonable match to the observed profile from our equation.

1. Before we load anything, it is important that you know the location of the topographic profile.

    ![Topographic profile location](Images/Sierras_profile_map.png)
    *Figure 1. Shaded relief digital elevation model of the western Sierra Nevada Mountains in California, USA. The line A-A´ is the location of a topographic profile used in Part 2 of Problem 2.*

2. Now that you know where the profile is located, you should download [a copy of the data file](sierras_profile.txt) for this week's exercise and save it in your directory `Lab-3` directory. The data file contains distances from the drainage divide and elevations for the topographic profile A-A´. For this part of the exercise you will also be using [another broken Python script](hillslope_profile_ex2.2.py) for loading and plotting the profile data and your calculated hillslope profile geometry. The profile data should be loaded into arrays `data_x[]` and `data_h[]`, noting that the first column in the data file should be `data_x` and the second should be `data_h`. There is no header on this file. As in Problem 1, part of this script is not currently working and you will need to add the `for` loop for calculating the hillslope elevations exactly like you did in Problem 1.
3. Once you have modified the program to add the `for` loop, you will want to change some of the variables that go into the equation for hillslope diffusion. You will be exploring a range of landscape uplift rates (`U`), but the values for the other variables should not change. Set the diffusion coefficient `kappa` to 1.8 m<sup>2</sup>/a and the half-width of the hillslope `L` should be half of the distance between the channels, which can be measured off the topographic profile in Figure 2 below. Your *x*-values should range across the entire interfluve with distance increments of 100 m.

    ![Topographic profile](Images/sierras_profile.png)<br/>
    *Figure 2. Topographic profile across an interfluve between 2 streams draining into the Yuba River, Sierra Nevada mountains, California, USA.*

4. Lastly, you will want to plot the observed topographic profile along with the model prediction to try and fit the observation by varying the uplift rate until you get a similar profile. Add a line in the script to plot the observed data using the `plot()` function. Be sure to use a different line color or pattern so that it is clear which line is the model and which is the data profile. Once you've determined your best-fit uplift rate, add text to the plot to display that rate using the `text()` function. Also, you will want to shift the model profile up about 750 m since the channels in the observed profile are at ~750 m elevation.

**For Problem 2 you should add the following to the end of this document**
1. A copy of the plot for Part 1 of Problem 2 with the 4 calculated values displayed on it and a figure caption as if the figure was in a scientific publication.
2. A 1 paragraph discussion of the implications these results have for mountain hillslopes. What do the various values you have calculated imply for natural systems?
3. A Python plot comparing the observed and predicted topographic profiles for Part 2 with the landscape uplift rate added as text on the plot.
4. A figure caption explaining what is plotted as if it were in a scientific publication.

**As in Problem 1, you should also save a copy of your modified code in your Github repository**.

# Answers
## Problem 1
This is some text. You can use *italics* or **bold** text easily. You may want to read a bit more about [formatting text in Github-flavored Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/). You can see an example of how to display an image with a caption below.

![Text shown if image does not load](Images/sine.png)<br/>
*Figure 1: Sine wave calculated from 0 to 2π*
