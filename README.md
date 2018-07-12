# Nginx-Docker-Miniprogram

微信小程序支持通过webview来内嵌网页，但是要求业务域名预先审核配置，就是说只能是你自己拥有的并且已经备案的域名。利用[Nginx]()做反向代理，可以利用符合要求的域名把请求转发到其他目标域名的网页。这个Demo同时使用了[Docker]()技术，开发者可以根据需求快速修改和部署。

## Demo
Demo演示了把 https://api.wecode.net.cn 请求转发到 https://www.fifaofficial.cn，其中包括一些静态资源的转发。同时，利用`sub_filter`替换html内的文本，使得不同的静态资源url替换成统一的域名。

## How to run
### 1. 配置Nginx
  * 配置文件
    Nginx的配置文件为`/conf/conf.d/default.conf`
  * 证书 
    把证书放到`/conf/certs/`目录下，并配置到`default.conf`的`ssl_certificate`和`ssl_certificate_key`

### 2. 运行Docker
  ``` bash
    docker container run \ 
    --rm \  
    --name mynginx \  
    --volume "$PWD/html":/usr/share/nginx/html \
    --volume "$PWD/conf":/etc/nginx \
    --volume "$PWD/logs":/var/log/nginx/ \
    -p 127.0.0.1:80:80 \
    -p 127.0.0.1:443:443 \
    -d \
    nginx
  ```