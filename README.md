# How to install NVIDIA CUDA drivers and Data Science libraries

1. Add `deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /` string to `/etc/apt/sources.list` file (APT source list).

2. Download and install the deb package with the CUDA repository:
```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
```

3. Add a repository key:
```sh
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
```

4. Update the package list:
```sh
sudo apt update
```

5. Install NVIDIA packages:
```sh
sudo apt install \
cuda-10-1 \
cuda-toolkit-10-1 \
cuda-tools-10-1 \
cuda-runtime-10-1 \
cuda-compiler-10-1 \
cuda-libraries-10-1 \
cuda-libraries-dev-10-1 \
libcudnn7=7.6.5.32-1+cuda10.1 \
libcudnn7-dev=7.6.5.32-1+cuda10.1
```

6. It is recommended to disable automatic updates of these packages to ensure stable operation of CUDA drivers:
```sh
sudo apt-mark hold install \
cuda-10-1 \
cuda-toolkit-10-1 \
cuda-tools-10-1 \
cuda-runtime-10-1 \
cuda-compiler-10-1 \
cuda-libraries-10-1 \
cuda-libraries-dev-10-1 \
libcudnn7=7.6.5.32-1+cuda10.1 \
libcudnn7-dev=7.6.5.32-1+cuda10.1
```

7. To make the libraries visible to all users, update the environment variable by adding it to the `/etc/environment` file: 
```
export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/"
echo export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/" >> /etc/environment
```
This completes the installation of the NVIDIA drivers. To install the Data Science libraries, follow next steps.

8. Install common packages:
```sh
sudo apt install \
curl \
gnupg \
git \
python3 python3-pip python3-venv python3-dev python3-setuptools python3-lib2to3 python3-distutils \
g++ g++-7 \
build-essential \
java-common openjdk-11-jre-headless default-jre-headless ca-certificates-java \
linux-libc-dev libc6-dev libssl-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev libcairo2-dev \
libgirepository1.0-dev linux-headers-$(uname -r)
```

9. Install the ML/DL libraries. You can edit the list depending on your task.
```sh
python3 -m pip install --use-feature=2020-resolver \
ai-benchmark \
Bottleneck \
catboost \
fastai \
freetype-py \
ipykernel \
ipython ipython-genutils ipywidgets \
jupyter jupyter-client jupyter-console jupyter-core jupyterlab jupyterlab-server notebook \
Keras Keras-Preprocessing \
lightgbm \
matplotlib \
nltk \
numpy \
nvidia-ml-py3 \
opencv-python \
pandas \
pandocfilters \
pip \
plotly \
protobuf \
scikit-learn \
scipy \
setuptools \
six \
sympy \
tensorflow-gpu tensorboard tensorboard-plugin-wit tensorboardX tensorflow-estimator \
torch \
torchvision \
wheel \
xgboost \
zipp
```
