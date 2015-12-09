FROM ubuntu:14.04
MAINTAINER Bradley J Chambers <brad.chambers@gmail.com>
ARG branch=master

RUN apt-get update && apt-get install -y --fix-missing --no-install-recommends \
    build-essential \
    ca-certificates \
    clang \
    cmake \
    git \
    libtiff4-dev \
    python-dev \
    python-numpy \
    wget \
    g++-4.8 \
    libboost-filesystem1.55-dev \
    libboost-iostreams1.55-dev \
    libboost-program-options1.55-dev \
    libboost-system1.55-dev \
    libboost-thread1.55-dev \
    libflann-dev \
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

RUN git clone https://github.com/hobu/hexer.git \
      	&& cd hexer \
      	&& mkdir build \
      	&& cd build \
      	&& cmake \
      		-DCMAKE_INSTALL_PREFIX=/usr \
      		-DCMAKE_BUILD_TYPE="Release" \
      		.. \
      	&& make \
      	&& make install \
        && cd / \
        && rm -rf hexer

RUN git clone https://github.com/CRREL/points2grid.git \
      	&& cd points2grid \
      	&& mkdir build \
      	&& cd build \
      	&& cmake \
      		-DCMAKE_INSTALL_PREFIX=/usr \
      		-DCMAKE_BUILD_TYPE="Release" \
      		.. \
      	&& make \
      	&& make install \
        && cd / \
        && rm -rf points2grid

RUN wget http://bitbucket.org/eigen/eigen/get/3.2.7.tar.gz \
        && tar -xvf 3.2.7.tar.gz \
        && cp -R eigen-eigen-b30b87236a1b/Eigen/ /usr/include/Eigen/ \
        && cp -R eigen-eigen-b30b87236a1b/unsupported/ /usr/include/unsupported/ \
        && cd / \
        && rm -rf eigen-eigen-b30b87236a1b

RUN git clone https://github.com/chambbj/pcl.git \
        && cd pcl \
        && git checkout pcl-1.7.2-sans-opengl \
        && mkdir build \
        && cd build \
        && cmake \
          -DBUILD_2d=ON \
          -DBUILD_CUDA=OFF \
          -DBUILD_GPU=OFF \
          -DBUILD_apps=OFF \
          -DBUILD_common=ON \
          -DBUILD_examples=OFF \
          -DBUILD_features=ON \
          -DBUILD_filters=ON \
          -DBUILD_geometry=ON \
          -DBUILD_global_tests=OFF \
          -DBUILD_io=ON \
          -DBUILD_kdtree=ON \
          -DBUILD_keypoints=ON \
          -DBUILD_ml=ON \
          -DBUILD_octree=ON \
          -DBUILD_outofcore=OFF \
          -DBUILD_people=OFF \
          -DBUILD_recognition=OFF \
          -DBUILD_registration=ON \
          -DBUILD_sample_concensus=ON \
          -DBUILD_search=ON \
          -DBUILD_segmentation=ON \
          -DBUILD_simulation=OFF \
          -DBUILD_stereo=OFF \
          -DBUILD_surface=ON \
          -DBUILD_surface_on_nurbs=OFF \
          -DBUILD_tools=OFF \
          -DBUILD_tracking=OFF \
          -DBUILD_visualization=OFF \
          -DWITH_LIBUSB=OFF \
          -DWITH_OPENNI=OFF \
          -DWITH_OPENNI2=OFF \
          -DWITH_FZAPI=OFF \
          -DWITH_PXCAPI=OFF \
          -DWITH_PNG=OFF \
          -DWITH_QHULL=OFF \
          -DWITH_QT=OFF \
          -DWITH_VTK=OFF \
          -DWITH_PCAP=OFF \
          -DCMAKE_INSTALL_PREFIX=/usr \
          -DCMAKE_BUILD_TYPE="Release" \
          .. \
        && make \
        && make install \
        && cd / \
        && rm -rf pcl

ENV CC clang
ENV CXX clang++

RUN git clone https://github.com/PDAL/PDAL \
        && cd PDAL \
        && git checkout ${branch} \
        && mkdir build \
        && cd build \
        && cmake \
          -DBUILD_PLUGIN_ATTRIBUTE=ON \
          -DBUILD_PLUGIN_CPD=OFF \
          -DBUILD_PLUGIN_GEOWAVE=OFF \
          -DBUILD_PLUGIN_GREYHOUND=ON \
          -DBUILD_PLUGIN_HEXBIN=ON \
          -DBUILD_PLUGIN_ICEBRIDGE=ON \
          -DBUILD_PLUGIN_MATLAB=OFF \
          -DBUILD_PLUGIN_MRSID=ON \
          -DBUILD_PLUGIN_NITF=ON \
          -DBUILD_PLUGIN_OCI=OFF \
          -DBUILD_PLUGIN_P2G=ON \
          -DBUILD_PLUGIN_PCL=ON \
          -DBUILD_PLUGIN_PGPOINTCLOUD=ON \
          -DBUILD_PLUGIN_SQLITE=ON \
          -DBUILD_PLUGIN_RIVLIB=OFF \
          -DBUILD_PLUGIN_PYTHON=ON \
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
