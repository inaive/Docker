FROM ubuntu:14.04
MAINTAINER Li Hao <lihao@me.com>
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y strongswan

RUN rm /etc/ipsec.conf
RUN rm /etc/ipsec.secrets

RUN mkdir /root/ipsec_cert && cd /root/ipsec_cert
ADD server_key.sh /root/ipsec_cert/
RUN chmod 775 /root/ipsec_cert/*.sh

WORKDIR /root/ipsec_cert/
RUN ./server_key.sh 45.62.113.32

RUN cp /root/ipsec_cert/cacerts/strongswanCert.pem /etc/ipsec.d/cacerts/strongswanCert.pem 
RUN cp /root/ipsec_cert/certs/vpnHostCert.pem /etc/ipsec.d/certs/vpnHostCert.pem
RUN cp /root/ipsec_cert/private/vpnHostKey.pem /etc/ipsec.d/private/vpnHostKey.pem

ADD ipsec.conf /etc/
ADD ipsec.secrets /etc/

RUN ipsec start

EXPOSE 500/udp 4500/udp

