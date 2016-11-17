# Image:
# reg.dev.twleansw.com/leansw/gocd-server-base:16.11.0

FROM delitescere/jdk:1.8.0_72
ARG GO_VERSION=16.11.0-4185

# GoCD scripts used here work with ash -- bash not needed.  Only git support is bundled.
RUN apk --no-cache add git openssh

# Exposing volumes in a simple manner, and setup links behind-the-scenes to match GoCD's directory structure
# This requires some bootstrapping in alpine-start.sh
RUN mkdir -p /config/default /config/db /config/addons /config/plugins /artifacts /logs /var/lib/go-server/plugins /tmp && \
  ln -sf /artifacts /var/lib/go-server/artifacts && \
  # Link to /etc/go is likely unnecessary
  ln -sf /config /etc/go && \
  ln -sf /config /var/lib/go-server/config && \
  ln -sf /config/addons /var/lib/go-server/addons && \
  ln -sf /config/db /var/lib/go-server/db && \
  ln -sf /config/plugins /var/lib/go-server/plugins/external && \
  ln -sf /logs /var/log/go-server

VOLUME ["/config", "/artifacts", "/logs"]

EXPOSE 8153 8154

# Dockerized startup script.  Should work on more than Alpine, but YMMV.
COPY alpine-start.sh /start

CMD ["/start"]

# Download Go and install into a consistent directory. Disable daemonize.
WORKDIR /
LABEL cd.go.version=$GO_VERSION cd.go.server=""

# Using 'jar' because 'unzip' doesn't support stdin, and bsdtar is not available on Alpine
# Can't extract only specific files because we're working on stdin.
RUN chmod +x /start && \ 
    echo "Installing GoCD ${GO_VERSION}" && wget -qO- https://download.go.cd/binaries/$GO_VERSION/generic/go-server-$GO_VERSION.zip | jar xf /dev/stdin && \
    mv ./go-server-* ./go-server && sed -e 's/DAEMON=Y/DAEMON=N/' /go-server/go-server.default > /config/default/go-server && \
    rm -rf go-server-* /var/tmp/* /go-server/init.* /go-server/server.cmd /go-server/*.bat /go-server/*.sh /go-server/default.* /go-server/defaultFiles
