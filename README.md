 # laravel-blog
Vien Blog - 一款基于laravel5.8开发的，支持markdown编辑以及图片拖拽上传的博客系统、SEO友好

## 博客亮点

- 界面简洁、适配pc和mobile、有良好的视觉体验
- 支持markdown、并且可以拖拽或者粘贴上传图片、分屏实时预览
- SEO友好：支持自定义文章slug、支持meta title、description、keywords
- 自定义导航、自定义sidebar、随时去掉不需要的模块
- 支持标签、分类、置顶、分享、友链等博客基本属性
- 支持AdSense
- 支持百度自动提交链接和手动提交链接

##### 进入项目目录后，用`composer`安装依赖

```
composer install
```

##### 生成`.env`文件

```
cp .env.example .env
```

##### 生成key

```
php artisan key:generate
```

##### 创建MySQL数据库`vienblog` ，字符集采用 `utf8mb4`, `utf8mb4_general_ci`

##### 编辑`.env`文件 `vim .env`，修改MySQL数据库连接配置，请将`DB_HOST`，`DB_PORT`，`DB_USERNAME`，`DB_PASSWORD` 改成你的数据库配置。

```
[...]

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=vienblog
DB_USERNAME=root
DB_PASSWORD=root

[...]
```

##### 数据迁移和数据填充

```
php artisan migrate
php artisan db:seed
```
##### 创建storage软连接

```
php artisan storage:link
```

##### 设置目录权限

```
chmod -R 755 storage/
chown -R www-data:www-data  storage/
```

### 使用

可以选择临时预览，也可以用Nginx部署服务

#### 临时预览

```
php artisan serv
```

打开浏览器访问`127.0.0.1:8000`

#### 使用Nginx

Nginx配置，将`root`指向项目的`public`目录，请用`pwd` 查看目录，并且改成你目录，千万不要直接粘贴复制。

```
root   /app/laravel-blog/public;
```

完整配置

```
server {
        listen 8088 default_server;
        listen [::]:8088 default_server;
				
        root /apps/vien_blog/public;
        index index.php index.html index.htm;
        server_name _;
				
        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.2-fpm.sock; # fpm，因为版本不同路径会有区别，这里请改成你，不知道路径可以执行php-fpm便会显示
								# fastcgi_pass 127.0.0.1:9000; # cgi
        }
}
```

打开浏览器访问`127.0.0.1:8088`

#### 后台登录

- 地址`/admin`
- 默认的admin管理账号是`vien@byteinf.com`密码是`vienblog`，进入控制台后可以修改管理员信息

