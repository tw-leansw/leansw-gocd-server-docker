# Image:
# registry.aliyuncs.com/leansw/gocd-server:16.9.0

FROM registry.aliyuncs.com/leansw/gocd-server-base:16.9.0

ADD ./gocd-plugins/external/*.jar /var/lib/go-server/plugins/external/
ADD ./gocd-config/cruise-config.xml /etc/go/
ADD ./gocd-config/password.properties /var/go/
RUN chown -Rv go:go /var/go /etc/go /var/lib/go-server

CMD /sbin/my_init
