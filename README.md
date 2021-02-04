# Notes on installing Kali Linux in WSL2 including KDE Plasma, Docker, Nvidia GPU and CUDA

# On Windows: install Kali Linux in WSL2

wsl --install -d kali-linux

# On Windows: (optional) install Docker for Desktop (Docker Desktop Installer)

# Install one of following presentation managers:
# 1) GWSL for Windows (XWindows manager) from Microsoft Store or https://github.com/Opticos/GWSL-Source
# 2) vcxsrv for Windows (XWindows manager) from https://sourceforge.net/projects/vcxsrv/
# 3) apt install xrdp (on Linux) (use Windows RDP instead of XWindows manager) from https://github.com/neutrinolabs/xrdp

# Install following software within Kali Linux

# upgrade current distro
sudo apt update -y && sudo apt upgrade -y && sudo apt dist-upgrade -y

# install nvidia gpu drivers and CUDA software (optional and large)
sudo apt install -y nvidia-driver nvidia-cuda-toolkit

# test nvidia driver
nvidia-smi

# install docker
sudo apt install -y docker.io

# give user permissions to use docker without sudo
sudo usermod -aG docker $USER

echo !!!!!!!!!!!!!!
echo Be sure Docker for Windows Desktop is running. Otherwise these tests will fail.
echo !!!!!!!!!!!!!!

# test docker
docker run hello-world

# test docker's gpu compatibility (assumes Nvidia drivers are already installed)
docker run --rm -it --gpus=all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark

# required for starting up xwindows
sudo apt install dbus-x11

# install desktop: kde-plasma-desktop (minimal), kde-standard (usuals), kde-full (lots)
# kali-desktop-kde is kde customized for kali distro.
sudo apt install -y kali-desktop-kde

# start KDE Plasma desktop manager
# if kde was just install, might be best to restart wsl
# 1) in Windows, do "wsl -d kali-desktop --shutdown"
# 2) in Windows, do "wsl -d kali-desktop"
# Put startplasma-x11 in startup file?
startplasma-x11

