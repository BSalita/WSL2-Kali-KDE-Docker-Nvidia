# Notes on installing Kali Linux in WSL2 including KDE Plasma GUI, Docker, Nvidia GPU and CUDA

## Use case is for exploring WSL2 GUI capabilities for data science. Seems stable but some things aren't working in GUI such as audio and network management. 
## Installation of other GUIs may be possible using similar methods (KeX, XFCE) but others don't presently work (Gnome and Cinnamon).

## Installation takes 30 minutes on AMD 4800H notebook

## Step 1) On Windows: install Kali Linux in WSL2. Assumes WSL2 is already installed.

`wsl --install -d kali-linux`

## Step 2) On Windows:
## 2.1) Install NVidia for WSL Driver: https://developer.nvidia.com/cuda/wsl
## Following steps (2.1.x) are optional. Only needed if CUDA and CUDNN are wanted:
### 2.1.1) Install Nvidia CUDA Tookit. See: https://towardsdatascience.com/installing-tensorflow-with-cuda-cudnn-and-gpu-support-on-windows-10-60693e46e781
### 2.1.2) Install CUDNN. See: https://medium.com/analytics-vidhya/installing-cudnn-for-gpu-support-with-tensorflow-on-windows-10-aff10c6c9929
### 2.1.3) Verify GPU is accessible from python: `python -c "import tensorflow as tf; tf.config.list_physical_devices('GPU')"`
### 2.1.4) If cudart64_101.dll is missing. see: https://stackoverflow.com/questions/59823283/could-not-load-dynamic-library-cudart64-101-dll-on-tensorflow-cpu-only-install
### 2.1.5) If missing Dlls are reported: see: https://github.com/tensorflow/tensorflow/issues/44291
## 2.2) Install Docker for Desktop from https://hub.docker.com/editions/community/docker-ce-desktop-windows

## Step 3) Install one of following presentation managers:
## 3.1) GWSL for Windows (XWindows manager) from Microsoft Store or https://github.com/Opticos/GWSL-Source
## 3.2) vcxsrv for Windows (XWindows manager) from https://sourceforge.net/projects/vcxsrv/
## 3.3) `apt install xrdp` (on Linux) to use Windows RDP instead of XWindows manager. See https://github.com/neutrinolabs/xrdp

## Install following software within Kali Linux

## Step 4) upgrade current distro
`sudo apt update -y && sudo apt upgrade -y && sudo apt dist-upgrade -y`

## Step 5) install nvidia gpu drivers and CUDA software
`sudo apt install -y nvidia-driver nvidia-cuda-toolkit`

## Step 6) test nvidia driver
`nvidia-smi`

## Step 7) install docker
`sudo apt install -y docker.io`

## Step 8) give user permissions to use docker without sudo
`sudo usermod -aG docker $USER`

## Step 9) test docker. be sure Docker for Windows Desktop is running. Otherwise these tests will fail.
`docker run hello-world`

## Step 10) test docker's gpu compatibility (assumes Nvidia drivers are already installed)
`docker run --rm -it --gpus=all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark`

## Step 11) required for starting up xwindows
`sudo apt install -y dbus-x11`

## Step 12) install desktop: kde-plasma-desktop (minimal), kde-standard (usuals), kde-full (lots). kali-desktop-kde is kde customized for kali distro.
## Use --no-install-recommends to disable inclusion of any extra packages.
`sudo apt install -y kali-desktop-kde --no-install-recommends`

## Step 13) start KDE Plasma desktop manager. if kde was just installed, might need to restart kali.
## 13A) Exit Kali Linux dropping back into Windows prompt
`exit`
## 13B) Reboot kali by shutting down kali and restarting
`wsl -d kali-desktop --shutdown && wsl -d kali-desktop`
## 13C) Within kali again start GUI. Assumes your presentation manager of choice (GWSL, vcxsrv or Remote Desktop (RDP)) is correctly installed and running. GUI will now be displayed by your presentation manager.
`startplasma-x11`

