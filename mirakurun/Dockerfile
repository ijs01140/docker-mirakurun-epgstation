FROM chinachu/mirakurun:latest
RUN apt-get update && \
    apt-get -y install git cmake libpcsclite1 libpcsclite-dev pkg-config && \
\
#libaribb25 build
    cd /tmp/ && git clone https://github.com/tsukumijima/libaribb25.git && \
    cd /tmp/libaribb25/ && \
    cmake -B build && \
    cd build && \
    make -j$(nproc) && \
    make install 
    