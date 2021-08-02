FROM debian:latest
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y gnupg2 wget
RUN apt-get install -y --no-install-recommends ssh sudo
RUN apt-get install -y dialog mercurial gcc-multilib git cmake g++
RUN apt-get install -y curl libunwind-dev nano
RUN apt-get install -y build-essential cmake git gnupg golang libpcre3-dev curl zlib1g-dev libcurl4-openssl-dev libssl-dev
RUN apt-get install -y pkg-config build-essential autoconf bison re2c libxml2-dev libsqlite3-dev
RUN apt-get install -y gcc-8-base apt-utils
RUN apt-get -y install puppet openssh-client
RUN useradd --create-home -s /bin/bash vagrant
RUN echo -n 'vagrant:vagrant' | chpasswd
RUN echo 'vagrant ALL = NOPASSWD: ALL' > /etc/sudoers.d/vagrant
RUN chmod 440 /etc/sudoers.d/vagrant
RUN mkdir -p /home/vagrant/.ssh
RUN chmod 700 /home/vagrant/.ssh
COPY vagrant.pub /home/vagrant/.ssh/authorized_keys
COPY vagrant.pub /root/.ssh/authorized_keys
RUN chmod 600 /home/vagrant/.ssh/authorized_keys
RUN chown -R vagrant:vagrant /home/vagrant/.ssh
RUN sed -i -e 's/Defaults.*requiretty/#&/' /etc/sudoers
RUN sed -i -e 's/\(UsePAM \)yes/\1 no/' /etc/ssh/sshd_config
RUN mkdir /var/run/sshd
RUN apt-get install -y aptitude nginx openssh-server python
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]