Code based on (https://github.com/wangteng0906/g2ww.git).
After modification, an alarm trigger metric is added to the message content.
# G2WW (Grafana 2 Wechat Work)
> Proxy Grafana Webhook alert to WeChat Work.

Grafana doesn't support push alert to WeChat Work(企业微信) by it's design, this is a small adapter for supporting this.


## Build g2ww

```
go build -o g2ww.linux *.go
```

Then g2ww will listen on `localhost:2408`, quite simple isn't it?

## Run g2ww

Run `g2ww` on server, it will listen on `http://127.0.0.1:2408` by default, keep it running in background (`systemd` or `screen`?).


## Let Nginx to proxy it

Like this:

```
server {
        listen 80;
        server_name localhost;

        location / {
            proxy_pass http://127.0.0.1:2408;
        }
}
```

## Create a Wechat Work Bot

Create a Wechat Work Bot and get the webhook address.

![](./img/ww-bot.png)

For instance, the webhook address is `https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=e28dde4c-1998-0002-0018-114514114514`.

## Configure Grafana

In the configuration above, we need to specify the address like this:

`https://IP:80/e28dde4c-1998-0002-0018-114514114514`

![](./img/grafana.png)

## Demo

![](./img/demo.png)

Quite simple, isn't it?
