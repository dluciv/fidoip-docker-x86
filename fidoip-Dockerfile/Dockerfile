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

# Timezone

ARG timezone=Europe/Moscow
RUN echo $timezone > /etc/timezone \
 && dpkg-reconfigure -f noninteractive tzdata

# FidoIP installation

WORKDIR /root

RUN apt-get -y install build-essential unzip zip bzip2 libncurses5-dev gettext wget xutils screen texinfo cvs

ADD no-cvs-login.patch /root/

RUN wget 'http://downloads.sourceforge.net/project/fidoip/fidoip/1.0.5/fidoip-1.0.5_5-1.tar' \
 && tar -xpf fidoip-1.0.5_5-1.tar \
 && patch -p0 -t < no-cvs-login.patch \
 && cd fidoip-1.0.5 \
 && ./fidoip-cvs-update.sh \
 && ./fido_linux.sh fido

# Template node setup

RUN cd fidoip-1.0.5 \
 && (echo 'Full Name\nStation Name\nLocation\n9:9999/1111.2222\nUplink Name\n9:9999/1111\nf1111.n5030.z2.binkp.net\nUplink Password\nn\ny' | ./setup_config.bash) \
 && ./relinkapps.sh \
 && ./set_perm.sh fido


# Shell

CMD chmod g+rw /dev/console && /usr/bin/sudo -i -u fido

# Cleanup

RUN apt-get -y purge --auto-remove build-essential cvs libncurses5-dev gcc \
 && apt-get clean

# Sharing

VOLUME /usr/local/etc /usr/local/bin /home/fido
