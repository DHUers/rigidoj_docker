# VERSION 0.0.1
FROM ubuntu:14.04

MAINTAINER DHUers "https://github.com/DHUers"

RUN echo "debconf debconf/frontend select Teletype" | debconf-set-selections &&\
    # apt-get -y install fping &&\
    # sh -c "fping proxy && echo 'Acquire { Retries \"0\"; HTTP { Proxy \"http://proxy:3128\";}; };' > /etc/apt/apt.conf.d/40proxy || true" &&\
    apt-get -y update &&\
    apt-get -y install software-properties-common &&\
    # add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main universe" &&\
    # add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc)-updates main universe" &&\
    apt-get -y update &&\
    apt-mark hold initscripts &&\
    apt-get -y upgrade &&\
    add-apt-repository -y ppa:rwky/redis &&\
    add-apt-repository -y ppa:nginx/stable &&\
    add-apt-repository -y ppa:webupd8team/java &&\
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections &&\
    apt-get install -y curl && curl http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | apt-key add - &&\
    echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" | \
    tee /etc/apt/sources.list.d/postgres.list &&\
    curl https://www.rabbitmq.com/rabbitmq-signing-key-public.asc | apt-key add - &&\
    echo "deb http://www.rabbitmq.com/debian/ testing main" | \
    tee /etc/apt/sources.list.d/rabbitmq.list &&\
    apt-get -y update &&\
    apt-get -y install build-essential git curl wget \
                       libxslt-dev libcurl4-openssl-dev \
                       libssl-dev libyaml-dev libtool \
                       libxml2-dev gawk \
                       pngcrush imagemagick gifsicle \
                       postgresql-9.4 postgresql-client-9.4 \
                       postgresql-contrib-9.4 libpq-dev libreadline-dev \
                       nginx language-pack-en sudo cron \
                       psmisc rsyslog oracle-java7-installer rabbitmq-server clang &&\
    dpkg-divert --local --rename --add /sbin/initctl &&\
    sh -c "test -f /sbin/initctl || ln -s /bin/true /sbin/initctl" &&\
    apt-get -y install redis-server haproxy openssh-server &&\
    echo 'gem: --no-document' >> /usr/local/etc/gemrc &&\
    mkdir /src && cd /src && git clone https://github.com/sstephenson/ruby-build.git &&\
    cd /src/ruby-build && ./install.sh &&\
    cd / && rm -rf /src/ruby-build &&\
    # echo install_package "yaml-0.1.6" "http://pyyaml.org/download/libyaml/yaml-0.1.6.tar.gz#5fe00cda18ca5daeb43762b80c38e06e" --if needs_yaml > /src/2.1.2.discourse &&\
    echo install_package "yaml-0.1.6" "http://pyyaml.org/download/libyaml/yaml-0.1.6.tar.gz#5fe00cda18ca5daeb43762b80c38e06e" --if needs_yaml > /src/2.1.5 &&\
    # echo install_package "ruby-v_2_1_2_discourse" "https://github.com/SamSaffron/ruby/archive/v_2_1_2_discourse.tar.gz#98741e3cbfd00ae2931b2c0edb0f0698" ldflags_dirs standard verify_openssl >> /src/2.1.2.discourse &&\
    # echo install_package "ruby-2_1_5" "https://github.com/ruby/ruby/archive/v2_1_5.tar.gz#64aba0d56d5617e8c96e76a795ab8cc2" ldflags_dirs standard verify_openssl >> /src/2.1.5 &&\
    echo install_package "ruby-v2_1_5" "https://github.com/DHUers/ruby/releases/download/v2_1_5/ruby-2_1_5_rigidoj.tar.gz" ldflags_dirs standard verify_openssl >> /src/2.1.5 &&\
    # install_package "openssl-1.0.1l" "https://www.openssl.org/source/openssl-1.0.1l.tar.gz#b2cf4d48fe5d49f240c61c9e624193a6f232b5ed0baf010681e725963c40d1d4" mac_openssl --if has_broken_mac_openssl
    apt-get -y install ruby bison &&\
    # ruby-build /src/2.1.2.discourse /usr/local &&\
    # cd /src/2.1.5 && autoconf &&\
    ruby-build /src/2.1.5 /usr/local &&\
    apt-get -y remove ruby1.9.1 &&\
    gem update --system &&\
    gem install bundler &&\
    cd / && git clone https://github.com/SamSaffron/pups.git &&\
    mkdir /jemalloc && cd /jemalloc &&\
      wget http://www.canonware.com/download/jemalloc/jemalloc-3.4.1.tar.bz2 &&\
      tar -xjf jemalloc-3.4.1.tar.bz2 && cd jemalloc-3.4.1 && ./configure && make &&\
      mv lib/libjemalloc.so.1 /usr/lib && cd / && rm -rf /jemalloc &&\
    apt-get -y install runit monit socat &&\
    apt-get clean &&\
    rm -f /etc/apt/apt.conf.d/40proxy &&\
    locale-gen en_US &&\
    mkdir -p /etc/runit/1.d &&\
    wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      tar -xjf phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      rm phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      cp phantomjs-1.9.7-linux-x86_64/bin/phantomjs /bin/phantomjs &&\
      rm -fr phantomjs-1.9.7-linux-x86_64 &&\
    wget http://static.jonof.id.au/dl/kenutils/pngout-20130221-linux.tar.gz &&\
      tar -xf pngout-20130221-linux.tar.gz &&\
      rm pngout-20130221-linux.tar.gz &&\
      cp pngout-20130221-linux/x86_64/pngout /bin/pngout &&\
      rm -rf pngout-20130221-linux

ADD runit-1 /etc/runit/1
ADD runit-1.d-cleanup-pids /etc/runit/1.d/cleanup-pids
ADD runit-2 /etc/runit/2
