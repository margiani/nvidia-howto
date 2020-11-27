# Установка драйверов CUDA и библиотек для машинного и глубокого обучения

1. Добавить строку `http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /` в файл `/etc/apt/sources.list` (список источников APT).

2. Скачать и установить deb-пакет с репозиторием CUDA:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804_10.1.105-1_amd64.deb
```

3. Добавить ключ репозитория:
```
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
```

4. Обновить список доступных пакетов:
`sudo apt update`

5. Установить общие пакеты:
```
sudo apt install linux-libc-dev ffmpeg curl wget gnupg git python3 python3-pip python3-venv python3-dev python3-setuptools python3-lib2to3 python3-distutils g++ g++-7 build-essential java-common openjdk-11-jre-headless default-jre-headless ca-certificates-java dh-python linux-libc-dev libc6-dev build-essential libssl-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev libcairo2-dev libgirepository1.0-dev linux-headers-$(uname -r)
```

6. Установить пакеты NVIDIA:
```
sudo apt install cuda-10-1 cuda-toolkit-10-1 cuda-tools-10-1 cuda-runtime-10-1 cuda-compiler-10-1 cuda-libraries-10-1 cuda-libraries-dev-10-1  libcudnn7=7.6.5.32-1+cuda10.1 libcudnn7-dev=7.6.5.32-1+cuda10.1
```

7. После установки желательно заблокировать автоматическое обновление этих пакетов, чтобы гарантировать стабильную работу CUDA-драйверов.
```
sudo apt-mark hold install cuda-10-1 cuda-toolkit-10-1 cuda-tools-10-1 cuda-runtime-10-1 cuda-compiler-10-1 cuda-libraries-10-1 cuda-libraries-dev-10-1  libcudnn7=7.6.5.32-1+cuda10.1 libcudnn7-dev=7.6.5.32-1+cuda10.1
```

8. Чтобы были видны все библиотеки, нужно обновить переменную окружения, добавить её в файл `/etc/environment`, чтобы её было видно всегда и всем пользователям: 
```
export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/"
echo export LD_LIBRARY_PATH="/usr/local/cuda-10.0/targets/x86_64-linux/lib:/usr/local/cuda-10.1/targets/x86_64-linux/lib:/usr/local/cuda-10.2/targets/x86_64-linux/lib:/opt/nvidia/nsight-systems/2020.3.4/target-linux-x64/libcupti.so.10.0:/usr/local/cuda-10.1/extras/CUPTI/lib64/" >> /etc/environment
```

9. Установить библиотеки для машинного и глубокого обучения. Список можно дополнять в зависимости от задач.
```
python3 -m pip install --upgrade pip wheel setuptools six
python3 -m pip install absl-py ai-benchmark argon2-cffi astunparse attrs backcall beautifulsoup4 bleach blis Bottleneck cachetools catalogue catboost certifi cffi chardet click cycler cymem Cython dataclasses decorator defusedxml distro-info entrypoints fastai fastprogress ffmpeg ffmpeg-python freetype-py future gast google-auth google-auth-oauthlib google-pasta graphviz grpcio h5py idna imageio imageio-ffmpeg importlib-metadata ipykernel ipython ipython-genutils ipywidgets jedi Jinja2 joblib json5 jsonschema jupyter jupyter-client jupyter-console jupyter-core jupyterlab jupyterlab-server Keras Keras-Preprocessing kiwisolver language-selector lightgbm Markdown MarkupSafe matplotlib mistune moviepy mpmath murmurhash nbconvert nbformat netifaces networkx nltk nose notebook numexpr numpy nvidia-ml-py3 oauthlib opencv-python opt-einsum packaging pandas pandocfilters parso pexpect pickleshare Pillow pip plac plotly preshed proglog prometheus-client prompt-toolkit protobuf ptyprocess pyasn1 pyasn1-modules pycparser Pygments pygobject pyparsing pyrsistent python-apt python-dateutil python-debian pytz PyYAML pyzmq qtconsole QtPy regex requests requests-oauthlib retrying rsa scikit-learn scipy Send2Trash setuptools six soupsieve spacy srsly sympy tensorboard tensorboard-plugin-wit tensorboardX tensorflow-estimator tensorflow-gpu termcolor terminado testpath thinc threadpoolctl torch torchvision tornado tqdm traitlets transforms3d typing urllib3 vispy wasabi wcwidth webencodings Werkzeug wheel widgetsnbextension wrapt xgboost zipp
```
