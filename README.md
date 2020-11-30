# Установка драйверов NVIDIA CUDA и библиотек для Data Science

1. Добавьте строку `deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /` в файл `/etc/apt/sources.list` (список источников APT).

2. Скачайте и установите deb-пакет с репозиторием CUDA:
```sh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
```

3. Добавьте ключ репозитория:
```sh
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
```

4. Обновите список пакетов:
```sh
sudo apt update
```

5. Установите пакеты NVIDIA:
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

6. После установки желательно заблокировать автоматическое обновление этих пакетов, чтобы гарантировать стабильную работу CUDA-драйверов:
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

7. Чтобы библиотеки были видны всем пользователям, обновите переменную окружения, добавив её в файл `/etc/environment`: 
```
export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/"
echo export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/" >> /etc/environment
```
На этом шаге установка драйверов NVIDIA завершается. Чтобы установить библиотеки для Data Science, выполните следующие шаги.

8. Установите общие пакеты:
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

9. Установите библиотеки для машинного и глубокого обучения. Их список можно изменить в зависимости от задач.
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
