FROM ubuntu:14.04
MAINTAINER Bradley J Chambers <brad.chambers@gmail.com>
ARG branch=master

RUN apt-get update && apt-get install -y --fix-missing --no-install-recommends \
    ca-certificates \
    gdal-bin \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["gdaldem"]
CMD ["-h"]
