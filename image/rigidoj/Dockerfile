FROM dhuacm/rigidoj-docker:base

MAINTAINER DHUers "https://github.com/DHUers"

RUN useradd rigidoj -s /bin/bash -m -U &&\
    mkdir /var/www && cd /var/www &&\
     git clone https://github.com/DHUers/rigidoj.git &&\
     cd rigidoj &&\
     git remote set-branches --add origin tests-passed &&\
     cd .. &&\
     chown -R rigidoj:rigidoj /var/www/rigidoj &&\
    cd /var/www/rigidoj &&\
     sudo -u rigidoj RAILS4=1 bundle install --deployment \
         --without test --without development &&\
    cd /var/www/rigidoj/vendor/bundle &&\
       find . -name tmp -type d | xargs rm -rf && cd / &&\
      wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      tar -xjf phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      rm phantomjs-1.9.7-linux-x86_64.tar.bz2 &&\
      cp phantomjs-1.9.7-linux-x86_64/bin/phantomjs /bin/phantomjs &&\
      rm -fr phantomjs-1.9.7-linux-x86_64
