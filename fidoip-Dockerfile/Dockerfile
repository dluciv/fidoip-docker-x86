# FidoIP docker image

FROM f69m/ubuntu32:lts
MAINTAINER Dmitry V. Luciv <dluciv@dluciv.name>

# Basic setup

RUN apt-get -y update \
 && apt-get -y upgrade \
 && apt-get -y install screen \
 && useradd -G root -U -m -s /bin/bash fido \
 && mkdir -p /usr/local/etc \
 && echo 'export LANG=ru_RU.UTF-8' > /home/fido/.bashrc \
 && chown -R fido /home/fido \
 && chgrp -R fido /home/fido \
 && locale-gen ru_RU \
 && locale-gen ru_RU.UTF-8 \
 && locale-gen ru_RU.KOI8-R \
 && update-locale

# FidoIP installation

WORKDIR /root

RUN apt-get -y install build-essential unzip zip bzip2 libncurses5-dev gettext wget xutils screen texinfo

RUN wget 'http://downloads.sourceforge.net/project/fidoip/fidoip/1.0.5/fidoip-1.0.5_5-1.tar' \
 && tar -xpf fidoip-1.0.5_5-1.tar \
 && cd fidoip-1.0.5 \
 && rm fidoip_win-1.0.5_5-1.zip \
 && ./fido_linux.sh fido \
 && (echo 'Full Name\nStation Name\nLocation\n2:5030/1111.2222\nUplink Name\n2:5030/1111\nf1111.n5030.z2.binkp.net\nUplink Password\nn\ny' | ./setup_config.bash fido) \
 && ./relinkapps.sh \
 && ./set_perm.sh fido \
 && cd \
 && rm fidoip-1.0.5_5-1.tar \
 && apt-get clean

# Shell

CMD chmod g+rw /dev/console && /usr/bin/sudo -i -u fido

# Sharing

VOLUME /usr/local/etc /usr/local/bin /home/fido
