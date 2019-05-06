FROM debian:9.8

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y curl \
  && rm -rf /var/lib/apt/lists/*

ADD pkg/linux_amd64/nomad /usr/bin/nomad

ADD docker/default.hcl /usr/local/etc/nomad/default.hcl
COPY docker/client.hcl /etc/nomad/client.hcl
COPY docker/default.hcl /etc/nomad/default.hcl
COPY docker/server.hcl /etc/nomad/server.hcl
COPY docker/docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod a+x /docker-entrypoint.sh

VOLUME ["/opt/nomad"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["start"]
