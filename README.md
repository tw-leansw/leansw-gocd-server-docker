# TW Leansw GoCD Server Dockerfile

Command to run the server:
```
docker run -d --restart=always --name=gocd-server \
    -l io.rancher.container.network=true \
    -p 8153:8153 -p 8154:8154 \
    reg.dev.twleansw.com/leansw/gocd-server:16.11.0
```
