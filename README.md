<h1 align="center">Ant Design Vue Pro</h1>
<div align="center">
based on  <a href="https://vuecomponent.github.io/ant-design-vue/docs/vue/introduce-cn/" target="_blank">Ant Design of Vue</a> & <a href="https://github.com/PanJiaChen/vue-element-admin" target="_blank">Vue Element Admin</a>
</div>


**Preview:**  [http://antv.tycoding.cn/](http://antv.tycoding.cn/)

## Introduce

本项目基于[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)开发， 请开发者先阅读[vue-element-admin文档](https://panjiachen.gitee.io/vue-element-admin-site/zh/)。

## Issues

由于本人是Java后端，对JS并不是很了解，因此此项目中还存在一些问题，希望前后端爱好者能积极参与到这个项目中，或者联系我商讨一些问题的解决方案。

**目前已知的问题：**

2. SideBar不能使用svg定义图标。原作者是依赖`el-icon`作为与svg的名称区分，在本项目中无奈我直接移除了
3. SideBar不能实现多层级路由（三级以上路由渲染不了），具体看`src/layout/Sidebar/SidebarMenu`组件。主要是因为原Element和AntV中`<menu>`组件的区别较大（这个问题如果有解决办法请及时联系我）。

## Features

- 提供最简洁的脚手架项目
- 移除原项目中：主题、国际化、TagsView、等组件
- 保持原有`vue-router`、`axios`、`vuex`的封装风格，对Java后端开发者更友好

本人能力有限，欢迎大家对项目二次封装，或提issue、pr。

项目文档正在写，请关注公众号**程序员涂陌**第一时间获取项目文档~

| 程序员涂陌                                                  |
| ----------------------------------------------------------- |
| ![qrcode_for_gh](http://cdn.tycoding.cn/20200610184737.jpg) |


## Docs

- [Ant Design Vue 文档](https://www.antdv.com/docs/vue/introduce-cn/)

- [Ant Design Vue Pro（官方推荐版本）](https://github.com/vueComponent/ant-design-vue-pro)

- [Vue Element Admin 源码](https://github.com/PanJiaChen/vue-element-admin)

- [Vue Element Admin 文档](https://panjiachen.gitee.io/vue-element-admin-site/zh/)



## Getting started

```bash
# clone the project
git clone https://github.com/TyCoding/ant-design-vue-pro.git

# enter the project directory
cd ant-design-vue-pro

# install dependency
npm install

# develop
npm run dev
```

This will automatically open http://localhost:9527

## Build

```bash
# build for test environment
npm run build:stage

# build for production environment
npm run build:prod
```

## Contact

- [Blog@TyCoding's blog](http://www.tycoding.cn)

- [GitHub@TyCoding](https://github.com/TyCoding)

- QQ Group: 671017003