FROM nginx
COPY ./nginx/nginx.conf /etc/nginx/
COPY ./webserver.c /
COPY ./start.sh /
RUN apt-get update && \
    apt-get install -y gcc libfcgi-dev spawn-fcgi && \
    gcc -Wall -Werror -Wextra webserver.c -lfcgi -o server && \
    chmod +x /start.sh
ENTRYPOINT [ "/start.sh" ]