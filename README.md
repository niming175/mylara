# mylara

### 容器介绍
#### 1、nginx  
  -- 挂载目录  
     配置文件 nginx/cong:挂载到容器的/etc/ngingx  
     项目文件 www 挂载到 /var/www  
  -- 端口  
      80  
      443   
#### 2、php-fpm （充当工作区）  
  --额外安装插件  
    1）composer  
    2）zlib1g-dev  
    3）zip   
    4）pdo_mysql  
    5）redis  
  -- 挂载目录  
    将项目中的www目录挂载到容器的/var/www下  
  --开放端口  
    9000  
#### 3、mysql  
  -- 初始化环境配置  
    MYSQL_DATABASE: blog  
    MYSQL_ROOT_PASSWORD: 123456  
    MYSQL_USER: niming175  
    MYSQL_PASSWORD: 123456  
  -- 目录挂载  
    data/mysql 挂载到容器的 /var/lib/mysql  
  -- 端口  
    3306  
#### 4、redis   
  -- 目录挂载  
    配置文件： redis/conf 挂载到 容器的etc/redis  
    数据：     data/redis 挂载到 容器的/data  
    
### 项目初始化
1、进入工作区（php-fpm充当工作区）  
  -- docker-compose exec php-fpm bash  
  -- ca /var/www/blog  
2、安装依赖  
  -- composer install  
3、修改配置文件  
  -- 相关配置已经预设好（.env配置）  
4、数据迁移  
  -- php artisan migrate  

### 测试

#### 1、项目运行  
  -- 用浏览器打开 http://localhost  
#### 2、数据库运行  
  -- 用浏览器进入网站（http://localhost）,点击redister  
  -- 注册用户  
  -- 提示注册成功 （失败则说明数据库或其他存在问题）  
  -- 退出后，点击login登录  
  -- 进入到mysql 容器，查看user表是否有注册的数据  
     *docker-composer exec mysql mysql -u niming175 -p123456  
     use blog   
     select * from users*  
#### 3、redis缓存  
  -- redis密码配置，进入redis 容器，查看keys * 提示需要密码（否则则配置存在问题）  
    docker-compose exec redis redis-cli  
    keys *  
  -- redis 密码登录  
     auth 123456 (我这里设的是123456)  
  -- 查看session  
    keys * （如果存在一条laravel开头的，则表示redis设置成功，前提是项目网站已经登录）  
