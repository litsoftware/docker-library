FROM nginx:latest

RUN addgroup nobody tty

RUN chgrp -R 0 /etc/nginx/ /var/cache/nginx /var/run /var/log/nginx  && \ 
    chmod -R g+rwX /etc/nginx/ /var/cache/nginx /var/run /var/log/nginx

# Install latest su-exec
RUN  set -ex; \
    \
    curl -o /usr/local/bin/su-exec.c https://raw.githubusercontent.com/ncopa/su-exec/master/su-exec.c; \
    \
    fetch_deps='gcc libc-dev'; \
    apt-get update; \
    apt-get install -y --no-install-recommends $fetch_deps; \
    rm -rf /var/lib/apt/lists/*; \
    gcc -Wall \
    /usr/local/bin/su-exec.c -o/usr/local/bin/su-exec; \
    chown root:root /usr/local/bin/su-exec; \
    chmod 0755 /usr/local/bin/su-exec; \
    rm /usr/local/bin/su-exec.c; \
    \
    apt-get purge -y --auto-remove $fetch_deps

COPY ./conf/site.conf /etc/nginx/conf.d/site.conf

# CMD [ "su-exec", "nobody", "nginx", "-g", "daemon off;"]
