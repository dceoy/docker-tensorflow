FROM nvidia/cuda:9.0-cudnn7-runtime

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y purge python3* \
      && apt-get -y update \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        software-properties-common \
      && add-apt-repository -y ppa:jonathonf/python-3.6 \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        build-essential curl libfreetype6-dev libhdf5-dev libpng12-dev \
        libzmq3-dev p7zip-full pbzip2 pigz pkg-config python3.6-dev rsync \
        unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && ln -sf /usr/bin/python3.6 /usr/bin/python \
      && ln -sf /usr/bin/python3.6 /usr/bin/python3 \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir \
        autopep8 bash_kernel cython feather-format flake8 ggplot jupyter \
        jupyter_contrib_nbextensions jupyterthemes keras matplotlib pandas \
        pip seaborn tensorflow-gpu tqdm \
      && rm -f /tmp/get-pip.py

ENV HOME /home/notebook

RUN set -e \
      && mkdir ${HOME} \
      && /usr/bin/python -m bash_kernel.install \
      && jupyter contrib nbextension install --system \
      && jt --theme oceans16 --toolbar --nbname --vimext \
      && find ${HOME} -exec chmod 777 {} \;

EXPOSE 6006
EXPOSE 8888

ENTRYPOINT ["jupyter"]
CMD ["notebook", "--port=8888", "--ip=0.0.0.0", "--allow-root", "--no-browser"]