FROM haproxy:2.2.4-alpine

COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

EXPOSE 8083 8086

COPY run.sh /bin/
RUN chmod +x /bin/run.sh

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["/bin/run.sh"]
