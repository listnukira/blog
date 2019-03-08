title: '[Hexo] hexo on nginx'
date: 2015-07-26 00:03:11
categories: Hexo
tags:
- Hexo
- Nginx
toc:false
---

記錄目前 Nginx 上關於 Hexo 的設定檔

<!-- more -->

## Configure file

設定檔以我的例子是放在 `/etc/nginx/sites-available/blog`

<pre>
server {
    return 404;
}

server {
    listen 80;
    listen [::]:443 ssl default_server;

    ssl_certificate /etc/letsencrypt/live/blog.listnukira.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/blog.listnukira.com/privkey.pem;

    root /home/listnukira/blog;
    server_name blog.listnukira.com;

    access_log  /var/log/nginx/blog_access.log;
    error_log   /var/log/nginx/blog_error.log;

    if ($scheme != "https") {
        return 301 https://$server_name$request_uri;
    }

    location ~* ^.+\.(ico|gif|jpg|jpeg|png)$ {
            root /home/listnukira/blog;
            access_log   off;
            expires      1d;
    }

    location ~* ^.+\.(css|js|txt|xml|swf|wav)$ {
        root /home/listnukira/blog;
        access_log   off;
        expires      10m;
    }

    location / {
        root /home/listnukira/blog;
        if (-f $request_filename) {
            rewrite ^/(.*)$  /$1 break;
        }
    }
}
</pre>

2018/08/30 修改 https 相關設定

