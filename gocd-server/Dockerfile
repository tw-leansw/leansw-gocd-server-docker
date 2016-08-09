FROM gocd/gocd-server:16.7.0

ADD ./gocd-plugins/external/*.jar /var/lib/go-server/plugins/external/
ADD ./gocd-config/cruise-config.xml /etc/go/
ADD ./gocd-config/password.properties /var/go/
CMD chown -Rv go:go /var/go && chown -Rv go:go /etc/go && chown -Rv go:go /var/lib/go-server  && /sbin/my_init 


