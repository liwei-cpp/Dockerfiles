FROM ubuntu:latest
USER root

RUN apt-get update && apt-get install --assume-yes git llvm python3 python3-dev python3-setuptools gcc libtinfo-dev zlib1g-dev build-essential cmake python3-pip

RUN cd /home && \
    git clone https://github.com/google/googletest && \
    cd googletest && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    make install

RUN cd /home && \
    git clone --recursive https://github.com/dmlc/tvm && \
    cd tvm && \
    mkdir build && \
    cat cmake/config.cmake | sed 's/USE_LLVM\sOFF/USE_LLVM ON/'> build/config.cmake && \
    echo 'set(USE_GTEST ON)' >> build/config.cmake && \
    cd build && \
    cmake .. && \
    make &&\
    make cpptest

RUN echo 'export TVM_HOME=/home/tvm' >> ~/.bashrc && \
    echo 'export PYTHONPATH=/home/tvm/python:/home/tvm/topi/python:/home/tvm/nnvm/python:\${PYTHONPATH}' >> ~/.bashrc

RUN pip3 install --user numpy decorator attrs && \
    pip3 install --user tornado && \
    pip3 install --user tornado psutil xgboost && \
    pip3 install --user mypy orderedset antlr4-python3-runtime

