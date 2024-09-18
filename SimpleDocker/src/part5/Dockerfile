FROM nginx:latest

COPY ./nginx/nginx.conf /etc/nginx/
COPY ./webserver.c /
COPY ./start.sh /

RUN apt-get update && \
    apt-get install -y gcc libfcgi-dev spawn-fcgi && \
    gcc /webserver.c -lfcgi -o server && \
    chmod 777 /var/cache/nginx/ /var/run/ && \
    chmod +x /start.sh && \
    chmod u-s /bin/su /usr/bin/newgrp \
      /usr/bin/passwd \
      /usr/bin/gpasswd \
      /usr/bin/chsh \
      /bin/mount \
      /bin/umount \
      /usr/bin/chfn && \
    chmod g-s /sbin/unix_chkpwd /usr/bin/chage \
      /usr/bin/expiry \
      /usr/bin/wall && \
    rm -rf /var/lib/apt/lists

USER nginx

ENTRYPOINT [ "/start.sh" ]
