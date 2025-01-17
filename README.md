青训营前端结业项目答辩汇报文档

一、项目介绍
======

> 项目名称：字节青训营Low-Code项目
> 
> 团队：six god
> 
> 项目服务地址 http://18.222.123.50:82
> 
> Github 地址: https://github.com/giraffecat/LowCode

### 1.1 项目背景及意义

在前端开发中，组件化思想是一个非常重要的思想。前端组件化开发可以很大程度地降低系统中各个功能的耦合性，提高代码复用率，例如像Bootstrap、elementUI等这些UI组件库，这些组件库对前端工程化、以及降低代码的维护难度，具有很大的帮助。

低代码平台解决的最大问题就是复用，除此之外，对于开发人员来说，这个平台能够显著提升开发效率，甚至还能让不具备编码技能的设计人员实现页面的构建和代码的产出。为了满足这些业务的需求，我们团队搭建了一款针对于H5页面开发的Low-Code平台，支持组件拖拽、配置、页面预览等多种功能，可快速实现页面的可视化搭建。

### 1.2 低代码平台概要

低代码平台主要是由「物料组件区」、「画布区」、「属性编辑区」这三个部分组成的。其中物料组件区负责展示可拖拽的组件，画布组件区负责渲染组件，对其进行可视化展示，属性编辑器负责修改选中组件的属性。针对这三者的职责，我们大概设计出了所需要实现的基本功能：

对于物料组件区，保证其是可拖拽的，并且能与画布区进行交互；对于画布区，可看成这是一个巨大的容器，具有对组件数据的渲染功能；对于属性编辑器，需要获取组件的实时数据，实现与对应组件的联动逻辑。

为了实现这些功能，本团队基于Vue.js框架以及element ui 组件库，采用JSON schema和vuex的全局数据管理和联动方案，以及vuedraggable插件实现组件的拖拽，为低代码平台提供一种可行的解决思路。

二、项目分工
======

本团队共有5人，大部分是准研三的学生。在队长的合理安排和明确分工下，各个成员各司其职，最终共同完成了本项目的主要功能。

整体页面展示图：

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=OGFiMTk2NzEwYzk3MDQ0MzA1MmE4Y2VlYjBmY2VmZjFfNVB0TWNTUmMySk5JSzh3dG16M1poUnVBY29KRW9ncXdfVG9rZW46Ym94Y25XREptcTZiS3hDOTBvMEU2OXhyeEJkXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

三、项目实现
======

项目服务地址 http://18.222.123.50:82。

### 3.1 技术选型

项目采用 Vue2 + VueRouter + VueX + ElementUI实现，同时采用vuedraggable插件实现组件的拖拽。

### 3.2 架构设计

整个项目架构可以分为四个部分，分别是顶部菜单栏、物料组件区、画布区、属性配置区。

1. #### 顶部菜单栏

主要实现的是页面管理功能，包括添加、清除、删除操作，以及调整画布大小、渲染、Github第三方登录功能。

2. #### 物料组件区

展示了一些基本的常用的可拖拽式的物料组件。其中包括两个容器组件，以及其他组件。

3. #### 画布区

渲染拖拽过来的物料组件，通过根据属性编辑区数据来实时更新渲染内容。同时可以实现组件的选中，对选中的组件进行删除和复制操作。

4. #### 属性编辑区

可以可视化选中组件的属性，调节属性的参数，更好后的参数可以传给画布进行实时的渲染。

### 3.3 项目代码介绍

主要从要解决的5个核心问题来介绍本项目的代码。

1. #### 可拖拽组件是如何初始化的？

我们定义一套JSON格式数据规范来描述组件的属性值，主要包括name（名称）, icon（图标）, fields（样式）属性，其中fields属性有包含label（名称）, type（类型）, value（值）属性。

以button组件为例：

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=MjI4ZGIyN2MxZjljZGE1MTFjYmJiOGZjYTc4ZDJjYWNfdzNLYklFV290YmZ3SGZIMERqaDRPOFlrZ1IyNEpVcW5fVG9rZW46Ym94Y25NZGM4ZnViWUJsTGxQSEw1TXVXRm5jXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

JSON数据在全局自动数据注册函数（registerSchema.js）的作用下，将物料数据全部信息存储在全局变量$initializing、 $fields上。所以左侧的物料组件是通过遍历$initializing数据展示的。

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=MzljNzA5NjcyZWM2NzRjYjFmNzQ4NWExMWZjMGJhOTZfQUFiRGRyN2pBQ1ZVd0Rzb3I0aXlteEtGcEpqZGNSdkdfVG9rZW46Ym94Y25OWGxmZ1RHT01xeE41a0dZWXdYd1ZiXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=OGQ2MTgxZTlkZWVjZmYzM2RhMTRjNmRkZTNmMWZlZWZfeWlFTFJOWTRBcXZLc3V3TkxhMG0wM3paNU94TkpsWDdfVG9rZW46Ym94Y25NTWVqRkFZNDdaTThobjVuU1JyOTRmXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

