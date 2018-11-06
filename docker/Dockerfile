FROM alpine:edge

COPY build.sh /build.sh
RUN /build.sh

EXPOSE 8096 8920

ENV PUID=1000 PGID=1000

VOLUME /config 

HEALTHCHECK CMD curl -q http://localhost:8096/emby/system/info/public?format=json -O /dev/null || exit 1

ENTRYPOINT \
    chown $PUID:$PGID /config && \
    su-exec $PUID:$PGID \
        mono /emby/MediaBrowser.Server.Mono.exe \
        -programdata /config \
        -ffmpeg /usr/bin/ffmpeg \
        -ffprobe /usr/bin/ffprobe
