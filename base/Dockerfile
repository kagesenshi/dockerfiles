FROM centos:7
ENV container docker
RUN yum update -y && yum install less systemd initscripts net-tools wget curl python python-devel openssh-clients openssh-server which nmap epel-release -y && yum install dnf -y && yum clean all
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
RUN systemctl disable network
RUN systemctl enable sshd 
RUN /usr/bin/ssh-keygen -A 
RUN echo "root:password" | chpasswd
RUN mkdir /root/.ssh/; chmod 0700 ~/.ssh/
ADD authorized_keys /root/.ssh/authorized_keys
RUN chmod -R 0600 /root/.ssh/authorized_keys
EXPOSE 22
VOLUME [ "/sys/fs/cgroup/" ]
CMD [ "/usr/sbin/init" ]
