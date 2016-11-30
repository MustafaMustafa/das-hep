# Build DESI software environment ontop an Ubuntu base
FROM ubuntu:16.04
MAINTAINER Mustafa Mustafa <mmustafa@lbl.gov>

# install astrometry and tractor dependencies
RUN apt-get update && \
    apt-get install -y wget make git python python-dev python-matplotlib gcc swig\
                       python-numpy libgsl2 gsl-bin pkg-config zlib1g-dev libcairo2-dev \
                       libnetpbm10-dev netpbm libpng12-dev libjpeg-dev python-pyfits \
                       zlib1g-dev libbz2-dev libcfitsio3-dev python-photutils python-pip && \
    pip install fitsio

# ------- install astrometry
RUN mkdir -p /desi_software/astrometry_net && \
    git clone https://github.com/dstndstn/astrometry.net.git && \
    cd astrometry.net && \
    make install INSTALL_DIR=/desi_software/astrometry_net &&\
    cd / && \
    rm -rf astrometry.net

ENV PYTHONPATH /desi_software/astrometry_net/lib/python:$PYTHONPATH
ENV PATH /desi_software/astrometry_net/lib/python/astrometry/util:$PATH
ENV PATH /desi_software/astrometry_net/lib/python/astrometry/blind:$PATH

# ------- install tractor
RUN mkdir -p /desi_software/tractor && \
    git clone https://github.com/dstndstn/tractor.git && \
    cd tractor && \
    make && \
    python setup.py install --prefix=/desi_software/tractor/

ENV PYTHONPATH /desi_software/tractor/lib/python2.7/site-packages:$PYTHONPATH

# ------- install missing GalSim dependencies (others have been installed above)
RUN apt-get install -y python-future python-yaml python-pandas scons fftw3-dev libboost-all-dev

# ------- install TMV
RUN wget https://github.com/rmjarvis/tmv/archive/v0.73.tar.gz -O tmv.tar.gz && \
    gunzip tmv.tar.gz && \
    mkdir tmv && tar xf tmv.tar -C tmv --strip-components 1 && \
    cd tmv && \
    scons && \
    scons install && \
    cd / && \
    rm -rf tmv.tar tmv

# ------- install GalSim
RUN wget https://github.com/GalSim-developers/GalSim/archive/v1.4.2.tar.gz -O GalSim.tar.gz && \
    gunzip GalSim.tar.gz && \
    mkdir GalSim && tar xf GalSim.tar -C GalSim --strip-components 1 && \
    cd GalSim && \
    scons && \
    scons install && \
    cd / && \
    rm -rf GalSim.tar GalSim
