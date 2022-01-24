FROM chinachu/mirakurun:latest
RUN apt update && \
    apt install -y git cmake libpcsclite1 libpcsclite-dev pkg-config && \
\
#libarib25(npm) uninstall
    unlink /opt/bin/arib-b25-stream-test && \
    npm uninstall arib-b25-stream-test && \
\
#libaribb25 build
    cd /tmp/ && git clone https://github.com/tsukumijima/libaribb25.git && \
    cd /tmp/libaribb25/ && \
    cmake -B build && \
    cd build && \
    make -j$(nproc) && \
    sudo make install 
    