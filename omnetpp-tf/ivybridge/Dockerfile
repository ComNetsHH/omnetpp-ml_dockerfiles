FROM ghcr.io/comnetshh/omnetpp-ml/omnetpp-tf-base:tf2.6.0-ivybridge as base
LABEL maintainer="Daniel Stolpmann <daniel.stolpmann@tuhh.de>"
LABEL org.opencontainers.image.description="Ubuntu based image derived from floopcz/tensorflow_cc:ubuntu containing a pre-built OMNeT++ distribution and TensorFlow for quickly compiling and running a model in Cmdenv (No IDE or Qtenv support!)"
LABEL org.opencontainers.image.licenses=""

# first stage - build omnet
FROM base as builder
ARG VERSION=5.6.2
WORKDIR /root
RUN wget https://github.com/omnetpp/omnetpp/releases/download/omnetpp-$VERSION/omnetpp-$VERSION-src-core.tgz \
         --referer=https://omnetpp.org/ -O omnetpp-src-core.tgz --progress=dot:giga && \
         tar xf omnetpp-src-core.tgz && rm omnetpp-src-core.tgz
RUN mv omnetpp-$VERSION omnetpp
WORKDIR /root/omnetpp
ENV PATH /root/omnetpp/bin:$PATH
# remove unused files and build
RUN ./configure WITH_QTENV=no WITH_OSG=no WITH_OSGEARTH=no && \
    make -j $(nproc) MODE=release base && \
    rm -r doc out test samples misc config.log config.status

# second stage - copy only the final binaries (to get rid of the 'out' folder and reduce the image size)
FROM base
ARG VERSION=5.6.2
ENV OPP_VER=$VERSION
RUN mkdir -p /root/omnetpp
WORKDIR /root/omnetpp
COPY --from=builder /root/omnetpp/ .
ENV PATH /root/omnetpp/bin:$PATH
RUN chmod 775 /root/ && \
    mkdir -p /root/models && \
    chmod 775 /root/models
WORKDIR /root/models
RUN echo 'PS1="omnetpp-tf2.6.0-$OPP_VER:\w\$ "' >> /root/.bashrc && chmod +x /root/.bashrc && \
    touch /root/.hushlogin
ENV HOME=/root/
CMD ["/bin/bash", "--init-file", "/root/.bashrc"]
