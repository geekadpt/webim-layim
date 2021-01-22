# 骆寻IM

Laravel + LayIM + GatewayWorker 开发的网页聊天系统。

## 新的改变

我们对之前的开源项目--[极云赋](https://gitee.com/geekadpt/ji_yun_fu)进行了重构，新版本的项目结构更为清晰，数据库设计更为合理，程序语法更为简洁，易于拓展维护。新版本不仅包含了旧版本的全部功能，我们还增加了如下几点新功能，与时俱进：
 1. **前后端完全分离** ，本项目包含一个完整的 API 服务器和两个全新设计的客户端( PC 客户端和手机客户端)；
 2. 全新的右键菜单；
 3. MySQL+MongoDB 双数据库配置，高性能的 MongoDB 负责存储大量的聊天记录和消息记录；
 4. 阿里云短信；
 5. 阿里云 OSS 存储大文件和图片；
 6. 应用 https 和 wss 传输协议；

## 项目截图

 - 体验网址：[im.luoxune.com](https://im.luoxune.com)

![添加好友](https://img-blog.csdnimg.cn/img_convert/2696f4765a5c2bcaf7b08a03378bc868.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021012218345298.png)


![在这里插入图片描述](https://img-blog.csdnimg.cn/2021012218345271.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/img_convert/e7309bef10ad2550072a0ec08d69d769.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021012218345267.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210122183451883.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210122183451853.png)
![在这里插入图片描述](https://luoxune.oss-cn-beijing.aliyuncs.com/app/mobile_exam.png)

## 项目结构
- app
  - Concole ------------------------------------------------------包含应用所有自定义的 Artisan 命令
  - Http
    - Controllers/Api ----------------------------------------------------------处理所有通过接口进入应用的请求
    - Middleware --------------------------------------------------------------中间件
    - Requests -----------------------------------------------------------------请求验证类
    - Resources ---------------------------------------------------------------接口资源类
  - Providers ----------------------------------------------------------服务提供者类
  - Services -----------------------------------------------------------服务类
- Applications/LuoXun ---------------------------------------GatewayWorker配置文件目录
- config  ----------------------------------------------------------------Laravel 配置文件目录
- database
  - factories ---------------------------------------------------------- 数据库工厂目录
  - migrations -------------------------------------------------------- 数据库迁移文件目录
  - seeds -------------------------------------------------------------- 数据填充目录
- public
  - plugins ------------------------------------------------------- 前端插件目录
  - layui ---------------------------------------------------------- 把包含 LayIM 的 Layui 放在这里
- resources
  - css ------------------------------------------------------------ 前端 CSS 目录
  - js -------------------------------------------------------------- 前端 JS 目录
  - lang ----------------------------------------------------------  多语言设置目录
  - views
      - mobile -------------------------------------------------------------- 手机客户端
      - pc ---------------------------------------------------------------------PC 客户端
      - index.blade.php -------------------------------------------------- 首页视图
      - login.blade.php --------------------------------------------------- 登录视图
      - reg.blade.php ----------------------------------------------------- 注册视图
- routes
      - api ---------------------------------------------------------------- 接口路由
      - web ---------------------------------------------------------------视图路由
- .env ------------------------------------------------------ Laravel 全局配置文件


## 安装使用
我们假设你的服务器已经配置好了 Laravel 项目环境。

安装拓展包
```bash
composer update
```
打包 css/js
```
npm install
npm run production
```
编辑配置文件，把XXXX都填上
```
cp .env_example .env
vim .env
```
把包含 LayIM 的 layui 放在 /public 目录下

修改 /resources/views/pc/app.blade.php 和 /resources/views/mobile/app.blade.php 中的域名
```html
var domain = ‘{Yourdomain}/wss’;
```
配置 nginx，解决 wss 协议问题

```powershell
#laravel 框架 nginx 配置文件中的对根目录的访问修改为以下
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


生成数据加密秘钥

```bash
php artisan key:generate
```

生成 jwt 令牌秘钥

```bash
php artisan jwt:secret
```

数据库迁移

```bash
php artisan migrate
```

填充用户和群组账号数据表

```bash
php artisan db:seed
```
上线项目
```bash
php artisan up
```


## FAQ

 1. 为什么项目中不包含 LayIM 文件？
LayIM 受国家计算机软件著作权保护，未经官网正规渠道授权不能公开产品源文件。当你获得 LayIM 后把包含 LayIM 的 layui 放在 /public 目录下即可。
 2. 为什么没有管理后台？
管理后台直接操作数据表，与项目中的请求处理逻辑无关。使用 [laravel-admin](https://laravel-admin.org/) 可以在十分钟内构建一个功能齐全的管理后台。
 3. 有没有配套文档？
旧版本有[配套文档](https://www.kancloud.cn/tiaohuaren/laravel)，新版本配套文档还在编写中。

## 捐赠
![在这里插入图片描述](https://luoxune.oss-cn-beijing.aliyuncs.com/app/donate_inte.png)
