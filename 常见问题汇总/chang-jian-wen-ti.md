# 常见问题

## 前端

### 1.Vue

#### 1.1\[Vue warn]: Plugin has already been applied to target app.

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202309270951207.png)

检查main.js中的组件有没有_**复用**_，比如

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202309270958041.png)

上面的情况就会导致这个warn

**解决办法**

删除复用就行

_**撰写人：刘施恩 发现问题人：梁潘宇 日期2023/9/26**_

#### 1.2\[Vue Router warn]: No match found for location with path \*/pk/pk\_ index"

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202309270951194.png)

一般出现这种问题，是_**路径填写的不对的问题**_

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202309270952990.png)

**解决办法**

当你的路由是这么编写的时候，name是不用加到路由里面的所以真正打开的方法是\*\*\*/pk\*\*\*/就够了

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202309270952331.png)

_**撰写人：刘施恩 发现问题人：梁潘宇 日期2023/9/26**_

## 人工智能

### 1.1 推理部署

#### 1.1.1 paddlelite windows C++预编译库使用

尝试过_**vs2019**_和_**vs2022**_都不大行，通过github发现了应该使用_**vs2017**_，下载_**vs2017**_的预编译库

**解决办法**

链接好后，将模式改成_**x64**_的Release模式

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310012240000.png)

然后在资源管理器中修改运行库的状态改为_**多线程**_

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310012238423.png)

_**撰写人：刘施恩 发现问题人：刘施恩 日期：2023/10/1**_
