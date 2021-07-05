# Vite + Vue.3.0 + Electron 集成搭建桌面app应用
## 环境
Node.js >=12.0.0
已安装vite，安装方式可以百度一下
安装yarn（可选）（下面步骤使用的yarn命令执行，npm或cnpm可自行转换命令）
## 1.创建vue模板的vite项目
    yarn create @vitejs/app my-vue-app --template vue
![e659e0e9c5e4b0b8d209ebf17dbff815.png](en-resource://database/1597:1)
                    
    cd my-vue-app
    yarn
    yarn dev

![33cbceebdd7ccac4c8102f048f0221cb.png](en-resource://database/1601:1)



#### 当前项目目录结构
![91dbcea31adc12cae20191876652268f.png](en-resource://database/1603:1)

## 2.安装electron相关模块
    yarn add electron -D

## 3.增加electron需要用到的文件
electron需要用到以下文件，需要手工创建
1. main.js
2.preload.js
#### 当前项目目录结构
![308c6d484594e2149789b3f3b06267e9.png](en-resource://database/1605:1)
PS: main.js和preload.js的内容可直接复制[electron-quick-start](https://github.com/electron/electron-quick-start)项目
preload.js无需修改
main.js需要修改BrowserWindow加载地址（dist目录是vue build后的目录）

    mainWindow.loadFile('index.html') 改成 mainWindow.loadFile('dist/index.html')

## 4.修改vite项目配置文件
修改vite.config.js 文件，配置app项目根路径
    
    base: path.resolve(__dirname, './dist')
    
![7d2b83cdcd67ab1f58d5b97f9d900c0b.png](en-resource://database/1609:1)

## 5.修改package.json
1. electron main 入口配置
2. electron 启动脚本配置
    
        "main": "main.js",
        "electron:start": "vite build & electron ."


![15dbb06afa414a1522ee9b2b9149a617.png](en-resource://database/1613:1)

大功告成
![270bfbcba93c3f0c40fae60a30147c4a.png](en-resource://database/1611:1)


## 后续补充
1.区分发布和开发环境（开发hotreload）
判断环境，正式打包：mainWindow.loadFile('index.html')
开发调试：mainWindow.loadURL(`http://localhost:3000/`)
