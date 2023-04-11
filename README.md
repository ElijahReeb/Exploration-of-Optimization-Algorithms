UW-EE399-Machine-Learning-Demonstrations
=========
This repository holds all of my coding assignments as I learn to develop machine learning algorithms from the ground floor. The repository begins with fitting simple models to data and moves towards more complex machine learning algorithims as I investigate and experiment with these during the course of a quarter at UW. Assignments were designed by Professor Nathan Kurtz. 

Project Author: Elijah Reeb, elireeb@uw.edu

.. contents:: Table of Contents

Homework 1
---------------------
Introduction
^^^^^^^^^^^^
The assignment starts with linear and polynomial optimizations to model a small dataset. These models demonstrate some of the flaws and cautions necessary when fitting data to a model and how overparameterization can lead to massive error when the training data differs from the testing data (demonstrated in parts 3 and 4). This assignment also leads to show how when using a non-linear functions there may be many minima and thus a more local minimum is necessary (part 2). 

Theoretical Backgroud
^^^^^^^^^^^^
This assignment mostly uses code functions to optimize the models. The main measure of how good a model is the least squared error. When one is determining a model it makes intuitive sense to chose a model that produces outputs close to each of the expected outputs. The first part of this assignment focused simply on that. Using a cosine function to model the data. We can observe a small error of about 1.6 and see that the model is somewhat close to the data. This goal will be applied to a few different models to demonstrate benefits to certain fits. 

.. image:: ![image](https://user-images.githubusercontent.com/130190276/231070744-86b0fa3b-b7e5-4efd-a5d4-2c2c56e18f4d.png)

Algorithm Implementation and Development
^^^^^^^^^^^^
The algorithm for calculation of error can be done easily with a line of code similar to that below. The "model" is the collection of parameters of the selected polynomial for example. 

.. code-block:: text

        Error = np.sqrt((1/n) * np.sum((model(x)-y)**2))
        
As for determining the optimal parameters in a model to have the best fit, other's coding commands were used. Because a local minimum is saught in a polynomial model the derivative can be taken to solve for the exact parameters. This was done in the 19th degree polynomial using the below commands in the numpy package to directly determine this fit. For more general cases and for non polynomial models a more general method of using opt.minimize from the scipy package was used. These commands were developed by others had have their own implementations not covered (specifically the Nelder-Mead algorithm). 

.. code-block:: text

        fit = np.polyfit(x,y,19)
        model = np.poly1d(fit)


Computational Results
^^^^^^^^^^^^
Part 2 of this assignment involved taking the four parameter cosine model shown in the figure above and completing a parameter sweep of two parameters at a time while the other parameters were fixed at their local minimums. The results of these sweeps are shown below in color maps. The darker the color shows lower error meaning the large bands of dark blue represent areas where that parameter is at or close to a minimum. There are clear minima areas for A, B, and D. This is shown in the middle top graph for A. The darkest shading on the far left shows that A is at minimum on that side. This is the same cases for B and the bottom left graph and D on the bottom right graph. The other graphs are more difficult to see the minima for. This illustrates the point that the model does not require the "absolute minimum of the parameters" but still can have a strong prediction. 

.. image:: ![image](https://user-images.githubusercontent.com/130190276/231073437-a90b1201-3d3c-4d46-8e42-5a324d96edb1.png)


.. image:: ![image](https://user-images.githubusercontent.com/130190276/231073199-0c6ca76f-8e10-4a67-a7ed-7aad422b84fe.png)


.. image:: ![image](https://user-images.githubusercontent.com/130190276/231072969-d5c5552e-9017-4616-a7de-e1436ee0fea8.png)



Summary and Conclusions
^^^^^^^^^^^^
Comparing the graphs from part 3 and part 4 above we can observe that when the first 20 data points are selected the model creates a decent representation of those training points. The training errors for part 3 linear and parabolic fits are about 2. The 19th degree polynomial fit has a much lower training error because the parameters are designed to go through many of the points. This is similar to part 4 with there being error close to 2 for the linear and parabolic fit and much smaller error in the 19th degree polynomial. Simply put, in training the two methods have similar error when creating a model.
However, when applied to the different testing data points, the methods in parts 3 and 4 greatly differ. Part 3 in the parabolic and 19th order had much higher error levels than the Part 4 method. This is emphasized by an error of nearly 30 billion for the 19th degree polynomial when applied to the testing data of part 3. The main reason for this difference was that the part 3 division lead towards the lacking conclusion that the data continued upwards. In a parabolic fit the optimal model "assumed" the data would decrease in the next section. In the 19th order polynomial the optimal model had so much wiggle that it completely decreased after the training data. In part 4 the model has to instead "fill in the middle" information. This leads to much less error with these select fitting methods.

