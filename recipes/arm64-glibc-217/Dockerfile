FROM centos:7

ARG GID=1045
ARG UID=1044

RUN groupadd --gid $GID node \
    && adduser --gid $GID --uid $UID node

# COPY cloudlinux.repo /etc/yum.repos.d/cloudlinux.repo

RUN ulimit -n 1024 \
    && yum install -y epel-release \
    && yum install -y centos-release-scl-rh \
    && yum upgrade -y \
    && yum install -y \
         git \
         curl \
         make \
         python2 \
         python3 \
         ccache \
         xz-utils \
         devtoolset-9 \
         glibc-devel

COPY --chown=node:node run.sh /home/node/run.sh

VOLUME /home/node/.ccache
VOLUME /out
VOLUME /home/node/node.tar.xz

USER node

ENTRYPOINT [ "/home/node/run.sh" ]
