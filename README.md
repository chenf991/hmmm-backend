# 黑马面面后端服务接口

> 黑马面面前端项目地址：https://github.com/lipengzhou/hmmm-frontend

## 项目运行

```shell
# 下载仓库源码
git clone https://github.com/lipengzhou/hmmm-backend.git

#----------------------------------------------
# 使用数据库管理软件创建一个名为 hmmm 的数据库
# 在 hmmm 数据库中执行项目中 hmmm/db/mianmian.sql 文件
# 在 hmmm/config/config.default.js 文件中配置 mysql 数据库连接信息
# 执行完成继续下面的操作
#----------------------------------------------

# 进入项目目录
cd hmmm-backend

# 安装依赖
npm install

# 启动开发服务
npm run dev
```

## 调试

调试配置 `launch.json`

```bash
{
  // 使用 IntelliSense 了解相关属性。
  // 悬停以查看现有属性的描述。
  // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "调试",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceRoot}",
      "runtimeExecutable": "npm",
      "windows": {"runtimeExecutable": "npm.cmd"},
      "runtimeArgs": ["run", "debug"],
      "console": "integratedTerminal",
      "protocol": "auto",
      "restart": true,
      "timeout": 20000,
      "port": 9999
    }
  ]
}
```

## NPM命令

- 开发运行

```bash
npm i
npm run dev
open http://localhost:7001/
```

- 部署运行

```bash
npm start
npm stop
```

- 其它
  - Use `npm run lint` to check code style.
  - Use `npm test` to run unit test.
  - Use `npm run autod` to auto detect dependencies upgrade, see [autod](https://www.npmjs.com/package/autod) for more detail.

## 组件

### 控制器参数检查

- [egg-validate](https://github.com/eggjs/egg-validate)

- [parameter](https://github.com/node-modules/parameter)

### 查询字符串合并

- [escaping-query-values](https://github.com/felixge/node-mysql#escaping-query-values)

```js
var sql = "SELECT * FROM ?? WHERE ?? = ?";
var inserts = ['users', 'id', userId];
sql = this.app.mysql.format(sql, inserts);
```

### sha256

> npm install -S sha.js

```js
reqBody.password = shajs('sha256').update(reqBody.password).digest('hex')
```

### 数据库

- [mysql](https://github.com/mysqljs/mysql#readme)
- [egg-mysql](https://github.com/eggjs/egg-mysql)
- [ali-rds](https://github.com/ali-sdk/ali-rds)
- [ali-sdk](https://github.com/ali-sdk/ali-sdk)

## 中间件

### 令牌检查 `authorization`

- 配置文件 `config/config.default.js`

```js
  config.middleware = [
    'authorization'
  ]

  config.authorization = {
    whiteList: [
      '/base/frame/login'
    ],
    tokenHeaderKey: 'Authorization',
    authorizationPre: 'VEA-ADMIN'
  }
```

### 全局错误处理 `error_handler`

- 配置文件 `config/config.default.js`

```js
  config.middleware = [
    'errorHandler'
  ]

  config.errorHandler = {
  }
```
