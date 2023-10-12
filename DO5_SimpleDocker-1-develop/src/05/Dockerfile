FROM nginx:latest

COPY ./run.sh /run.sh
COPY ./main.c /main.c
COPY ./nginx.conf /etc/nginx/nginx.conf

RUN \
    # useradd -d /home/dockle -m -s /bin/bash dockle \
    # USER dockle && \
    # next 4 lines for part6
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid && \
    chown -R nginx:nginx /var/log/nginx && \
    chown -R nginx:nginx /var/cache/nginx && \
    # chmod lines for dockle
    chmod 777 bin/su && \
    chmod 777 bin/mount && \
    chmod 777 usr/bin/wall && \
    chmod 777 usr/bin/gpasswd && \
    chmod 777 sbin/unix_chkpwd && \
    chmod 777 bin/umount && \
    chmod 777 usr/bin/newgrp && \
    chmod 777 usr/bin/chage && \
    chmod 777 usr/bin/chfn && \
    chmod 777 usr/bin/passwd && \
    chmod 777 usr/bin/expiry && \
    chmod 777 usr/bin/chsh && \
    apt update && \
    apt install -y spawn-fcgi && \
    apt install -y libfcgi-dev && \
    apt install -y gcc && \
    # next line for dockle too
    rm -rf /var/lib/apt/lists && \
    chmod 777 run.sh

#USER nginx
HEALTHCHECK NONE
ENTRYPOINT ["/run.sh"]