$initializing、 $fields在后续的可视化拖拽页面中也扮演着渲染与物料配置之间的纽带。

2. #### 画布是如何渲染的？

前提要把物件拖拽到画布中。本项目选择了vuedraggable插件来实现组件的拖拽。

vuedraggable一款基于Sortable.js实现的vue拖拽插件。支持移动设备。可以在不同组件间拖拽，使用起来也很简单，总之是一款非常优秀的vue拖拽组件。每个组件其实都是一个vuedraagable容器。

> Options 表示draggable 列表配置项，group用于分组（相同的组之间可以相互拖拽），sort定义是否可以拖拽(false 不可以拖拽到当前组)，animation定义动画时间
> 
> clone事件，handleClone用来将组件的Json数据深度拷贝到渲染数据中

当从物料区选择组件拖拽到画布上时，首先会将组件的元数据进行深度拷贝，插入到当前的渲染物料数据中。画布组件一直处于watch的监视状态，一旦有组件掉落，就会触发widgets属性（我们用来描述整个画布中组件的所有数据）的更新。有了最新的widgets数据，就可以对其中和UI组件相关的属性进行渲染。

    watch: {    widgets: {      handler(val) {        // console.log("widgets", val)        this.list = val;      },      immediate: true,      deep: true,    },    list: {      handler(val) {        this.$emit("update:widgets", val);      },      immediate: true,      deep: true,    },  },

同时，画布还有选中组件的功能，主要是功能给每个组件设置click事件触发，当被点击时，会加上选中的样式，显示出工具栏。

3. #### 属性编辑器是如何实现数据联动的？

为画布上的组件添加点击事件，使其能够在点击时设置右侧属性编辑面板的内容，同时改变属性编辑区的数据，会触发选中组组件的样式更新。所以这里很重要的是属性编辑区和画布区组件的通信。

层级很复杂，我们使用适用于多层组件通信的方案provide/inject，属性编辑区组件直接传递给选中组件一个this，这样选中组件可以实时获取到属性编辑区组件最新的值，而且属性编辑区组件也能拿到选中组件的数据。

如下面的代码所示：

    // 属性编辑区组件{provide() {    return {      chontrol: this, // inject响应式监听    };  },  data() {    return {      widgets: [],      curComponent: undefined,    };  } }  // 在选中组件中，选中物料setcurComponent(cmp) {  this.show = true; // 选中样式可见  this.chontrol.curComponent = cmp; // 设置当前组件的数据curComponent  }

可以看到我们的属性编辑区的面板，对于同一样类型的属性，我们采用相同的模板来进行可视化操作。这是本项目的一个特色之一，就是我们抽象了出数组、图片上传、对象、跳转等十多个的属性编辑组件，组件的类型记录在物料组件的JSON数据type属性中。这样可以便于更好地规范和管理组件数据，同时提高开发效率，后期新增物料组件时，可以通过拖拽属性编辑组件，直接导出物料组件的JSON数据，避免了繁琐的手动编辑数据工作。

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=MzFkZjA1ZTY3NmU4NTM3ZmVlNzhiN2U0YjkyMWZmNzdfNnVWTTVQb2FPN1hQOUN1ZkJUaFo2cnpEeHlLZWpKSHlfVG9rZW46Ym94Y25zRng3N3EyZkF4N09aVE4wU0dNMDJkXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

4. #### 页面管理如何实现？

利用状态管理仓库vuex来管理一些经常用到、且容易变动的数据，比如pages数据, widgets数据。画布中每一次的变动（widgets对象改变），都会触发仓库中widgets数据更新，而pages数据是一个对象数组，记录了每一个页面的widgets， id, name的值。

![](https://izrq7ytia1.feishu.cn/space/api/box/stream/download/asynccode/?code=MTNlMWY3ODBjNDllOWEyM2VjZjVkZGIxYWIzNTg5MjVfeTRlZkFRUm1HbW5zeTlmZzlGQ2l3aFYzaDNlVk1jMXhfVG9rZW46Ym94Y25GejdMa3VJWm9oejRXRUd1M3FPaW1oXzE2NjI3ODk1MzU6MTY2Mjc5MzEzNV9WNA)

    watch: {    widgets: {      handler(val) {        // 更新此时的widgets        this.$store.commit("setWidgets", val);        // 更新pages中的widgets        this.$store.commit("updateWidgets", val);      },      immediate: true,      deep: true,    },  },    mounted() {    this.newPage();    eventBus.$on('updateCurPage',(cur)=>{      this.curPage = cur
              })  },

必要的时候，用全局事件总线辅助。

5. #### 预览

基本和画布数据的可视化一样，但是值得注意的是，这里的组件的点击事件不再是选中。

isPreview判断当前的操作是预览还是编辑状态。

四、测试结果
======

功能测试：

1. 组件拖动、嵌套正常

2. 组件基本属性编辑正常

3. 当前画布清空、预览正常

4. 画布新建、删除、切换正常

5. 点击按钮后在自定义页面间跳转正常

6. 图片上传正常
