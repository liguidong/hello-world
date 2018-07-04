## Laravel学习笔记

> 仅仅记录学习过程中遇到的问题

#### 路由

1.新版的laravel路由从app中挪到了单独的/routes/目录

2.web.php中路由增加后访问404（MNMP）

查看nginx日志发现，他解析请求后进行了一个寻找目录的操作，当然挂了

根据laravel官方的解决方法：

nginx配置中增加以下即可

```nginx
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```

3.post请求路由在第三方工具测试时，需取消CSRF保护

``app/Http/Middleware/VerifyCsrfToken` `中设置排除路由

