FROM nvidia/cuda:11.3.1-cudnn8-runtime-ubuntu20.04

ENV DEBIAN_FRONTEND noninteractive

ADD https://bootstrap.pypa.io/get-pip.py /tmp/get-pip.py

RUN set -e \
      && ln -sf /bin/bash /bin/sh

RUN set -e \
      && apt-get -y purge python3* \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        curl libfreetype6-dev libhdf5-dev libpng-dev libzmq3-dev locales \
        p7zip-full pandoc pbzip2 pigz pkg-config python3-dev \
        python3-distutils rsync texlive-fonts-recommended \
        texlive-plain-generic texlive-xetex texlive-xetex unzip \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && locale-gen en_US.UTF-8 \
      && update-locale

RUN set -e \
      && ln -sf /usr/bin/python3 /usr/bin/python \
      && /usr/bin/python /tmp/get-pip.py \
      && pip install -U --no-cache-dir \
        autopep8 bash_kernel cython feather-format flake8 flake8-bugbear \
        flake8-isort ggplot jupyter jupyter_contrib_nbextensions \
        jupyterthemes keras matplotlib pandas pep8-naming pip seaborn \
        tensorflow tqdm \
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
