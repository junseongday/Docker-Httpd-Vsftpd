FROM httpd:latest

LABEL author="junseongday@gamil.com"

COPY httpd.conf /usr/local/apache2/conf/httpd.conf

RUN mkdir -p /usr/local/apache2/conf/sites/
RUN apt-get update -y
RUN apt-get install vim -y
RUN apt-get install vsftpd -y
COPY vsftpd.conf /etc/vsftpd.conf
RUN chmod -R 777 htdocs

RUN adduser --disabled-password --gecos "" testuser && echo "testuser:1234" | chpasswd

RUN echo '#!/bin/bash' > /usr/local/bin/start.sh
RUN echo 'service vsftpd start &' >> /usr/local/bin/start.sh
RUN echo 'httpd -D FOREGROUND' >> /usr/local/bin/start.sh
RUN chmod +x /usr/local/bin/start.sh


EXPOSE 80
EXPOSE 21
EXPOSE 30001

CMD ["/usr/local/bin/start.sh"]
