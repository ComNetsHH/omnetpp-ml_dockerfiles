FROM floopcz/tensorflow_cc:ubuntu-2.6.0
LABEL maintainer="Daniel Stolpmann <daniel.stolpmann@tuhh.de>"
LABEL org.opencontainers.image.description="Ubuntu based image derived from floopcz/tensorflow_cc:ubuntu containing TensorFlow and all required packages to build and use OMNeT++ on the command line (clang compiler, make etc.)"
LABEL org.opencontainers.image.licenses=""

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends git wget curl make ca-certificates bison flex clang perl python3 libxml2-dev libavcodec-dev libavformat-dev  libavutil-dev libavresample-dev libfl-dev libpcap-dev libprotobuf-dev && \
    apt-get clean && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 1 && \
    rm -rf /var/lib/apt/lists/*
