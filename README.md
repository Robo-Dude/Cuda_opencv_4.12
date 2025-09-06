# Cuda_opencv_4.12
# Build OpenCV 4.12 with CUDA 12.9 on Ubuntu 24.04 (with cuDNN 9.12 & RTX 3050)

This guide explains how to compile and install OpenCV 4.12 from source with CUDA 12.9, cuDNN 9.12, and Python 3 bindings on Ubuntu 24.04.
Tested on: NVIDIA RTX 3050 GPU.

## 1. Install Dependencies
```
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

```

## 2. Install CUDA 12.9 & cuDNN 9.12

Install CUDA 12.9 from NVIDIA’s official CUDA Toolkit with nvidia 575 driver.

https://developer.nvidia.com/cuda-12-9-0-download-archive

Install cuDNN 9.12 compatible with CUDA 12.9.

https://developer.nvidia.com/cudnn-9-12-0-download-archive

#### Verify installation:

```
nvcc --version
nvidia-smi
```

<img width="1211" height="163" alt="Screenshot from 2025-09-06 22-11-13" src="https://github.com/user-attachments/assets/4906216c-30d5-462f-9d11-1bdd64759063" />


<img width="1211" height="457" alt="Screenshot from 2025-09-06 22-10-42" src="https://github.com/user-attachments/assets/f3769226-987f-4db6-9686-4c0a99ff449f" />


## 3. Get OpenCV Source
```
# clean
cd ~ 
sudo rm -rf opencv*

# download the latest version
wget -O opencv.zip https://github.com/opencv/opencv/archive/4.12.0.zip 
wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.12.0.zip

# unpack
unzip opencv.zip 
unzip opencv_contrib.zip 

# Some administration to make life easier later on
mv opencv-4.12.0 opencv
mv opencv_contrib-4.12.0 opencv_contrib

```
## 4. Create Build Directory

```
# set install dir
cd ~/opencv
mkdir build
cd build
```

## 5. Configure with CMake

For RTX 3050 , CUDA_ARCH_BIN=8.6 , Check for your's here --  https://developer.nvidia.com/cuda-gpus

```
cmake -D CMAKE_BUILD_TYPE=RELEASE \
  -D CMAKE_INSTALL_PREFIX=/usr \
  -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
  -D EIGEN_INCLUDE_PATH=/usr/include/eigen3 \
  -D WITH_OPENCL=OFF \
  -D CUDA_ARCH_BIN=8.6 \
  -D WITH_CUDA=ON \
  -D WITH_CUDNN=ON \
  -D WITH_CUBLAS=ON \
  -D ENABLE_FAST_MATH=ON \
  -D CUDA_FAST_MATH=ON \
  -D OPENCV_DNN_CUDA=ON \
  -D ENABLE_NEON=OFF \
  -D WITH_QT=OFF \
  -D WITH_OPENMP=ON \
  -D BUILD_TIFF=ON \
  -D WITH_FFMPEG=ON \
  -D WITH_GSTREAMER=ON \
  -D WITH_TBB=ON \
  -D BUILD_TBB=ON \
  -D BUILD_TESTS=OFF \
  -D WITH_EIGEN=ON \
  -D WITH_V4L=ON \
  -D WITH_LIBV4L=ON \
  -D WITH_PROTOBUF=ON \
  -D OPENCV_ENABLE_NONFREE=ON \
  -D INSTALL_C_EXAMPLES=OFF \
  -D INSTALL_PYTHON_EXAMPLES=OFF \
  -D PYTHON3_PACKAGES_PATH=/usr/lib/python3/dist-packages \
  -D OPENCV_GENERATE_PKGCONFIG=ON \
  -D BUILD_EXAMPLES=OFF \
  -D CMAKE_CXX_FLAGS="-march=native -mtune=native" \
  -D CMAKE_C_FLAGS="-march=native -mtune=native" ..
```
<img width="1211" height="517" alt="Screenshot from 2025-09-06 22-10-14" src="https://github.com/user-attachments/assets/7c8e4277-3b46-4bfd-975a-704f61d1b842" />


## 6. Build & Install
```
make -j$(nproc)
sudo make install
sudo ldconfig
```

## 7. Verify Installation in Python

```
python3 -c "import cv2; print(cv2.__version__)"
python3 -c "import cv2; print(cv2.cuda.getCudaEnabledDeviceCount())"
```

<img width="1211" height="119" alt="Screenshot from 2025-09-06 22-24-01" src="https://github.com/user-attachments/assets/f2c0bf73-93b8-4bb8-ae64-2d1ab3de750f" />



