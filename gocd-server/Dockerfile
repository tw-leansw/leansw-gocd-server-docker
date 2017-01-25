# Image:
# reg.dev.twleansw.com/leansw/gocd-server:16.11.0
# Usage:
# docker run -d -p 8153:8153 -p 8154:8154 <image-name:tag>

FROM reg.dev.twleansw.com/leansw/gocd-server-base:16.11.0

ADD ./gocd-plugins/external/*.jar /var/lib/go-server/plugins/external/
ADD ./gocd-config/gocd-server-config.xml /etc/go/
ADD ./gocd-config/password.properties /var/go/
