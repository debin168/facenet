FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04

ENV PYCHARM_HOME=/etc/pycharm && \
    LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH 

# install libs, python3, pycharm ect...
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        openjdk-8-jre \
        curl \
        pkg-config \
        python3 \
        python3-dev \
        rsync \
        software-properties-common \
        unzip \
        python3-tk \
        wget \
        git \
        tar \
    	cmake \
   	checkinstall \
    	gfortran \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        liblapack-dev \
        libopenblas-dev \
        libxrender1 \
        libxtst6 \
    	libjpeg-dev \
    	libtiff-dev \
    	libjasper-dev \
    	libpng-dev \
    	libavcodec-dev \
    	libavformat-dev \
    	libswscale-dev \
    	libv4l-dev \
    	libgtk2.0-dev \
    	libatlas-base-dev \
    	liblapacke-dev \
        && \
    wget https://download.jetbrains.com/python/pycharm-community-2016.2.3.tar.gz -O /tmp/pycharm.tar.gz && \
    mkdir ${PYCHARM_HOME} && tar -xzvf /tmp/pycharm.tar.gz -C ${PYCHARM_HOME} --strip=1 && \
    curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    rm get-pip.py && \
    ldconfig /usr/local/cuda/lib64 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /

# Installing OpenCV
RUN wget https://github.com/Itseez/opencv/archive/3.2.0.zip -O opencv.zip \
	&& unzip opencv.zip \
	&& wget https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip -O opencv_contrib.zip \
	&& unzip opencv_contrib \
	&& mkdir /opencv-3.2.0/cmake_binary \
	&& cd /opencv-3.2.0/cmake_binary \
	&& cmake -DOPENCV_EXTRA_MODULES_PATH=/opencv_contrib-3.2.0/modules \
	  -DBUILD_TIFF=ON \
	  -DBUILD_opencv_java=OFF \
	  -DWITH_CUDA=OFF \
	  -DENABLE_AVX=OFF \
	  -DWITH_OPENGL=ON \
	  -DWITH_OPENCL=ON \
	  -DWITH_IPP=ON \
	  -DWITH_TBB=ON \
	  -DWITH_EIGEN=ON \
	  -DWITH_V4L=ON \
	  -DBUILD_TESTS=OFF \
	  -DBUILD_PERF_TESTS=OFF \
	  -DCMAKE_BUILD_TYPE=RELEASE \
	  -DBUILD_opencv_python3=ON \
	  -DCMAKE_INSTALL_PREFIX=$(python3 -c "import sys; print(sys.prefix)") \
	  -DPYTHON_EXECUTABLE=$(which python3) \
	  -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
	  -DPYTHON_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") .. \
	&& make -j8 install \
	&& rm /opencv.zip \
	&& rm /opencv_contrib.zip \
	&& rm -r /opencv-3.2.0 \
	&& rm -r /opencv_contrib-3.2.0











