FROM ubuntu:24.04
LABEL maintainer="binge8 <cxwa28@163.com>"

RUN apt update && apt -y upgrade && \
    apt-get install -y --no-install-recommends \
    openssh-server cron curl vim ca-certificates

COPY scripts/init.sh /
RUN mkdir /var/run/sshd /var/run/cron && \
    echo 'root:root' |chpasswd && \
    sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22

ENTRYPOINT ["/init.sh"]
