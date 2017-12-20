# **Finding Lane Lines on the Road**

Finding lane lines on the Road is a project which goal is to automatically detect lane lines using an algorithm to apply in self driving cars. This algorithm uses Computer Vision techniques to show on road images and videos a couple of lines on top of the lanes. It is really important to detect the lines because the are a reference for where to steer the vehicle and decide where to go.

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />


Instructions to use it
---

1. Read and follow the instructions in https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md to set up your development environment.
2. Clone this repository

   git clone https://github.com/vmonestel/CarND-LaneLines-P1.git

3. Open the code in a Jupyter Notebook

The project code is in a Jupyter notebook (Jupyter is an Ipython notebook where you can run blocks of code and see results interactively).  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

To start Jupyter in your browser, use terminal to navigate to the project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in point 1):

`> jupyter notebook`

4. A browser window will appear showing the contents of the current directory. Click on the file called "P1_finding_lane_lines.ipynb".
5. Another browser window will appear displaying the notebook. Hit "Run" in every box to run the code. Also, you will find descriptions of all the implemented functions. The code takes the images from test_images folder and the videos from test-videos folder, processed then and save the results in their output folders. 
6. There is also some documentation in writeup.md file

Issues
---

This code may not work fine when an image/video is processed and it has curves or shadows on the road.

