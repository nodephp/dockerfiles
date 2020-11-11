FROM ubuntu

RUN apt-get update && apt-get install -y subversion 
RUN apt-get update && apt-get install -y libsasl2-modules-ldap sasl2-bin
RUN sed  -i 's/MECHANISMS="pam"/MECHANISMS="ldap"/g'  /etc/default/saslauthd
RUN sed  -i 's/START=no/START=yes/g'  /etc/default/saslauthd
COPY  saslauthd.conf /etc/saslauthd.conf 
COPY  svn.conf /usr/lib/sasl2/svn.conf

RUN echo "service saslauthd restart\n/usr/bin/svnserve --daemon --foreground --root /opt/svn" >/root/svn.sh
CMD ["/bin/sh","/root/svn.sh"]

EXPOSE 3690
WORKDIR /opt/svn

