# OpenSSH-enable-in-docker-container
FROM ubuntu:18.04
MAINTAINER shaily tomar
RUN apt-get update \
    && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:a' | chpasswd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' \
    /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional \
    pam_loginuid.so@g' -i /etc/pam.d/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]

now build the image 
# docker build .
and run the container 
# docker run -it --name ctr image_name
now
take the remote access of the container....... 
sudo ssh@citrIP
password

