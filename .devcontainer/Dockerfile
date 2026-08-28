FROM debian:12

# Install build dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        g++ \
        gfortran \
        make \
        automake \
        autoconf \
        bzip2 \
        unzip \
        wget \
        curl \
        sox \
        libtool \
        git \
        python3 \
        python3-pip \
        zlib1g-dev \
        ca-certificates \
        patch \
        python-is-python3 && \
    rm -rf /var/lib/apt/lists/*

# Clone and compile Kaldi (or you can mount your own)
RUN git clone --depth 1 https://github.com/kaldi-asr/kaldi.git /opt/kaldi && \
    cd /opt/kaldi/tools && \
    ./extras/install_openblas.sh && \
    make -j $(nproc) && \
    cd /opt/kaldi/src && \
    ./configure --shared --mathlib=OPENBLAS && \
    make depend -j $(nproc) && \
    make -j $(nproc)

WORKDIR /workspace
