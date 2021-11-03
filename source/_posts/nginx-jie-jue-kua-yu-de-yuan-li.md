---
title: 'Nginx 解决跨域的原理'
date: 2019-09-16 14:58:43
tags: []
published: true
hideInList: false
feature: 
---
>前端server域名为：`http://xx_domain`
>后端server域名为：`https://github.com`

`http://xx_domain` 对 `https://github.com` 发起请求一定会出现跨域

不过只需要启动一个nginx服务器，将server_name设置为`xx_domain`,然后设置相应的location以拦截前端需要跨域的请求，最后将请求代理回`github.com`。如下面的配置：
```
## 配置反向代理的参数
server {
    listen    8080;
    server_name xx_domain

    ## 1. 用户访问 http://xx_domain，则反向代理到 https://github.com
    location / {
        proxy_pass  https://github.com;
        proxy_redirect     off;
        proxy_set_header   Host             $host;        # 传递域名
        proxy_set_header   X-Real-IP        $remote_addr; # 传递ip
        proxy_set_header   X-Scheme         $scheme;      # 传递协议
        proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    }
}
```
这样可以完美绕过浏览器的同源策略：github.com访问nginx的github.com属于同源访问，而nginx对服务端转发的请求不会触发浏览器的同源策略。
```
http {
    include mime.types;
    server_tokens off;

    ## 配置反向代理的参数
    server {
        listen    8080;

        ## 1. 用户访问 http://ip:port，则反向代理到 https://github.com
        location / {
            proxy_pass  https://github.com;
            proxy_redirect     off;
            proxy_set_header   Host             $host;
            proxy_set_header   X-Real-IP        $remote_addr;
            proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
        }

        ## 2.用户访问 http://ip:port/README.md，则反向代理到
        ##   https://github.com/zibinli/blog/blob/master/README.md
        location /README.md {
            proxy_set_header  X-Real-IP  $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass https://github.com/zibinli/blog/blob/master/README.md;
        }
    }
}
```