FROM pytorch/pytorch:latest

ENV WORKDIR=/workspaces

WORKDIR ${WORKDIR}
RUN git clone https://github.com/kakao/khaiii.git

WORKDIR ${WORKDIR}/khaiii
RUN pip install cython
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

RUN mkdir build
WORKDIR ${WORKDIR}/khaiii/build

RUN cmake ..
RUN make all
RUN make resource

RUN apt-get update -y
RUN apt-get install -y language-pack-ko
RUN locale-gen en_US.UTF-8
RUN update-locale LANG=en_US.UTF-8

WORKDIR ${WORKDIR}/khaiii/build

RUN make package_python
WORKDIR ${WORKDIR}/khaiii/build/package_python
RUN pip install .

WORKDIR /
RUN rm -rf /workspaces
RUN rm -rf /workspace