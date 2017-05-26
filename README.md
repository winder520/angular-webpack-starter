# 文件打开

## 获取项目文件


`git clone https://code.aliyun.com/winderwang/kop-platform-ui.git`


## 安装相关依赖及运行项目

> 1、安装node 和安装npm
[node下载地址](https://nodejs.org/en/)

> 2、用vscode或webstorm打开项目

> 3、用开发软件自带的终端（命令行） 输入
`npm install` 或 `cnpm install`

> 4、用开发软件自带的终端（命令行） 输入
`npm install -g webpack`

> 5、用开发软件自带的终端（命令行） 输入
`npm start`

> 6、在浏览器中输入:http://localhost:4200/

## 测试环境相关配置

> 1、安装karma `npm install -g karma`

> 2、在仿DOS窗口运行：`npm run test`

## 开发的时候注意项

> 1、在组件里面引用CSS（LESS）的时候用 `require` 导入：

  ```js

  require('./app.component.less')

  @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.less']
  })
  export class AppComponent implements OnInit {}
  ```

> 2、在CSS或HTML引用外部图片要用相对路径

  ```CSS
  .row {
    margin: 0px;
    padding: 0px;
    height: 100%;
    background: url('../assets/images/faces/ee_1.png')
  }
  ```

  ```HTML
  <img src="../assets/images/css-sprites/notify.png" class="chat-but">
  ```

> 3、图片格式请使用格式 jpg png gif

> 4、在js（ts）里面不要直接使用图片地址的方式，打包不支持

> 5、编写测试代码的时候文件名后缀以：组件（｜指令｜服务）.spec.ts 结尾

## 和后端集成

### 后端地址

`git clone https://code.aliyun.com/winderwang/kop-platform-api.git`


### 需要代理设置配置

#### nginx配置

修改配置文件路径：

盘符:\文件夹（一个或多个）\nginx文件夹\conf\nginx.conf

```
server {
    listen       80;
    server_name  pf.dev.kopbit.com;

    charset utf-8;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   Cookie $http_cookie;
        add_header Access-Control-Allow-Origin *.6starhome.com;
        add_header Access-Control-Allow-Headers X-Requested-With;
        add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
        add_header Access-Control-Allow-Credentials true;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header Host            $http_host;
        proxy_redirect off;        proxy_set_header X-NginX-Proxy true;
        proxy_read_timeout 5m;
        proxy_connect_timeout 5m;
        proxy_pass http://127.0.0.1:4200;
    }

    location /api {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   Cookie $http_cookie;
        add_header Access-Control-Allow-Origin *.6starhome.com;
        add_header Access-Control-Allow-Headers X-Requested-With;
        add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
        add_header Access-Control-Allow-Credentials true;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header Host            $http_host;
        proxy_redirect off;        proxy_set_header X-NginX-Proxy true;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_read_timeout 5m;
        proxy_connect_timeout 5m;
        proxy_pass http://127.0.0.1:3000;
    }
}
```

#### host 配置

修改文件路径：
C:\Windows\System32\drivers\etc\hosts

`127.0.0.1 pf.dev.kopbit.com`

注：前端端口为：4200  api 端口为：3000

#### 启动(不分先后顺序)：

1. 启动前端程序 (npm start)

2. 启动后端程序 (npm start)

3. 启动nginx

## api接口

  [可普平台api接口--知识库](http://ide.kopbit.com/app/edit-space/index.html?projectId=57ac3ca0-d7a5-11e6-8ff1-dd1c8e9d7d44)
