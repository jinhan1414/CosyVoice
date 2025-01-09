FROM pytorch/pytorch:2.0.1-cuda11.7-cudnn8-runtime
ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /opt/CosyVoice

RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get -y install git unzip git-lfs
RUN git lfs install
RUN git clone --recursive https://github.com/jinhan1414/CosyVoice.git

# 安装Flask
RUN pip install flask

# 这里使用 python==3.10 是因为找不到同时支持 python3.8 和 torch2.0.1-cu118 的镜像
RUN cd CosyVoice && pip3 install -r requirements.txt

# 克隆预训练模型并安装相关依赖
RUN git clone https://www.modelscope.cn/iic/CosyVoice-ttsfrd.git pretrained_models/CosyVoice-ttsfrd
WORKDIR pretrained_models/CosyVoice-ttsfrd
RUN unzip resource.zip -d .
RUN pip install ttsfrd_dependency-0.1-py3-none-any.whl
RUN pip install ttsfrd-0.4.2-cp310-cp310-linux_x86_64.whl
