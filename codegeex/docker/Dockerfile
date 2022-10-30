FROM python:3.8.15

RUN pip install --upgrade pip

RUN apt-get update
RUN apt-get install -y curl npm git vim tar
RUN apt-get install -y build-essential g++

RUN mkdir -p /workspace/download

# Go
RUN curl -o /workspace/download/go.tar.gz -SL https://go.dev/dl/go1.18.4.linux-amd64.tar.gz \
    && tar -zxf /workspace/download/go.tar.gz -C /usr/local && rm /workspace/download/go.tar.gz
ENV PATH=/bin:/usr/local/go/bin:$PATH

# JavaScript
RUN curl -o /workspace/download/node.tar.gz -SL https://nodejs.org/download/release/v16.14.0/node-v16.14.0-linux-x64.tar.gz \
    && mkdir -p /usr/local/lib/nodejs && tar -zxf /workspace/download/node.tar.gz -C /usr/local/lib/nodejs && mv /usr/local/lib/nodejs/node-v16.14.0-linux-x64 /usr/local/lib/nodejs/node \
    && rm /workspace/download/node.tar.gz && npm install -g js-md5@0.7.3
ENV PATH=/usr/local/lib/nodejs/node/bin:$PATH
ENV NODE_PATH=/usr/local/lib/node_modules

# Boost
RUN curl -o /workspace/download/boost_1_71_0.tar.gz -SL https://boostorg.jfrog.io/artifactory/main/release/1.71.0/source/boost_1_71_0.tar.gz \
    && tar -zxf /workspace/download/boost_1_71_0.tar.gz && rm /workspace/download/boost_1_71_0.tar.gz && cd boost_1_71_0 \
    && ./bootstrap.sh --prefix=/usr/ && ./b2 && ./b2 install \
    && cd .. && rm -r boost_1_71_0

# OpenSSL
RUN curl -o /workspace/download/openssl.tar.gz -SL https://www.openssl.org/source/old/3.0/openssl-3.0.0.tar.gz \
    && tar -zxf /workspace/download/openssl.tar.gz && rm /workspace/download/openssl.tar.gz && cd openssl-3.0.0 \
    && ./Configure && make && make install \
    && cd .. && rm -r openssl-3.0.0
ENV PATH=/usr/bin/openssl:$PATH

# Java
RUN curl -o /workspace/download/jdk.tar.gz -SL https://download.oracle.com/java/18/archive/jdk-18.0.2.1_linux-x64_bin.tar.gz \
    && mkdir /usr/java && tar -zxf /workspace/download/jdk.tar.gz -C /usr/java && rm /workspace/download/jdk.tar.gz

ENV JAVA_HOME=/usr/java/jdk-18.0.2.1
RUN update-alternatives --install /usr/bin/java java $JAVA_HOME/bin/java 20000 \
    && update-alternatives --install /usr/bin/javac javac $JAVA_HOME/bin/javac 20000 \
    && rm -r /workspace/download \
    && env

# HumanEvalX
RUN git clone https://github.com/mitya52/CodeGeeX.git /workspace/CodeGeeX && pip install -e /workspace/CodeGeeX

CMD ["bash"]