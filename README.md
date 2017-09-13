# How to compile xgboost with GPU support on windows 10 with python wrapper

This tutorial is for setting up xgboost with GPU support

# Things I had already installed:

1. Windows 10 Pro

2. Anaconda with python 3.6

   https://www.anaconda.com/download/  

3. Tensorflow 1.3 with GPU support

   https://www.tensorflow.org/install/install_windows  
   Here I just installed tensorflow with GPU as the default and did not use a virtual environment  
   which required:  
  * CUDA Toolkit 8.0
  * Nvidia Drivers for my aging 980 GTX
  * cuDNN v6 (not required by xgboost)
  
4. Git for windows

   https://git-scm.com/download/win  

5. Visual Studio 14 2015 (I tried Visual Studio 15 2017 but ran into errors so reverted to using older Visual Studio)

   https://imagine.microsoft.com/en-us/Catalog/Product/101  
  * do custom install and add the "Visual C++" package, it will be needed
  
6. CMake for windows

   https://cmake.org/download/  

# Installation Steps
I basically followed the guide at the following link, using Visual Studio instead of mingw to build
https://xgboost.readthedocs.io/en/latest/build.html#building-on-windows

1. Download xgboost source with git clone

   git clone --recursive https://github.com/dmlc/xgboost xgboostGPU  

   Here I named the folder as xgboostGPU but if you omit that it will just use the default name xgboost  
   
2. Update xgboost submodule

   cd xgboostGPU  
   git submodule init  
   git submodule update  

3. CMake to create build files

   mkdir build  
   cd build  
   cmake .. -G "Visual Studio 14 2015 Win64" -DUSE_CUDA=ON  
   
   This will create the xgboost.sln solution file in the 'build' directory that was just created

4. Build using Visual Studio 14 2015
   Make sure the drop down boxes are selecting 'Release' and 'x64'

   ![alt text](/VS2015_1.PNG?raw=true "Visual Studio 2015 screen capture 1")  
   
   Right click on xgboost on the right panel and select 'build' (This is the part where I get error if I used Visual Studio 15 2017)
   
   ![alt text](/VS2015_2.PNG?raw=true "Visual Studio 2015 screen capture 2")  
   
5. Install python wrapper for xgboost with GPU
   
   cd ../python-package
   python setup.py install
   
   Congrats, if everything was successful then xgboost is now installed with GPU support and python wrapper
   
# Test xgboost with GPU
Running a quick script with xgboost with GPU and compare the difference with CPU:

   cd ../demo
   cd gpu_acceleration
   python cover_type.py
   
With gpu the run time was ~15 sec and with CPU ~60 sec, so about a 4x speedup for me on a 980 GTX for this script, your milage may vary
