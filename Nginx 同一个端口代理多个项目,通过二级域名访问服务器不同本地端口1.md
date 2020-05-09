## 一.前后台代码整合

**1.打包前台代码,存放到后台的public目录下,后台配置了static静态资源访问,**

**就能直接从后台代码作为入口,访问整合后的项目.**

**2.React,Vue都是单页面应用,前台路由是不会发起网络请求的,但是F5刷新会发起请求,**

**此时由于后台根本没有对应的中间件处理函数,刷新引起的请求得不到响应,404.**

解决方案,模拟脚手架功能;本地开发的时候F5刷新,脚手架给我们返回了一个index.html

项目整合后,我们可以在后台代码中模拟

```javascript
// 配置前台路由 把前台打包放到Public目录下,可解决单页面刷新问题
app.use(cxt=>{
    cxt.set('Content-Type','text/html;charset=UTF-8')
    const data = fs.readFileSync(__dirname+'/public/index.html')
    cxt.body = data
})
```

这样就能解决整合上线后刷新404问题

## 二.Nginx 同一个端口代理多个项目,通过二级域名访问服务器不同本地端口

##### 1.首先到服务器添加解析记录,设置好二级域名解析

例如我的域名 baidu.com

 二级域名1 nec.baidu.com

 二级域名2 ra.baidu.com

##### 2.到服务器上传项目

 在www目录下建两个文件夹 ,

 项目一是一个网易云API工具,我放在/root/www/NetEasyCloud目录下,项目使用3000端口

 项目二是一个react+antd+node项目,放在/root/www/react-antd目录下,项目使用3001端口

##### 3.检查上传的项目启动是否正常,依赖包安装完先启动看能不能正常运行

 最重要的一步!!!!!

##### 4.配置nginx.server /etc/nginx/nginx.server

 1.第一行 user root;

 2.配置server

 这里要注意server文件在编辑器没有语法报错提示,注意分号,空格,花括号完整!!!!

 server{ } 可以配置多个

 server_name可以配置多个域名 ,用空格隔开,就能实现多个地址指向一个项目

```nginx
server {
       listen 80;
       # 之前把第一个3000端口项目放在了NetEasyCloud目录下
       root /root/www/NetEasyCloud/;
       # server_name 监听你的域名,设置成你的对应二级域名就行
       server_name nec.baidu.com;
       # 这是注释, 访问根路由/    这里的路由也可以设置访问路径
       location / {
           # 默认打开index.html文件
           #index index.html;
           #转发到本地的3000端口,这里指的3000是在指服务器上本地运行项目的3000端口
           proxy_pass http://localhost:3000;
       }
   #    这里是配置nginx  gzip压缩加速 这段代码可以放到server外面
   gzip on;
   gzip_buffers 32 4k;
   gzip_comp_level 6;
   gzip_min_length 200;
   gzip_types text/css text/xml application/javascript;
   gzip_vary on;
```

##### 5.配置完成后保存nginx.config上传,链接ssh 启动服务(使用pm2管理)

```nginx
    pm2 stop all    //停止运行所有项目
    pm2 start app.js    //进入到项目文件夹找到入口文件,通过pm2启动
    //两个项目都启动之后开启nginx
    service nginx stop   //关闭nginx服务
    service nginx start  //开启nginx服务
```

 没有报错!!!nginx启动无异常

 去访问二级域名 nec.baidu.com 指向网易云api项目

 ra.baidu.com 指向react项目





```nginx
server {
    listen       80;
    server_name  localhost;
    location /a {
        proxy_pass http://127.0.0.1:8001/;
    }
    location /b {
        proxy_pass http://127.0.0.1:8002/;
    }
    location /c {
        proxy_pass http://127.0.0.1:8003/;
    }
}
```

[[Nginx 如何反向代理多个端口到同一端口不同目录上？](https://segmentfault.com/q/1010000017065655)](https://segmentfault.com/q/1010000017065655)