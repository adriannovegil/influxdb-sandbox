FROM alpine:3.7

COPY relay.toml /etc/relay.toml.tpl

COPY run.sh envtpl /bin/
RUN chmod +x /bin/envtpl
RUN chmod +x /bin/run.sh

RUN apk --update add pkgconf ncurses-terminfo ncurses-terminfo-base ncurses-libs readline bash && \
    apk --update --virtual build-deps add go>1.6 curl gcc git musl-dev make python && \
    export GOPATH=/go && \
    go get -v github.com/influxdata/influxdb-relay && \
    cd $GOPATH/src/github.com/influxdata/influxdb-relay && \
    python ./build.py && \
    chmod +x ./build/influx* && \
    ls -l ./build/* && \
    mv ./build/influx* /bin/ && \
    apk del build-deps && cd / && rm -rf $GOPATH/ /var/cache/apk/*

EXPOSE 9096

ENTRYPOINT ["/bin/sh"]

CMD ["/bin/run.sh"]
