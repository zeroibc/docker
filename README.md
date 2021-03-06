# docker搭建laravel开发环境

### **1、pull拉取git<br>**

### **2、进入到dockers文件夹<br>**
`cd dockers`<br>

### **3、build一个镜像<br>**
`docker build -t chensk/php5.6` .<br>

### **4、执行`docker-composer up -d` 启动容器,启动容器前先打开docker-composer.yml文件修改mysql容器的environment<br>**

### **5、`docker ps` 查看启动的容器，并找到php的容器id,执行下面的命令，进入到php容器内部<br>**
`docker exec -it php的容器id /bin/bash`

### **6、在宿主机挂在的目录中，执行下面的命令安装laravel** <br>
`composer create-project --prefer-dist laravel/laravel blog`

### **7、laravel项目安装成功后，在宿主机的挂在目录中就可以看到刚刚创建的laravel项目了，此时更改nginx.conf文件里的root值和fastcgi_param值，将其指定到容器中得项目目录** <br>

### **8、重启docker容器** <br>
`docker-composer down` 关闭容器<br>
`docker-composer up -d` 启动容器<br>
### **9、打开浏览器 127.0.0.1就可以访问项目了，此时可以跟上端口，也可以修改nginx配置文件的server_name，换成一个域名** <br>

### **10、宿主机中访问容器的mysql**<br>
`mysql -uroot -h 127.0.0.1 -P 4306 -p`

### 注意：<br>
**docker-composer启动容器前，先获取php5.6、redis、nginx 、mysql的镜像**,
**laravel链接mysql时注意要在.env里将host更改为本机ip,如果mysql版本大于等于8.0,那么要更改配置文件，否则报错，原因为8.0以上版本加密方式改变。**
**scrapy框架为scrapinghub/scrapinghub-stack-scrapy:1.5-py3-latest，所以在启动在执行docker-composer up -d时要先`cd scrapy`,然后`docker build -t chensk/spider:v1`**
