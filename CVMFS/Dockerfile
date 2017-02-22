FROM opensuse:42.1
MAINTAINER Mustafa Mustafa <mmustafa@lbl.gov>

RUN zypper install -y wget \
                      tar  \
                      gcc  \
                      gcc-c++  \
                      patch  \
                      cmake  \
                      zlib-devel  \
                      libattr-devel  \
                      valgrind  \
                      valgrind-devel  \
                      libopenssl-devel  \
                      libuuid-devel  \
                      libuuid1  \
                      fuse  \
                      fuse-devel  \
                      python  \
                      python-devel  \
                      libpcap  \
                      libpcap-devel  \
                      libcap  \
                      libcap-devel  \
                      unzip

RUN mkdir cvmfs_install && \
    cd cvmfs_install && \
    wget https://ecsft.cern.ch/dist/cvmfs/cvmfs-2.3.3/source.tar.gz && \
    tar -xf source.tar.gz && \
    cd cvmfs-2.3.3 && \
    cmake . && \
    make && \
    make install
