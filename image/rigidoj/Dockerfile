FROM dhuacm/rigidoj-docker:base

MAINTAINER DHUers "https://github.com/DHUers"

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
    useradd rigidjudge -s /bin/bash -m -U &&\
    cd /var &&\
     curl -s https://api.github.com/repos/DHUers/RigidJudge/releases/latest |\
      grep browser_download_url | head -n 1 | cut -d '"' -f 4 |\
      wget -i - -O RigidJudge.tar &&\
     tar -xf RigidJudge.zip &&\
     rm RigidJudge.zip &&\
     chown -R rigidjudge:rigidjudge /var/RigidJudge &&\
    cd /var/RigidJudge/bin/sandbox &&\
     make clean && make all
