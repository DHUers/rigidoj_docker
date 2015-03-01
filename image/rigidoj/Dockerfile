FROM dhuacm/rigidoj-docker:base

MAINTAINER DHUers "https://github.com/DHUers"

RUN gcc --version &&\
    g++ --version &&\
    clang --version &&\
    javac -version

RUN useradd rigidoj -s /bin/bash -m -U &&\
    cd /var/www &&\
     git clone https://github.com/DHUers/rigidoj.git &&\
     chown -R rigidoj:rigidoj /var/www/rigidoj &&\
    cd /var/www/rigidoj &&\
     sudo -u rigidoj RAILS4=1 bundle install --deployment \
         --without test --without development &&\
    cd /var/www/rigidoj/vendor/bundle &&\
       find . -name tmp -type d | xargs rm -rf && cd / &&\
    # RigidJudge
    useradd rigidjudge -s /bin/bash -m -U
