FROM centos/php-71-centos7

USER root

# Install Pygments for syntax highlighting
# Install nss_wrapper and openssh-server for SSH and Git
RUN yum install -y --setopt=tsflags=nodocs python-pygments openssh-server nss_wrapper ImageMagick rsyslog sudo sendmail && yum clean all -y

# Copy scripts
COPY ./scripts/ /opt/app-root/etc/

# Wrap Git and SSH to make nss_wrapper with with phd
COPY ./scripts/nss_wrapper /opt/app-root/bin/git
COPY ./scripts/nss_wrapper /opt/app-root/bin/ssh

# Custom SSH config
COPY ./sshd_config /etc/ssh/sshd_config
COPY ./sshd_env /etc/sysconfig/sshd
COPY ./scripts/phabricator-ssh-hook /usr/local/bin/phabricator-ssh-hook
COPY ./sudoers /etc/sudoers

# VCS user for repo hosting
RUN useradd -g 0 -u 1002 -M -d /opt/app-root/src -p NP -s /bin/sh repo

USER 1001
