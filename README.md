# Cuda_opencv_4.12
# Build OpenCV 4.12 with CUDA 12.9 on Ubuntu 24.04 (with cuDNN 9.12 & RTX 3050)

This guide explains how to compile and install OpenCV 4.12 from source with CUDA 12.9, cuDNN 9.12, and Python 3 bindings on Ubuntu 24.04.
Tested on: NVIDIA RTX 3050 GPU.

## 1. Install Dependencies
  sudo apt-get install -y cmake
  sudo apt-get install -y libjpeg-dev libjpeg8-dev libjpeg-turbo8-dev
  sudo apt-get install -y libpng-dev libtiff-dev libglew-dev
  sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev
  sudo apt-get install -y libgtk2.0-dev libgtk-3-dev libcanberra-gtk*
  sudo apt-get install -y python3-pip
  sudo apt-get install -y libxvidcore-dev libx264-dev
  sudo apt-get install -y libtbb-dev libxine2-dev
  sudo apt-get install -y libv4l-dev v4l-utils qv4l2
  sudo apt-get install -y libtesseract-dev libpostproc-dev
  sudo apt-get install -y libvorbis-dev
  sudo apt-get install -y libfaac-dev libmp3lame-dev libtheora-dev
  sudo apt-get install -y libopencore-amrnb-dev libopencore-amrwb-dev
  sudo apt-get install -y libopenblas-dev libatlas-base-dev libblas-dev
  sudo apt-get install -y liblapack-dev liblapacke-dev libeigen3-dev gfortran
  sudo apt-get install -y libhdf5-dev libprotobuf-dev protobuf-compiler
  sudo apt-get install -y libgoogle-glog-dev libgflags-dev
