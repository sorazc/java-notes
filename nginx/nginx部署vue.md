# nginx部署vue

## Vue项目配置
### publicPath
默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上，例如 https://www.my-app.com/。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 https://www.my-app.com/my-app/，则设置 publicPath 为 /my-app/。

这个值在开发环境下同样生效。如果你想把开发服务器架设在根路径，你可以使用一个条件式的值：
```javascript
module.exports = {
  publicPath: process.env.NODE_ENV === 'production'
    ? '/production-sub-path/'
    : '/'
}
```
## nginx虚拟主机配置

```
server {
    listen       80;
    server_name  localhost;
    # 取消全局root配置
    # root   /usr/local/sixiucheng/codes;
    
    # 一级路径配置
    location / {
        # 取消全局root配置后 一级路径配置为root
        root   /usr/local/vue/front-ui/;
        # 针对vue项目历史模式的特定设置，详情自行参考https://router.vuejs.org/zh/guide/essentials/history-mode.html
        try_files $uri $uri/ @router;
        # 设置默认页
        index  index.html index.htm;
    }

    # 二级路径配置
    location /student { 
        # 二级路径要将root修改为alias
        alias   /usr/local/vue/back-ui/;
        try_files $uri $uri/ /backstage/index.html;
        index  index.html index.htm;
    }
    location @router {
        rewrite ^.*$ /index.html last;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   html;
    }
}
```