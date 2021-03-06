# basics
```
sudo apt update && sudo apt -y upgrade && sudo apt -y autoremove && sudo apt -y autoclean
sudo apt -y install screen htop git cmake
sudo apt -y install build-essential 
```

# jetson-inference
https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md
```

mkdir -p ~/git
cd ~/git
git clone https://github.com/dusty-nv/jetson-inference
cd jetson-inference
git submodule update --init
mkdir build
cd build
cmake ../
make
```
https://github.com/dusty-nv/jetson-inference/blob/master/docs/imagenet-console-2.md
```
cd ~/git/jetson-inference/build/aarch64/bin
./imagenet-console orange_0.jpg output_0.jpg
./imagenet-console granny_smith_1.jpg output_1.jpg
```

# TensorFlow
https://docs.nvidia.com/deeplearning/dgx/install-tf-xavier/index.html
```
# prerequesties
sudo apt -y install libhdf5-serial-dev hdf5-tools
sudo apt -y install python3-pip
sudo apt -y install zlib1g-dev zip libjpeg8-dev libhdf5-dev 
sudo pip3 install -U numpy grpcio absl-py py-cpuinfo psutil portpicker grpcio six mock requests gast h5py astor termcolor
# tensorflow
pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu
```

# python
```
sudo apt -y install python3-pip
# scipy
sudo apt -y install libblas-dev liblapack-dev
sudo apt -y install gfortran
sudo pip3 install -U scipy 
# 
sudo pip3 install -U pandas scikit-learn
# matplotlib
sudo apt -y install libfreetype6-dev libpng-dev pkg-config
sudo pip3 install -U matplotlib
# 
# sudo pip3 install -U keras
# sudo pip3 install pillow Jetson.GPIO Jetson.GPIO
```

# jupyter
```
# sudo apt -y install jupyter-notebook
sudo apt -y install libpng-dev libjpeg8-dev libfreetype6-dev libxft-dev
sudo pip3 install -U jupyterlab
# node.js is required for extensions
sudo apt install -y nodejs
sudo pip3 install -U jupyter-git jupyter-tensorboard
# 
jupyter-notebook --generate-config
cat >>  ~/.jupyter/jupyter_notebook_config.py << EOL
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.token = ''
```

# media
```
sudo apt install autofs smbclient cifs-utils 
sudo apt install ffmpeg gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly
sudo systemctl stop autofs.service
sudo mkdir -p /Volume/media
sudo systemctl start autofs.service
```


# F200 realsense
```
sudo apt -y install libusb-1.0-0-dev pkg-config
sudo apt -y install qtcreator
sudo apt -y install libxinerama-dev libglfw3-dev libxcursor-dev libgtk-3-dev
mkdir -p ~/git
cd ~/git
git clone https://github.com/IntelRealSense/librealsense.git
cd librealsense
mkdir build
cd build
cmake ..
make
sudo make install
cd ..
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules && udevadm trigger
./scripts/patch-uvcvideo-16.04.simple.sh
sudo modprobe uvcvideo
```

# pyTorch
```
wget https://nvidia.box.com/shared/static/veo87trfaawj5pfwuqvhl6mzc5b55fbj.whl -O torch-1.1.0a0+b457266-cp36-cp36m-linux_aarch64.whl
pip3 install numpy torch-1.1.0a0+b457266-cp36-cp36m-linux_aarch64.whl
git clone https://github.com/pytorch/vision
cd vision
sudo python setup.py install
```

# opencv
```
#swap領域(ここでは6GB)の作成
fallocate -l 6G swapfile
chmod 600 swapfile
mkswap swapfile
sudo swapon swapfile
#swap領域が設定されているかの確認
free -m

cd
wget https://raw.githubusercontent.com/AastaNV/JEP/master/script/install_opencv4.0.0_Nano.sh
chmod 774 install_opencv4.0.0_Nano.sh
./install_opencv4.0.0_Nano.sh ~
```

