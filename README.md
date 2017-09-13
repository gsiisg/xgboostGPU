# How to compile xgboost with GPU support on windows 10

This tutorial is for setting up xgboost with GPU support

# Things I had already installed:

1. Windows 10 Pro

2. Anaconda with python 3.6
   https://www.anaconda.com/download/  

3. Tensorflow 1.3 with GPU support which required
  * CUDA Toolkit 8.0
  * Nvidia Drivers for my aging 980 GTX
  * cuDNN v6 (not required by xgboost)
   https://www.tensorflow.org/install/install_windows  
   Here I just installed tensorflow with GPU as the default and did not use a virtual environment  

4. Git for windows
https://git-scm.com/download/win

5. Visual Studio 14 2015 (I tried Visual Studio 15 2017 but ran into errors so reverted to using older Visual Studio)
-> do custom install and add the "Visual C++" package it will be needed
https://imagine.microsoft.com/en-us/Catalog/Product/101

6. CMake for windows
https://cmake.org/download/

# Installation Steps
I basically followed the guide at the following link, using Visual Studio instead of mingw to build
https://xgboost.readthedocs.io/en/latest/build.html#building-on-windows

1. Download xgboost source with git clone
git clone --recursive https://github.com/dmlc/xgboost xgboostGPU

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
double click on the 'xgboost.sln' file, this should start Visual Studio 14 2015
