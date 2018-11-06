FROM alpine:edge

COPY build.sh /build.sh
RUN /build.sh

EXPOSE 8096 8920

ENV PUID=1000 PGID=1000

VOLUME /config /opt/media

HEALTHCHECK CMD wget -q http://localhost:8096/swagger -O /dev/null || exit 1

ENTRYPOINT \
    chown $PUID:$PGID /config /opt/media && \
    su-exec $PUID:$PGID \
        mono /emby/MediaBrowser.Server.Mono.exe \
        -programdata /config \
        -ffmpeg /usr/bin/ffmpeg \
        -ffprobe /usr/bin/ffprobe
