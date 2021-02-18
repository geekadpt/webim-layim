# Locyin-WebIM

A web chat system developed by Laravel + LayIM + GatewayWorker.

## New Changes

We have reconstructed the previous open source project--[ji_yun_fu](https://gitee.com/geekadpt/ji_yun_fu), the new version of the project structure is clearer, the database design is more reasonable, the program syntax is more concise, easy to expand and maintain. The new version not only includes all the functions of the old version, but also adds the following new functions to keep pace with the times:

The project includes a complete API server and two newly designed clients (PC client and mobile client);

2. New context menu;

3. MySQL + mongodb dual database configuration, high-performance mongodb is responsible for storing a large number of chat records and message records;

4. Alibaba cloud SMS;

5. Alicloud OSS stores large files and pictures;

6. Apply the transmission protocol of HTTPS and WSS;

## Project Screenshot

 - demo：[im.luoxune.com](https://im.luoxune.com)

![add_friends](https://img-blog.csdnimg.cn/img_convert/2696f4765a5c2bcaf7b08a03378bc868.png#pic_center)
![user_profile](https://img-blog.csdnimg.cn/2021012218345298.png)


![message_box](https://img-blog.csdnimg.cn/2021012218345271.png)
![create_group](https://img-blog.csdnimg.cn/img_convert/e7309bef10ad2550072a0ec08d69d769.png#pic_center)
![chat_logs](https://img-blog.csdnimg.cn/2021012218345267.png)
![group_context_menu](https://img-blog.csdnimg.cn/20210122183451883.png)
![friend_context_menu](https://img-blog.csdnimg.cn/20210122183451853.png)
![mobile_client](https://luoxune.oss-cn-beijing.aliyuncs.com/app/mobile_exam.png)

## Project Structure
- app
  - Concole ------------------------------------------------------Contains all custom artisan commands
  - Http
    - Controllers/Api ----------------------------------------------------------Handle all requests to enter the application through the interface
    - Middleware --------------------------------------------------------------middleware
    - Requests -----------------------------------------------------------------Request validation class
    - Resources ---------------------------------------------------------------Interface resources class
  - Providers ----------------------------------------------------------Providers
  - Services -----------------------------------------------------------Services
- Applications/LuoXun ---------------------------------------GatewayWorker configuration file directory
- config  ----------------------------------------------------------------Laravel configuration file directory
- database
  - factories ---------------------------------------------------------- Database factory directory
  - migrations -------------------------------------------------------- Database migration file directory
  - seeds -------------------------------------------------------------- Data seed directory
- public
  - plugins ------------------------------------------------------- Plugins
  - layui ---------------------------------------------------------- Put the layui which contains layim here
- resources
  - css ------------------------------------------------------------ Front-end CSS directory
  - js -------------------------------------------------------------- Front-end JS directory
  - lang ----------------------------------------------------------  Multilingual Settings directory
  - views
      - mobile -------------------------------------------------------------- Mobile client
      - pc ---------------------------------------------------------------------PC client
      - index.blade.php -------------------------------------------------- Index page view
      - login.blade.php --------------------------------------------------- Login page view
      - reg.blade.php ----------------------------------------------------- Register page view
- routes
      - api ---------------------------------------------------------------- api routers
      - web ---------------------------------------------------------------web routers
- .env ------------------------------------------------------ Laravel global configuration file


## Installation And Use
Suppose your server is configured with the laravel project environment.


```bash
composer update
```

```
npm install
npm run production
```

```
cp .env_example .env
vim .env
```
Place the layui containing layim in the / public directory

modify the domain name in  /resources/views/pc/app.blade.php and /resources/views/mobile/app.blade.php 
```html
var domain = ‘{Yourdomain}/wss’;
```
configure Nginx，resolve wss protocol problems

```powershell
location / {
	try_files $uri $uri/ /index.php?$query_string;
}
location /wss {
	proxy_pass localhost:5210;
	proxy_http_version 1.1;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection “upgrade”;
	proxy_set_header Host $host;
}
```


```bash
php artisan key:generate
```


```bash
php artisan jwt:secret
```


```bash
php artisan migrate
```


```bash
php artisan db:seed
```

```bash
php artisan up
```


## FAQ

 1. Why don't we include layim files in this project?
    Layim is protected by the copyright of national computer software, and the product source files cannot be disclosed without the authorization of the official website. When you get layim, put the layui containing layim in the / public directory.
 2. Why is there no backstage management?
The data table is directly operated by the management background, which has nothing to do with the request processing logic in the project.Use You can use [laravel-admin](https://laravel-admin.org/) to build a fully functional management background in ten minutes.
 3. Have supporting documents or not?
    The old version has [supporting documents](https://www.kancloud.cn/tiaohuaren/laravel), while the new version is still being written.

## Donation
![在这里插入图片描述](https://luoxune.oss-cn-beijing.aliyuncs.com/app/donate_inte.png)
