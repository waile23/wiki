#nodejs使用过程中的常见问题


##安装

- phantomjs安装不上的问题，切换下载地址  
`npm install phantomjs --phantomjs_cdnurl=http://cnpmjs.org/downloads`
- npm安装  
`npm install -ddd`

- 安装node-sass
`
# 设置本地代理
```
npm config set proxy http://127.0.0.1:1080
npm i node-sass

# 下载完成后删除 http 代理
npm config delete proxy
```
