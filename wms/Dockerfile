FROM opendatacube/datacube-core

RUN pip3 install \
    flask scikit-image gunicorn \
    && rm -rf $HOME/.cache/pip

RUN apt-get update && apt-get install -y \
    wget unzip \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp/code
RUN wget https://github.com/opendatacube/datacube-wms/archive/master.zip -O /tmp/dashboard.zip \
    && unzip /tmp/dashboard.zip \
    && mv /tmp/code/datacube-wms-master /code

WORKDIR /code

RUN python3 setup.py install

CMD gunicorn -b '0.0.0.0:8000' -w 1 --timeout 300 datacube_wms:wms
