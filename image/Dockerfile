FROM ubuntu:16.04
WORKDIR /root

#Bug installing dependencies
#RUN touch /etc/init.d/systemd-logind
#
RUN apt-get update && apt-get -y install wget vim
RUN apt-get install -y git cmake  build-essential

RUN git clone https://gitlab.eurecom.fr/oai/openairinterface5g.git

RUN apt-get install -y libxml2-dev libxslt1-dev openssl libconfig-dev libssl-dev libopengm-dev nettle-dev

RUN apt-get install -y xmp libatlas-base-dev libyaml-dev ctags

#WORKDIR /tmp
#RUN df -lh
#RUN wget www.freediameter.net/hg/freeDiameter/archive/1.3.2.tar.gz -O - | tar xzf -
#WORKDIR ./freeDiameter-1.3.2
#RUN apt-get -y install cmake make gcc g++ bison flex libsctp-dev libgnutls-dev libgcrypt-dev libidn11-dev ssl-cert debhelper fakeroot libpq-dev libmysqlclient-dev libxml2-dev swig python-dev

WORKDIR ./openairinterface5g

RUN apt-get install -y sudo apt-utils

ADD build_helper.patch ./
RUN git apply build_helper.patch

SHELL ["/bin/bash", "-c"]
RUN source ./oaienv && ./maketags
RUN source ./oaienv && ./cmake_targets/build_oai -I

RUN source ./oaienv && ./cmake_targets/build_oai --phy_simulators

#RUN echo source $(pwd)/oaienv >> ~/.bashrc


#RUN echo hello

#RUN wget https://ufpr.dl.sourceforge.net/project/powerdevs/powerdevs_amd64_981.deb -O powerdevs_amd64.deb
#RUN dpkg -i /tmp/powerdevs_amd64.deb ; apt-get -yf install && dpkg -i powerdevs_amd64.deb
#RUN rm powerdevs_amd64.deb
#
#
#ENV DEBIAN_FRONTEND="teletype" \
#    LANG="en_US.UTF-8" \
#    LANGUAGE="en_US:en" \
#    LC_ALL="en_US.UTF-8" \
#    QT_X11_NO_MITSHM=1
#
#
##Install scilab backdoor
#RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
#RUN scilab-cli -e "atomsRepositoryDel('http://atoms.scilab.org/5.4'); atomsRepositoryAdd('http://atoms.scilab.org/5.5'); atomsInstall('BackDoor'); exit(0)"
#
##Fix bug on backdoor 0.2
#RUN mv /usr/share/scilab/contrib/BackDoor/0.2/etc/BackDoor.start  /usr/share/scilab/contrib/BackDoor/0.2/etc/backdoor.start
#
##RUN wget "https://atoms.scilab.org/toolboxes/BackDoor/0.2/files/BackDoor_0.2_5.5.bin.x86_64.linux.tar.gz"
##RUN tar xvzf BackDoor_0.2_5.5.bin.x86_64.linux.tar.gz
##RUN sed -i 's/Maintainer.*/Maintainer: Federico Bergero <fedebergero@gmail.com>/'  BackDoor_0.2/DESCRIPTION
##RUN tar cvzf BackDoor_0.2_5.5.bin.x86_64.linux.tar.gz BackDoor_0.2/
##RUN scilab-cli -e "atomsSetConfig('offline','True'); atomsInstall('/tmp/BackDoor_0.2_5.5.bin.x86_64.linux.tar.gz'); exit(0)"
##RUN mv /usr/share/scilab/contrib/BackDoor/0.2/etc/BackDoor.start  /usr/share/scilab/contrib/BackDoor/0.2/etc/backdoor.start
#
#
#RUN apt-get update && apt-get -y install gdb
