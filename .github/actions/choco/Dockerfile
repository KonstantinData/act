FROM alpine:3.21

ARG CHOCOVERSION=1.1.0

RUN apk add --no-cache bash ca-certificates git \
  && apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community add mono mono-dev \
  && cert-sync /etc/ssl/certs/ca-certificates.crt \
  && wget "https://github.com/chocolatey/choco/archive/${CHOCOVERSION}.tar.gz" -O- | tar -xzf - \
  && cd choco-"${CHOCOVERSION}" \
  && chmod +x build.sh zip.sh \
  && ./build.sh -v \
  && mv ./code_drop/chocolatey/console /opt/chocolatey \
  && mkdir -p /opt/chocolatey/lib \
  && rm -rf /choco-"${CHOCOVERSION}" \
  && apk del mono-dev \
  && rm -rf /var/cache/apk/*

ENV ChocolateyInstall=/opt/chocolatey
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
