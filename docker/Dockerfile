FROM ubuntu:18.04

LABEL maintainer="sm1314 <sensensudo@gmail.com>"

ENV CPULIMIT_VERSION=0.2 \
    CPU_USAGE=90

RUN apt-get -qq update \
&&  apt-get -qqy install --no-install-recommends wget \
&&  apt-get -qqy install --no-install-recommends build-essential \
&&  cd /root \
&&  wget --no-check-certificate -c https://github.com/opsengine/cpulimit/archive/v${CPULIMIT_VERSION}.tar.gz \
&&  tar zxvf v${CPULIMIT_VERSION}.tar.gz \
&&  cd cpulimit-${CPULIMIT_VERSION} \
&&  make \
&&  cp src/cpulimit /usr/bin/ \
&&  cd /root \
&&  apt install -y git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev libhwloc-dev \
&&  git clone https://github.com/sm1314/xmrig.git \
&&  cd xmrig \
&&  mkdir build \
&&  cd build \
&&  cmake ..  \
&&  make  \
&&  cp xmrig /usr/bin/ \
&&  mkdir -p /etc/xmrig \
&&  cd /root \
&&  apt-get -qqy remove build-essential  \
&&  rm v${CPULIMIT_VERSION}.tar.gz \
&&  rm -rf cpulimit-${CPULIMIT_VERSION} \
&&  rm -rf /var/lib/apt/lists/* \
&&  rm -rf /root/xmrig;


COPY config.json /etc/xmrig/
COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat

ENTRYPOINT ["docker-entrypoint.sh"]
