# Laravel-Nginx-404
http://wenda.golaravel.com/question/324

把整个项目复制到 /usr/share/nginx/html 后，修改 app/storage 权限为 777，然后浏览器访问 / 可以访问，但除了 / 路由其他路由全部返回 404，比如 /home 返回 404 NOT FOUND，而在开发时是没有这些问题的。数据库这些都没问题，因为开发是在同一台机上。


server {

listen 8040;

server_name yourdomain.com;

root /path/to/your/laravel/project/public;

index index.html index.php;
location / {
    try_files $uri $uri/ /index.php$is_args$query_string;
  }
location ~ \.php$ {

    try_files $uri =404;

    fastcgi_pass 127.0.0.1:9000;

    fastcgi_index index.php;

    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

    include fastcgi_params;

}

}
