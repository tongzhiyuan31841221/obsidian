## Yarn 简介

[Yarn](https://classic.yarnpkg.com/zh-Hans) 是 Facebook, Google, Exponent 和 Tilde 开发的一款新的 JavaScript 包管理工具。就像我们可以从官方文档了解那样，它的目的是解决这些团队使用 npm 面临的少数问题。

Yarn 官网：[https://classic.yarnpkg.com/zh-Hans](https://classic.yarnpkg.com/zh-Hans/)

%% 有个小问题为什么安装依赖后有时候看不到node-modules%%
## 安装

官网脚本：

```javascript
curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --nightly
```

```javascript
npm install -g yarn
```


安装成功后，即可查看版本：

```javascript
yarn –version
```


## 常用命令

### 初始化新项目

```javascript
yarn init
```

npm 方式：

```javascript
npm init
```


yarn init 与 npm init 一样通过交互式会话创建一个 package.json 文件。

### 添加依赖包

通过 yarn add 添加依赖会更新 package.json 以及 yarn.lock 文件。

```javascript
yarn add [package]yarn add [package]@[version]yarn add [package]@[tag]
```


npm 方式：

```javascript
npm install [package]
```


将依赖项分别添加到不同依赖项，例如分别添加到 devDependencies、peerDependencies 和 optionalDependencies：

```javascript
yarn add [package] --devyarn add [package] --peeryarn add [package] --optional
```


### 升级依赖包

```javascript
yarn upgrade [package]yarn upgrade [package]@[version]yarn upgrade [package]@[tag]
```


npm 方式：

```javascript
npm update [package]
```


### 移除依赖包

```javascript
yarn remove [package]
```


npm 方式：

```javascript
npm uninstall [package]
```

### 安装项目的全部依赖

```javascript
yarn
```

```javascript
yarn installyarn install --force # 强制下载安装
```

npm 方式：

```javascript
npm installnpm install --force # 强制下载安装
```

### 运行脚本

```javascript
yarn run [script] [<args>]
```


yarn run 用来执行 package.json 中 scripts 属性下定义的脚本，例如：

```javascript
{  "name": "my-package",  "scripts": {    "dev": "node app.js",    "start": "node app.js"  }}
```

执行 scripts 属性下 dev 对应的脚本 node app.js

```javascript
yarn run dev
```


npm 方式：

```javascript
npm run dev
```


执行 scripts 属性下 start 对应的脚本 node app.js

```javascript
yarn start
```

npm 方式：

```javascript
npm start
```


### 显示某个包信息

```javascript
yarn info <package>
```

这个命令会拉取包的信息并返回为树格式，例如：

```javascript
yarn info react
```


```javascript
yarn info vx.x.x
{ name: 'react',
  version: '15.4.0-rc.2',
  description: 'React is a JavaScript library for building user interfaces.',
  time: { modified: '2016-10-06T22:09:27.397Z', ... } 
  ...
}
```

复制

这个命令默认的报告样式是单引号序列化的，如果要输出有效的 JSON 行格式，就使用标准的 --json 标志：

```javascript
yarn info react --json
```

复制

```javascript
{"type":"inspect","data":{"name":"react","time":{...}}}{"type":"finished","data":417}
```

复制

npm 方式：

```javascript
npm info <package>npm info <package> --json
```

复制

### 列出项目的所有依赖

```javascript
yarn list
```

复制

npm 方式：

```javascript
npm list
```

复制

Yarn 中的 list 命令列出当前工作文件夹所有的依赖，通过参考所有包管理器的元信息文件，包括项目的依赖，例如：

```javascript
yarn list vx.x.x
├─ package-1@1.3.3
├─ package-2@5.0.9
│  └─ package-3@^2.1.0
└─ package-3@2.7.0
```

复制

默认情况下，所有包的依赖会被显示，如果要限制依赖的深度，你可以给 list 命令添加一个标志 --depth 所需的深度：

```javascript
yarn list [--depth] [--pattern]
```

复制

例如：

```javascript
yarn list --depth=0
```

复制

### 管理 yarn 配置文件

**设置**：

```javascript
yarn config set <key> <value> 
```

复制

npm 方式：

```javascript
npm config set <key> <value> 
```

复制

**读取**：

```javascript
yarn config get <key>
```

复制

npm 方式：

```javascript
npm config get <key>
```

复制

**删除**：

```javascript
yarn config delete <key>
```

复制

npm 方式：

```javascript
npm config delete <key>
```

复制

**查看当前配置**：

```javascript
yarn config list
```

复制

npm 方式：

```javascript
npm config list
```

复制

**设置淘宝镜像**：

```javascript
yarn config set registry https://registry.npm.taobao.org
```

复制

npm 方式：

```javascript
npm config set registry https://registry.npm.taobao.org
```

复制

### 缓存

**列出已缓存的包**：

```javascript
yarn cache list
```

复制

**列出匹配指定模式已缓存的包**：

```javascript
yarn cache list --pattern <pattern>
```

复制

例如：

```javascript
yarn cache list --pattern gulp
yarn cache list --pattern "gulp|grunt"
yarn cache list --pattern "gulp-(match|newer)"
```

复制

**打印出当前 yarn 全局缓存的位置**：

```javascript
yarn cache dir
```

复制

**清除缓存**：

```javascript
yarn cache clean
```

复制

此外，您可以指定一个或多个想要清除的包：

```javascript
yarn cache clean [<module_name...>]
```

复制

### 改变缓存路径

设置 cache-folder 来配置缓存目录：

```javascript
yarn config set cache-folder <path>
```

复制

你也可以用 --cache-folder 标志指定缓存目录：

```javascript
yarn <command> --cache-folder <path>
```

复制

你还可以通过环境变量 YARN_CACHE_FOLDER 指定缓存目录︰

```javascript
YARN_CACHE_FOLDER=<path> yarn <command>
```
