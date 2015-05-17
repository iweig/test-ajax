# test-ajax

一个本地模拟接口

## install

```
npm install test-ajax
```

## demo

``` js
var test_ajax = require('test-ajax');

test_ajax({
    prot: 90, //端口
    cache_path: "./__cache/", //缓存文件的路径，基于base
    global: {},
    static_path: ['/static/'], //静态域，基于url
    admin: '/admin/', //后台域，基于url
    doc: '/doc/', //文档域，基于url
    open: true,//是否打开浏览器
    md: false,//是否支持md文档浏览
});
```

[在线demo](http://test-ajax.xuexb.com/admin/)

## options

### prot

`number`, 端口，默认`90`

### cache_path
`string`, 缓存目录，基于`base`（文件路径）

### global
`object`, 通用参数，在返回值里使用，如：
```
({
    global:{
        '500': 500,
        '404': '{"errcode": "404"}'
    }
})
```

返回值里使用（注：需要开启编译）：
```
<%=global['500']%>
<%=global['404']%>
```

### static_patch
`array`, 静态资源目录，比如模板，样式，以`url`开始

### admin
`string`, 后台路径，`url`开始

### doc
`string`, 文档路径，`url`开始

### open
`boolean`, 是否打开浏览器

## todo
* 美化页面，页面太丑，不忍直视。但目前功能ok后这个以后有时候再说吧~
* `jsonp`
* 文档下载
* 接口打包下载，上传
* 当本地静态遇到`node-combo`时的处理（ps:下一个要研究的东西就是`node-combo`&&单元测试）

## 后话
这套机制适合我吧，因为我们项目静态域单独，但接口是以根目录开始的，比如我使用的目录大概是：
```
本地静态：static.xx.me/
    tpl/ html模板
    js/ js文件，这里写接口都是以 url: '/api/login' 方式，因为到后端（线上）时就是这个目录
    css/ 样式
    api/ 本地接口测试
以上是本地环境，接口使用test-ajax调试

线上静态：static.xx.me/
    js/ js文件，这里写接口都是以 url: '/api/login' 方式，因为到后端（线上）时就是这个目录
    css/ 样式
线上正式： www.xx.com/
    api/ 接口目录
以上是正式环境，接口走正式的server端，无需切换
```
当然`test-ajax`只是一种思路，适合自己项目的才是最好的~