FROM cockpit/infra-base
LABEL maintainer='cockpit-devel@lists.fedorahosted.org'

RUN dnf -y update && \
    dnf -y install lighttpd && \
    dnf clean all

RUN mkdir -p /usr/local/bin && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \
    rm -rf /usr/share/nginx/html && \
    ln -snf /cache/images /usr/share/nginx/html && \
    chown -R user /home/user

COPY install-service /usr/local/bin/
COPY nginx.conf /etc/nginx/

VOLUME /secrets /cache

EXPOSE 8080 8443
STOPSIGNAL SIGQUIT
CMD /usr/sbin/nginx -g "daemon off;"

