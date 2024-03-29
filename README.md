# Jetson-Nano-Yolov5



I am using 128GB SD card

1.Installing Python on Jetson Nano
2.Installing Opencv on Jetson Nano
3.Connecting Camera and testing on Jetson Nano

1.Installing Python on Jetson Nano
  
   1.1.sudo apt-get install python3-pip
       Installing pip using above command
   1.2.$pip3 install virtualenv
       Installing Virtal environment using above command
   1.3.$python3 -m virtualenv -p python3 environment_name --system-site-packages
       myenv in my case
   1.4 activate environment 
        $source myenv/bin/actiavte
 

2.Installing opencv in to jetson Nano

   2.1.createing Swap File
    $free -h
    $sudo fallocate -l 4G /var/swapfile
    $sudo chmod 600 /var/sawpfile
    $sudo mkswap /var/swapfile
    $sudo swapon /var/swapfile
    $sudo bash -c 'echo "/var/swapfile swap swap defaults 0 0 ">>/etc/fstab'
    $reboot   
 
   2.2Install Dependencies

     	sudo sh -c "echo '/usr/local/cuda/lib64' >> /etc/ld.so.conf.d/nvidia-tegra.conf"
	sudo ldconfig
	sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
	sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
	sudo apt-get install libgtk2.0-dev libcanberra-gtk*
	sudo apt-get install python3-dev python3-numpy python3-pip
	sudo apt-get install libxvidcore-dev libx264-dev libgtk-3-dev
	sudo apt-get install libtbb2 libtbb-dev libdc1394-22-dev
	sudo apt-get install libv4l-dev v4l-utils
	sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
	sudo apt-get install libavresample-dev libvorbis-dev libxine2-dev
	sudo apt-get install libfaac-dev libmp3lame-dev libtheora-dev
	sudo apt-get install libopencore-amrnb-dev libopencore-amrwb-dev
	sudo apt-get install libopenblas-dev libatlas-base-dev libblas-dev
	sudo apt-get install liblapack-dev libeigen3-dev gfortran
	sudo apt-get install libhdf5-dev protobuf-compiler
	sudo apt-get install libprotobuf-dev libgoogle-glog-dev libgflags-dev

       ./install_dependencies.sh

   2.3 Download OpenCV:
	cd ~
	wget -O opencv.zip https://github.com/opencv/opencv/archive/4.5.1.zip 
	wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.5.1.zip 
	unzip opencv.zip 
	unzip opencv_contrib.zip
	mv opencv-4.5.1 opencv
	mv opencv_contrib-4.5.1 opencv_contrib
	rm opencv.zip
	rm opencv_contrib.zip

    2.4 Lets build OpenCV now:
	cd ~/opencv
	mkdir build
	cd build 
        copy and paste this entire block of commands below into your terminal.
	cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D EIGEN_INCLUDE_PATH=/usr/include/eigen3 -D WITH_OPENCL=OFF -D 	WITH_CUDA=ON -D CUDA_ARCH_BIN=5.3 -D CUDA_ARCH_PTX="" -D WITH_CUDNN=ON -D WITH_CUBLAS=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON -D OPENCV_DNN_CUDA=ON -D ENABLE_NEON=ON -D 	WITH_QT=OFF -D WITH_OPENMP=ON -D WITH_OPENGL=ON -D BUILD_TIFF=ON -D WITH_FFMPEG=ON -D WITH_GSTREAMER=ON -D WITH_TBB=ON -D BUILD_TBB=ON -D BUILD_TESTS=OFF -D WITH_EIGEN=ON -D 	WITH_V4L=ON -D WITH_LIBV4L=ON -D OPENCV_ENABLE_NONFREE=ON -D INSTALL_C_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D BUILD_NEW_PYTHON_SUPPORT=ON -D BUILD_opencv_python3=TRUE -D 	OPENCV_GENERATE_PKGCONFIG=ON -D BUILD_EXAMPLES=OFF ..

	(optional)Build OpenCV. This command below will take a long time (around 2 hours), make -j4     # (make then space single dash and then j4)

Finish the install:
cd ~
sudo rm -r /usr/include/opencv4/opencv2
cd ~/opencv/build
sudo make install
sudo ldconfig;make clean;sudo apt-get update 

Verify OpenCV Installation
#open python3 shell
python3
import cv2
cv2._version_


Install jtop, a system monitoring software for Jetson Nano.
cd ~
sudo -H pip3 install -U jetson-stats 
sudo reboot
jtop


Test Your Camera on Jetson Nano:
Turn on your Jetson Nano.
Open a new terminal window, and type:
ls /dev/video0   #csi camera
ls /dev/video*   # show you a list of cameras

Take a Photo:
nvgstcapture-1.0 --orientation=2       # for testing CSI camera
# V4L2 USB camera 
nvgstcapture-1.0 --camsrc=0 --cap-dev-node=1


install pytorch

https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048

select pytorch according to ur jetpack version

wget https://nvidia.box.com/shared/static/p57jwntv436lfrd78inwl7iml6p13fzh.whl -O   torch-1.8.0-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev libomp-dev
pip3 install 'Cython<3'
pip3 install numpy   torch-1.8.0-cp36-cp36m-linux_aarch64.whl


select correct toprchvision

$ sudo apt-get install libjpeg-dev zlib1g-dev libpython3-dev libopenblas-dev libavcodec-dev libavformat-dev libswscale-dev
$ git clone --branch v0.9.0 https://github.com/pytorch/vision torchvision   # see below for version of torchvision to download
$ cd torchvision
$ export BUILD_VERSION=0.9.0  # where 0.x.0 is the torchvision version  
$ python3 setup.py install --user
$ cd ../  # attempting to load torchvision from build dir will result in import error
$ pip install 'pillow<7' # always needed for Python 2.7, not needed torchvision v0.5.0+ with Python 3.6


clone yolov5 and in requiremnets remove pytorch and totchvion libraraies

sudo apt install -y libfreetype6-dev

 i am using yolov5 6.2


wget https://github.com/ultralytics/yolov5/releases/tag/v6.2/yolov5.pt

        

