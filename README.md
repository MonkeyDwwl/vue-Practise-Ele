# About vue-Practise-Ele
学习vue之后写的练手小项目，仿写ele单页应用。通过项目加深对知识点的理解，**特别声明：仅作个人练手项目而已，并无任何商业用途**。

## 项目技术栈
- vue2.0
- vue-router
- axios
- vuex
- less
- flex
- es6
- webpack
- vue-cli(脚手架)  

## 项目结构
```
.
├── README.md
├── build
├── config
├── index.html
├── node_modules   #包和模块安装目录
├── package.json   #项目配置文件
├── src
│   ├── App.vue
│   ├── api   #api文件
│   │   └── data.json
│   ├── assets
│   │   ├── css
│   │   └── fonts
│   ├── components  #各组件目录
│   │   ├── Buy
│   │   ├── Cart
│   │   ├── Food
│   │   ├── Goods
│   │   ├── Header
│   │   ├── Popup
│   │   ├── Ratings
│   │   └── Seller
│   ├── main.js 
│   ├── router   #路由文件
│   │   └── index.js
│   └── store
└── static   #静态资源目录
    ├── css
    │   └── reset.css
    └── js
        └── iscroll-probe.js
```

## 主要功能
- 显示商家的基本信息
- 显示商品的信息（包括分类列表和商品列表）
- 商品的详情页面
- 添加购物车的操作
- 购物车的相关操作
- 显示商家的评论信息
- 显示商家的详情信息

## 组件划分
个人喜好对组件的划分粒度比较细，可以按个人习惯和项目大小重新划分。  

- 头部组件
	- 弹出层组件
- 商品列表组件
	- 添加购物车组件
	- 购物车组件
- 评论组件
- 商家详情组件  

## api数据的获取
### 使用axios异步获取相关api数据信息

```
axios.get(url)
      .then(response => {
      	//取得数据
        this.goods = response.data;
      })
      .catch(error => console.log(error));
```

**需要注意的是：**response获得的数据，要结合具体接口情况来获取真正需要的数据，比如可能你需要的数据是在`response.data`中。  

### 关于axios跨域
在练习时使用axios获取api时，可能经常会遇到跨域的问题，针对跨域除了之前的几种传统方式以外发现个新的方法，在webpack中有个`webpack-dev-server`，这里内部集成了`http-proxy-middleware`；接下来只需要找到`webpack.config.js`文件（这个文件在不同的脚手架中位置可能不太一样），然后在devServer中使用proxy配置即可。真的超级简便，具体方法[参见手册](https://doc.webpack-china.org/configuration/dev-server/#devserver-proxy)。  
本项目仅作为练手，所以选择了模拟数据。  

## 部分效果图
![](http://upload-images.jianshu.io/upload_images/2730186-162805ed54936f89.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

![](http://upload-images.jianshu.io/upload_images/2730186-36b068b47d6077f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  

## 项目运行
克隆项目到本地  

```
npm install  //安装依赖

npm run dev  //开启服务

浏览器访问http://localhost:8080
```

本项目为个人练手项目，并无商业用途。如有错误或不明之处欢迎 issue~



