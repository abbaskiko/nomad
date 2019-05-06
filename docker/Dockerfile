FROM debian:9.8

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y curl \
  && rm -rf /var/lib/apt/lists/*

# ENV NOMAD_VERSION=0.5.6-drain-patch-05 \
#     NOMAD_SHA256=aec3a73af95b0d11a9585bb481e30c909a93ea8d16390069f0af6a35a9965783

# RUN curl -o /tmp/nomad.zip https://s3.amazonaws.com/circle-downloads/nomad_$NOMAD_VERSION.linux_amd64.zip \
#       && echo "${NOMAD_SHA256}  /tmp/nomad.zip" | sha256sum -c \
#       && unzip -d /usr/bin /tmp/nomad.zip \
#       && rm /tmp/nomad.zip
ADD pkg/linux_amd64/nomad /usr/bin/nomad

ADD default.hcl /usr/local/etc/nomad/default.hcl
COPY client.hcl /etc/nomad/client.hcl
COPY default.hcl /etc/nomad/default.hcl
COPY server.hcl /etc/nomad/server.hcl
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+x /docker-entrypoint.sh

VOLUME ["/opt/nomad"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["start"]
