FROM amazonlinux:2.0.20181010-with-sources

#
# Based on instructions from:
# http://www.jeramysingleton.com/install-erlang-and-elixir-on-centos-7-minimal/
#

# Setup and install build essentials
RUN set -xe \
  && yum -y update \
  && yum -y upgrade \
  && yum -y install gcc gcc-c++ glibc-devel make ncurses-devel openssl-devel autoconf java-1.8.0-openjdk-devel \
                    git wget tar gzip

# Install EPEl Release which is required by Erlang
RUN set -xe \
  && yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
  && yum -y install epel-release


# Install Erlang
RUN set -xe \
  && echo "# In /etc/yum.repos.d/rabbitmq-erlang.repo" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "[rabbitmq-erlang]" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "name=rabbitmq-erlang" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "baseurl=https://dl.bintray.com/rabbitmq/rpm/erlang/21/el/7" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "gpgcheck=1" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "gpgkey=https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "repo_gpgcheck=0" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && echo "enabled=1" >> /etc/yum.repos.d/rabbitmq-erlang.repo \
  && yum -y update \
  && yum -y install erlang

# elixir expects utf8.
# elixir expects utf8.
ENV ELIXIR_VERSION="v1.7.4" \
  LANG=C.UTF-8

RUN set -xe \
  && ELIXIR_DOWNLOAD_URL="https://github.com/elixir-lang/elixir/archive/${ELIXIR_VERSION}.tar.gz" \
  && ELIXIR_DOWNLOAD_SHA256="c7c87983e03a1dcf20078141a22355e88dadb26b53d3f3f98b9a9268687f9e20" \
  && curl -fSL -o elixir-src.tar.gz $ELIXIR_DOWNLOAD_URL \
  && echo "$ELIXIR_DOWNLOAD_SHA256  elixir-src.tar.gz" | sha256sum -c - \
  && mkdir -p /usr/local/src/elixir \
  && tar -xzC /usr/local/src/elixir --strip-components=1 -f elixir-src.tar.gz \
  && rm elixir-src.tar.gz \
  && cd /usr/local/src/elixir \
  && make install clean

CMD ["iex"]
