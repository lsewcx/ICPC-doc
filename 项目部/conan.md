# Conan

## 简介

conan是c++的_**包管理器**_，类似于pip，maven，只是了解的人比较少，下面来学习一下如何在_**linux中**_，用conan＋cmake来配置环境

也不是说windows不可以用，一般在windows不会用cmake

## 安装方式

```shell
pip install conan
```

## 生成配置文件

```shell
connan profile detect
```

## 编写需要的环境

示例

```
[requires]
nlohmann_json/3.11.2
[generators]
CMakeDeps
CMakeToolchain
[layout]
cmake_layout
```

大家不要担心，这个文件也不需要自己写在

[Conan 2.0: C and C++ Open Source Package Manager](https://conan.io/center)

这边都可以找到，它会给出编写示例

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310142049413.png)

## 安装环境

```
conan install conanfile.txt --build=missing
```

## 编写代码

在编写代码之前，首先是最让人头疼的cmake环境，但是它也给出了示例

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310142044289.png)

头文件也有示例

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310142044888.png)

这里给出cmake示例/home/lse/conan/build/Release/generators/是执行_**conan install**_后生成的环境的路径，改成你自己的生成的就行

```cmake
cmake_minimum_required(VERSION 3.16)
set (CMAKE_CXX_STANDARD 17)
project(HELLO)
SET(SRC main.cpp)
ADD_EXECUTABLE(HELLO ${SRC})
set(nlohmann_json_DIR /home/lse/conan/build/Release/generators/)
find_package(nlohmann_json REQUIRED)
target_link_libraries(HELLO nlohmann_json::nlohmann_json)
```

然后你的CMakeLists文件在哪里就设置什么样的路径

```shell
cmake ../  -DCMAKE_BUILD_TYPE=Release
```

然后

make一下再执行即可
