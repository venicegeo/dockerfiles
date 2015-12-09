FROM ubuntu:14.04
MAINTAINER Bradley J Chambers <brad.chambers@gmail.com>
ARG branch=master

RUN apt-get update && apt-get install -y --fix-missing --no-install-recommends \
    build-essential \
    ca-certificates \
    cmake \
    git \
    libtiff4-dev \
    wget \
    g++-4.8 \
    libboost-filesystem1.55-dev \
    libboost-iostreams1.55-dev \
    libboost-program-options1.55-dev \
    libboost-system1.55-dev \
    libboost-thread1.55-dev \
    libgdal1h \
    libgdal-dev \
    gdal-bin \
    libgeos++-dev \
    libproj-dev \
    libgeotiff-dev \
    libxml2-dev \
  && rm -rf /var/lib/apt/lists/* \
  && wget http://www.liblas.org/samples/autzen/autzen.laz

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50

RUN git clone https://github.com/hobu/nitro \
        && cd nitro \
        && mkdir build \
        && cd build \
        && cmake \
          -DCMAKE_INSTALL_PREFIX=/usr \
          .. \
        && make \
        && make install \
        && cd / \
        && rm -rf nitro

RUN git clone https://github.com/LASzip/LASzip.git laszip \
        && cd laszip \
        && mkdir build \
        && cd build \
        && cmake \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DCMAKE_BUILD_TYPE="Release" \
          .. \
        && make \
        && make install \
        && cd / \
        && rm -rf laszip

RUN git clone  https://github.com/verma/laz-perf.git \
        && cd laz-perf \
        && mkdir build \
        && cd build \
        && cmake \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DCMAKE_BUILD_TYPE="Release" \
          .. \
        && make \
        && make install \
        && cd / \
        && rm -rf laz-perf

RUN git clone https://github.com/PDAL/PDAL \
        && cd PDAL \
        && git checkout ${branch} \
        && mkdir build \
        && cd build \
        && cmake \
          -DBUILD_PLUGIN_ATTRIBUTE=OFF \
          -DBUILD_PLUGIN_CPD=OFF \
          -DBUILD_PLUGIN_GEOWAVE=OFF \
          -DBUILD_PLUGIN_GREYHOUND=OFF \
          -DBUILD_PLUGIN_HEXBIN=OFF \
          -DBUILD_PLUGIN_ICEBRIDGE=OFF \
          -DBUILD_PLUGIN_MATLAB=OFF \
          -DBUILD_PLUGIN_MRSID=OFF \
          -DBUILD_PLUGIN_NITF=ON \
          -DBUILD_PLUGIN_OCI=OFF \
          -DBUILD_PLUGIN_P2G=OFF \
          -DBUILD_PLUGIN_PCL=OFF \
          -DBUILD_PLUGIN_PGPOINTCLOUD=OFF \
          -DBUILD_PLUGIN_SQLITE=OFF \
          -DBUILD_PLUGIN_RIVLIB=OFF \
          -DBUILD_PLUGIN_PYTHON=OFF \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DENABLE_CTEST=OFF \
          -DWITH_APPS=ON \
          -DWITH_LAZPERF=ON \
          -DWITH_GEOTIFF=ON \
          -DWITH_LASZIP=ON \
          -DWITH_TESTS=OFF \
          .. \
        && make -j4 \
        && make install \
        && cd / \
        && rm -rf PDAL

ENTRYPOINT ["pdal"]
CMD ["-h"]
