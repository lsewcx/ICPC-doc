# go语言

## go语言基础

## 环境搭建

Go 和 C语言、C++、Python、Java 等一样都是编程语言。学习任何一门编程语言本质上都分3步走：

* 第一步：安装 `解释器 或 编译器`。
* 第二步：学相关编程语言语法，然后写代码。
* 第三步：用已安装`解释器 或 编译器` 去运行自己写的代码，这样代码就会去完成我们编写的功能了。

Go是编译型语言，所以我们一般称Go安装是`编译器`。

Go是开源且跨平台的一门编程语言，所以他支持window、linux、mac操作系统，同时也意味着我们可以在各种系统中安装Go的编译器。

### 1. Mac系统

#### 1.1 下载Go编译器

https://golang.google.cn/

#### 1.2 点击安装

默认的安装目录：`/usr/local/go/`

编译器启动文件：`/usr/local/go/bin/go`

#### 1.3 配置环境PATH

```
export PATH=/usr/local/go/bin:$PATH
```

#### 1.4 其他配置

**1.4.1 创建一个任意目录**

此目录以后放你写的所有go代码。

```
/Users/wupeiqi/GolangProjects/
- bin,通过go install编译时候，生成的可执行文件。
- pkg,通过go install编译时候，生成的包文件。
- src,放我们以后编写的所有go代码和依赖。
	- crm
		- app.go
	- luffcity
		- xx.go
```

**1.4.2 配置环境变量**

```
// Go安装目录
export GOROOT=/usr/local/go
// 代码和编译之后的文件相关代码
export GOPATH=/Users/wupeiqi/GolangProjects
// 存放编译之后的文件
export GOBIN=/Users/wupeiqi/GolangProjects/bin
```

#### 1.5 环境变量“持久化”

vim \~/.bash\_profile

```
export PATH=/usr/local/go/bin:$PATH
export GOROOT=/usr/local/go
export GOPATH=/Users/wupeiqi/GolangProjects
export GOBIN=/Users/wupeiqi/GolangProjects/bin
```

#### 1.6 编写go代码

```
$GOPATH
├── bin
├── pkg
└── src
    └── crm
        └── app.go
```

```go
package main

import "fmt"

func main() {
    fmt.Println("叫爸爸")
}
```

#### 1.7 运行

本质上就是让Go编译器去运行咱们编写的代码。

方式1：

```go
// 先进入项目目录
go run app.go
```

方式2（推荐）：

```go
// 先进入项目目录

// 编译代码
go build
// 运行
./crm
```

方式3：

```go
// 先进入项目目录
go install 

// 去bin运行
./crm
```

```
$GOPATH
├── bin
│   └── crm
├── pkg
└── src
    └── crm
        └── app.go
```

### 2. Linux系统

#### 2.1 下载Go编译器

https://golang.google.cn/

#### 2.2 安装

```
安装目录
/opt/go
```

启动Go编译器文件：`/opt/go/bin/go`

#### 2.3 配置环境变量PATH

```
export PATH=/opt/go/bin:$PATH
```

#### 2.4 其他配置

**2.4.1 创建一个任意目录**

存放咱们编写的所有项目代码，编译文件之后存放编译后的文件。

```
/home/wupeiqi/GolangProjects/
- bin,在执行go install 命令，生成的可执行文件的目录。
- pkg,在执行go install 命令，存放生成的包文件。
- src,以后编写的所有Go代码都会放在这个目录。
	- crm
		- app.go
	- luffy
		- lk.go
```

**2.4.2 环境变量的配置**

```
export GOROOT=/opt/go
export GOPATH=/home/wupeiqi/GolangProjects
export GOBIN=/home/wupeiqi/GolangProjects/bin
```

#### 2.5 环境变量的“持久化”

vim \~/.bash\_profile

```go
export PATH=/opt/go/bin:$PATH
export GOROOT=/opt/go
export GOPATH=/home/wupeiqi/GolangProjects
export GOBIN=/home/wupeiqi/GolangProjects/bin
```

#### 2.6 编写go代码

```
/home/wupeiqi/GolangProjects（简写$GOPATH）
├── bin
├── pkg
└── src
    └── crm
        └── app.go
```

```go
package main
import "fmt"
func main() {
    // 调用Println函数在屏幕输出：叫爸爸
    fmt.Println("叫爸爸")
}
```

#### 2.7 运行代码

本质上将写好的代码交给Go编译器去执行。

方式1：

```
// 进入项目目录
go run app.go
```

方式2（推荐）：

```
// 进入项目目录

// 编译代码并生成一个可执行文件
go build  

// 运行
./crm
```

方式3：

```
// 进入项目目录

// 编译代码，把编译之后的结果会放在 bin/pkg目录
go install 

// 运行
./crm
```

```
├── bin
│   └── crm
├── pkg
└── src
    └── crm
        └── app.go
```

Go程序员的项目：

* 产出一个可执行文件。
* 产出一个包文件。

### 3. Windows系统

#### 3.1 下载Go编译器

https://golang.google.cn/

#### 3.2 点击安装

建议安装：`C:\Go`

#### 3.3 环境变量PATH

以便于以后运行GO编译器时，无需再写路径。

#### 3.4 其他配置

**3.4.1 创建一个任意目录**

以后咱们的go项目都要按照要求放在这个目录。

```
Y:\GolangProjects
 - bin,go install在编译项目时，生成的可执行文件会放到此目录。
 - pkg,go install在编译项目时，生成的包文件会放到此目录。
 - src,以后所有的项目都要放在这个目录。
 	- crm
 		- app.go
	- luffy
		- xx.go
```

**3.4.2 环境变量配置**

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151128416.png)

#### 3.5 编写代码

```
Y:\GolangProjects
 - bin
 - pkg
 - src,以后所有的项目都要放在这个目录。
 	- crm
 		- app.go
```

```go
package main

import "fmt"

func main() {
    fmt.Println("叫爸爸")
}
```

#### 3.6 运行

本质上就是把Go代码交给Go编译器去执行。

方式1：

```
// 进入项目目录
go run app.go
```

方式2（推荐）：

```
// 进入项目目录
go build

crm.exe
```

方式3：

```
// 进入项目目录
go install

执行 crm.exe
```

```
Y:\GolangProjects
 - bin
 	- crm.exe
 - pkg
 	- windows_amd64
 		- utils.a
 - src,以后所有的项目都要放在这个目录。
 	- crm
 		- app.go
 	- utils
 		- page.go
```

平时开发：

* 开发可执行文件，用来让用户使用。
* 开发一个包文件，其他项目来进行调用。

### 总结

首先要去下载Go编译器，然后进行安装，在安装目录下就是GO编译器相关的所有内容。

```
mac:     /etc/local/go/
linux:   /opt/go/
windows: C:\go\
```

在安装目录下有 bin目录中有一个go可执行文件，基于他来启动编译器。

* 直接通过路径找到可执行文件去运行（麻烦）
* 将 `/etc/local/go/bin` 目录添加PATH环境变量中。

那么在终端就可以执行执行`go version`，调用咱们安装的编译器。

如果想要正确的使用go编译器，还需做一些相关的配置（其他语言）。

*   创建目录，用于存放项目代码、编译后的可执行文件、编译后的包文件。

    ```
    xxxx
    - bin
    - pkg
    - src
    	- crm
    		app.go
    ```
*   环境变量

    ```
    GOROOT,GO编译器安装目录。
    GOPATH，用于存放项目代码、编译后的可执行文件、编译后的包文件（go 1.11版本后，go mod）。
    GOBIN，编译后的可执行文件存放的目录。
    ```

编写代码，然后进行。

写了两个项目：

* crm，编译后生成一个可执行文件。
* utils，编译后生成一个包文件。

运行项目

* go run，运行项目代码，内部会先编译并将编译后的文件放在系统的临时目录，然后再自动执行。
* go build，运行项目代码，手动编译并生成一个可执行文件，然后再自动执行。
* go install ，生成可执行文件 + 包文件，并且会将编译后的文件放在bin/pkg目录。

### 4.开发工具

* Goland，IDE（继承开发环境）【收费】
* vscode，编辑器 + 第三发组件 【免费】

#### 4.1 下载Goland

https://www.jetbrains.com/go/

#### 4.2 配置

* 字体
* 参数提示

#### 4.3 项目开发

* 新项目
* 打开老项目

注意：项目放在 `$GOPATH/src`目录。

## 快速上手

* 初识包管理，知道项目中文件和文件、文件和文件夹之间关系。
* 输出，写代码，在go编译器运行时会在屏幕显示内容。
* 初识数据类型
  * 整型，数字。例如：1、2、3、4
  * 字符串，表示文本信息。例如：“如家” "锦江之星"
  * 布尔类型，真假。例如： 1>2 、 "如家" == “家”
* 变量 & 常量，当做是昵称。
* 输入，让咱们用户输入内容。
* 条件语句，开发一个猜数次程序，用户输入数字与咱们定义的数字进行比较。

### 1.初识包管理

关于包管理的总结：

* 一个文件夹可以称为一个包。
* 在文件夹（包）中可以创建多个文件。
* 在同一个包下的每个为文件中必须指定 `包名称且相同`

重点：关于包的分类

* main包，如果是main包，则必须写一个main函数，此函数就是项目的入口（main主函数）。 编译生成的就是一个可执行文件。
* 非main包，用来将代码进行分类，分别放在不同的包和文件中。

注意：

* 调用其他包的功能，需要先 import 导入，然后再使用；调用自己包中的功能时，直接调用即可（无需导入）
* 文件中的函数首字母是小写，表示此函数只能被当前包内部文件调用。首字母是大写，则意味着任何包都可以调用。

### 2.输出

在终端将想要展示的数据显示出来，例如：欢迎登录、请输入用户名等。。。

* 内置函数
  * print
  * println
* fmt包（推荐）
  * fmt.Print
  * fmt.Println

扩展：进程里有 stdin/stdout/stderr 。

```go
package main

import "fmt"

func main() {
	// 基于内置函数（不推荐）
	//print("好吃不过饺子 \n")
	//print("好玩不过嫂子 \n")
	//println("好吃不过饺子")
	//println("好玩不过嫂子")

	// fmt包（推荐）
	//fmt.Print("好吃不过饺子 \n")
	//fmt.Print("好玩不过嫂子 \n")
	//fmt.Println("好玩不过嫂子")
	//fmt.Println("好玩不过嫂子")
	//fmt.Println("我叫", "Alex", "我媳妇", "是个", "....")
	//fmt.Println("我叫Alex我媳妇是个....")

	// fmt包 扩展：格式化输出
	// %s，占位符 "文本"
	// %d，占位符 整数
	// %f，占位符 小数（浮点数）
	// %.2f，占位符 小数（保留小数点后2位，四舍五入）
	// 百分比
	fmt.Printf("老汉开着%s,去接%s的媳妇，多少钱一次？%d块。嫂子给打折吧，%.2f怎么样？小哥哥包你100%%满意", "车", "老男孩", 100, 3.889)
}
```

### 3.注释

* 单行注释， //
* 多行注释， /\* \*/

快捷：contrl + ?

### 4.初识数据类型

* 整型，整数
* 字符串，文本
* 布尔型，真假

```go
package main

import "fmt"

func main() {
	// 整型
	fmt.Println(666)
	fmt.Println(6 + 9)
	fmt.Println(6 - 9)
	fmt.Println(6 * 9)
	fmt.Println(16 / 9) // 商
	fmt.Println(16 % 9) // 余数

	// 字符串类型，特点：通过双引号
	fmt.Println("武沛齐")
	fmt.Println("钓鱼要掉刀鱼，刀鱼到岛上钓")
	fmt.Println("alex" + "SB")
	//fmt.Println("alex" + 666)
	fmt.Println("alex" + "666")
	// 对比
	fmt.Println("1" + "2") // 结果："12"
	fmt.Println(1 + 2)     // 结果：3

	// 布尔类型，真假
	fmt.Println(1 > 2) // false  假
	fmt.Println(1 < 2) // true   真
	fmt.Println(1 == 2)
	fmt.Println(1 >= 2)
	fmt.Println("Alex" == "sb")

	// 超前
	if 2 > 1 {
		fmt.Println("叫爸爸")
	} else {
		fmt.Println("孙子")
	}

}
```

### 5.变量

可以理解为昵称。

*   声明 + 赋值

    ```go
    var sd string = "老男孩alex"
    fmt.Println(sd)

    var age int = 73
    fmt.Println(age)

    var flag bool = true
    fmt.Println(flag)
    ```
*   先声明后赋值

    ```go
    // 声明了一个字符类型变量 sd
    var sd string
    // 给sd变量赋值
    sd = "老男孩alex"
    fmt.Println(sd)
    ```

#### 5.1 声明变量的意义？

*   编写代码省事

    ```
    // 文本，请将文本输出3次："伤情最是晚凉天，憔悴斯人不堪怜。"
    var message string = "伤情最是晚凉天，憔悴斯人不堪怜。"
    fmt.Println(message)
    fmt.Println(message)
    fmt.Println(message)
    ```
*   存储结果，方便之后使用

    ```
    // 存储结果，方便之后使用
    var v1 int = 99
    var v2 int = 33
    var v3 int = v1 + v2
    var v4 int = v1 * v2
    var v5 int = v1 + v2 + v3 + v4
    fmt.Println(v1, v2, v3, v4, v5)
    ```
*   存储用户输入的值

    ```go
    var name string
    fmt.Scanf("%s", &name) // 用户输入字符串并赋值给name变量
    if name == "alex" {
        fmt.Println("用户名输入正确")
    } else {
        fmt.Println("用户名输入失败")
    }
    ```

#### 5.2 变量名要求

*   【要求】变量名必须只包含：字母、数字、下划线

    ```go
    var %1 string，错误
    var $ string，错误
    ```
*   【要求】数字不能开头

    ```go
    var 1 string  错误
    var 1name string  错误
    var _ string 正确
    ```
*   【要求】不能使用go语言内置的关键字

    ```
    var var string = "南通州北通州南北通州通南北"  错误
    ```

    ```
    break、default、func、interface、select、case、defer、go、map、struct、chan、else、goto、package、switch、const、fallthrough、if、range、type、continue、for、import、return、var
    ```
* 建议
  * 变量名见名知意：name/age/num ; v1、v2、v3
  * 驼峰式命名：myBossName / startDate

练习题：

```go
var n1 int 
var data bool
var _9 string
```

#### 5.3 变量简写

*   声明+赋值

    ```go
    var name string = "武沛齐"

    var name = "武沛齐"

    name := "武沛齐"  // 推荐
    ```
*   先声明再赋值

    ```go
    var name string
    var message string
    var data string

    var name,message,data string
    name = "武沛齐"
    message = "中奖了"
    data = "中了5000w"
    ```

因式分解，例如：声明5个变量，分别有字符串、整型

```go
var (
    name   = "武沛齐"
    age    = 18
    hobby  = "大保健"
    salary = 1000000
    gender string  // 只声明但不赋值，有一个默认： ""
    length int     // 只声明但不赋值，有一个默认： 0
    sb bool     // 只声明但不赋值，有一个默认： false
)
fmt.Println(name, age, hobby, salary, gender,length,sb)
```

扩展：go编译器会认为声明变量不使用 就是耍流氓。

#### 5.4 作用域

如果我们定义了大括号，那么在大括号中定义的变量。

* 不能被上级使用。
* 可以在同级使用。
* 可以再子级使用。

```go
package main

import "fmt"

func main() {
	name := "武沛齐"
	fmt.Println(name)
	if true {
		age := 18
		name := "alex"
		fmt.Println(age)
		fmt.Println(name)
	}
	fmt.Println(name)
}
```

全局变量和局部变量

* 全局变量，未写在函数中的变量称为全局变量；不可以使用`v1:=xx`方式进行简化；可以基于因式分解方式声明多个变量；项目中寻找变量时最后一环。
* 局部变量，编写在{}里面的变量；可以使用任意方式简化；可以基于因式分解方式声明多个变量；

```go
package main

import "fmt"

// 全局变量（不能以省略的方式）
var school string = "老男孩IT教育" // 可以
//var school = "老男孩IT教育" 	 // 可以
//school := "老男孩IT教育"  		 // 不可以

var (
	v1 = 123
	v2 = "你好"
	v3 int
)

func main() {

	name := "武沛齐" // 局部变量
	fmt.Println(name)
	if true {
		age := 18      // 局部变量
		name := "alex" // 局部变量
		fmt.Println(age)
		fmt.Println(name)
	}
	fmt.Println(name)
	fmt.Println(school)
	fmt.Println(v1, v2, v3)
}
```

### 6.常量

不可被修改的变量。

```go
package main

import "fmt"

func main() {
	// 定义变量
	//var name string = "武沛齐"
	//var name = "武沛齐"
	name := "武沛齐"
	name = "alex"
	fmt.Println(name)

	// 定义常量
	//const age int = 98
	const age = 98
	fmt.Println(age)
}
```

#### 6.1 因式分解

```go
package main

import "fmt"


func main() {
	// 定义变量
	//var name string = "武沛齐"
	//var name = "武沛齐"
	name := "武沛齐"
	name = "alex"
	fmt.Println(name)

	// 定义常量
	//const age int = 98
	const age = 98
	fmt.Println(age)

	// 常量因式分解
	const (
		v1 = 123
		v2 = 456
		pi = 9.9
	)
	fmt.Println(v1, v2, pi, gender)
}

```

#### 6.2 全局

```go
package main

import "fmt"

const Data = 999
const (
	pi     = 3.1415926
	gender = "男"
)

func main() {
	// 定义变量
	//var name string = "武沛齐"
	//var name = "武沛齐"
	name := "武沛齐"
	name = "alex"
	fmt.Println(name)

	// 定义常量
	//const age int = 98
	const age = 98
	fmt.Println(age)

	// 常量因式分解
	const (
		v1 = 123
		v2 = 456
		//pi = 9.9
	)
	fmt.Println(v1, v2, pi, gender)
}

```

#### 6.3 iota

可有可无，当做一个在声明常量时的一个计数器。

```go
package main

const (
	monday = iota + 1
	tuesday
	wednesday
	thursday
	friday
	saturday
	sunday
)

const (
	n1 = iota
	n2
	n3
)

func main() {

	// iota
	// 示例1
	/*
		const (
			v1 = 1
			v2 = 2
			v3 = 3
			v4 = 4
			v5 = 5
		)
		fmt.Println(v1, v2, v3, v4, v5)
	*/

	// 示例2
	/*
		const (
			v1 = iota
			v2
			v3
			v4
			v5
		)
		fmt.Println(v1, v2, v3, v4, v5)
	*/

	// 示例3
	/*
		const (
			v1 = iota + 2
			v2
			v3
			v4
			v5
		)
		fmt.Println(v1, v2, v3, v4, v5)
	*/

	// 示例4：
	/*
		const (
			v1 = iota + 2
			_
			v2
			v3
			v4
			v5
		)
		fmt.Println(v1, v2, v3, v4, v5)
	*/

}
```

### 7.输入

让用户输入数据，完成项目交互。

* fmt.Scan
* fmt.Scanln
* fmt.Scanf

```go
package main

import "fmt"

func main() {
	// 示例1：fmt.Scan
	/*
		var name string
		fmt.Println("请输入用户名：")
		fmt.Scan(&name)
		fmt.Printf(name)
	*/

	// 示例2：fmt.Scan
	var name string
	var age int

	fmt.Println("请输入用户名：")
	// 当使用Scan时，会提示用户输入
	// 用户输入完成之后，会得到两个值：count,用户输入了几个值；err，用输入错误则是错误信息
	_, err := fmt.Scan(&name, &age)
	if err == nil {
		fmt.Println(name, age)
	} else {
		fmt.Println("用户输入数据错误", err)
	}
	// 特别说明：fmt.Scan 要求输入两个值，必须输入两个，否则他会一直等待。
}

```

```go
package main

import "fmt"

func main() {
	// 示例1：fmt.Scanln
	/*
		var name string
		fmt.Print("请输入用户名：")
		fmt.Scanln(&name)
		fmt.Printf(name)
	*/

	// 示例2：fmt.Scanln

	var name string
	var age int
	fmt.Print("请输入用户名：")
	// 当使用Scanln时，会提示用户输入
	// 用户输入完成之后，会得到两个值：count,用户输入了几个值；err，用输入错误则是错误信息
	count, err := fmt.Scanln(&name, &age)
	fmt.Println(count, err)
	fmt.Println(name, age)

	// 特别说明：fmt.Scanln 等待回车。
}
```

```go
package main

import "fmt"

func main() {
	var name string
	var age int

	fmt.Print("请输入用户名：")
	_, _ = fmt.Scanf("我叫%s 今年%d 岁", &name, &age)
	fmt.Println(name, age)
}
```

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	reader := bufio.NewReader(os.Stdin)
	// line，从stdin中读取一行的数据（字节集合 -> 转化成为字符串）
	// reader默认一次能4096个字节（4096/3)
	//    1. 一次性读完，isPrefix=false
	// 	  2. 先读一部分，isPrefix=true，再去读取isPrefix=false
	line, _, _ := reader.ReadLine()
	data := string(line)
	fmt.Println(data)
}

```

### 8.条件语句

#### 8.1 最基本

```go
if 条件 {
    成立后，此代码块执行
}else{
    不成立，此代码块执行
}
```

```go
if 条件 {
    成立后，此代码块执行
}
```

示例：

```go
package main

func main() {
	/*
		if true {
			fmt.Println("666")
		}else{
			fmt.Println("999")
		}
	*/

	/*
		if 1 > 2 {
			fmt.Println("666")
		} else {
			fmt.Println("999")
		}
	*/

	/*
		flag := false
		if flag {
			fmt.Println("条件成立")
		}else{
			fmt.Println("条件不成立")
		}
	*/

	// 练习题1:用户输入姓名，判断是否正确
	/*
		var name string
		fmt.Print("请输入姓名：")
		fmt.Scanln(&name)
		if name == "alex" {
			fmt.Println("用户名输入正确")
		} else {
			fmt.Println("用户名输入错误")
		}
	*/
	// 练习题2:用户输入数字，判断奇数、偶数
	/*
		var number int
		fmt.Print("请输入数字：")
		fmt.Scanln(&number)
		if number % 2 == 0{
			fmt.Println("您输入的是偶数")
		}else{
			fmt.Println("您输入的是奇数")
		}
	*/
	// 练习题3:用户和密码，判断用户名密码是否正确。
	/*


		var username, password string
		fmt.Print("请输入用户名：")
		fmt.Scanln(&username)

		fmt.Print("请输入密码：")
		fmt.Scanln(&password)

		if username == "alex" && password == "sb" {
			fmt.Println("欢迎登录pornhub")
		} else {
			fmt.Println("用户名或密码错误")
		}
	*/
	// 练习题4:请输入用户名校验是否是VIP
	/*
		var username string
		fmt.Print("请输入用户名：")
		fmt.Scanln(&username)

		if username == "alex" || username == "eric" {
			fmt.Println("天上人间大VIP")
		} else {
			fmt.Println("屌丝")
		}
	*/
}

```

#### 8.2 多条件判断

```go
if 条件A{
    ...
}else if 条件B{
    ...
}else if 条件C{
    ...
}else{
    ...
}
```

示例：

```go
package main

import "fmt"

func main() {
	var length int
	fmt.Print("请输入你的长度：")
	fmt.Scanln(&length)

	if length < 1 {
		fmt.Println("没用的东西，还特么是坑")
	} else if length < 6 {
		fmt.Println("刚刚能用")
	} else if length < 18 {
		fmt.Println("生活和谐")
	} else {
		fmt.Println("太特么大了")
	}
}
```

#### 8.3 嵌套

```go
package main

import "fmt"

func main() {
	fmt.Println("欢迎致电10086，1.话费相关；2.业务办理；3.人工服务。")

	var number int
	fmt.Scanln(&number)

	if number == 1 {
		fmt.Println("话费服务，1.交话费；2.查询。")
		var n1 int
		fmt.Scanln(&n1)
		if n1 == 1 {
			fmt.Println("缴话费啦")
		} else if n1 == 2 {
			fmt.Println("查话费了")
		} else {
			fmt.Println("输入错误")
		}
	} else if number == 2 {
		fmt.Println("业务办理")
	} else if number == 3 {
		fmt.Println("人工服务")
	} else {
		fmt.Println("输入错误")
	}
	
	// 建议：条件的嵌套不要太多
}
```

## 基础知识

* switch case语句，条件判断。
* for循环语句，循环。
* goto语法，不太建议使用。
* 字符串格式化，“拼接”数据。
* 运算符

### 1.switch语句

```go
package main

func main() {

	// 表达式
	/*
		switch 1 + 1 {
		case 1:
			fmt.Println("等于1")
		case 2:
			fmt.Println("等于2")
		case 3:
			fmt.Println("等于3")
			fmt.Println("等于3")
		default:
			fmt.Println("都不满足")
		}
	*/
	// 变量
	/*
		var age int
		fmt.Scanln(&age)
		switch age {
		case "1":
			fmt.Println("等于1")
		case 2:
			fmt.Println("等于2")
		case 3:
			fmt.Println("等于3")
			fmt.Println("等于3")
		default:
			fmt.Println("都不满足")
		}
	*/
	// 注意事项: 数据类型一致的情况。 正确：1>2   3+4    错误： 1>"3"   5+"6"
}
```

### 2.for循环

#### 2.1 死循环

```go
for {
    ...
}
```

#### 2.2 布尔值条件

```go
for 1>2 {
    ...
}
```

```go
flag := true
for flag {
    
}
```

#### 示例

```go
package main

func main() {

	// 示例1：死循环
	/*
		fmt.Println("开始")
		for {
			fmt.Println("红鲤鱼与绿鲤鱼与驴")
			time.Sleep(time.Second * 1) // 等一秒再继续执行
		}
		fmt.Println("结束")
	*/

	// 示例2：
	/*
		fmt.Println("开始")
		for 2 > 1 {
			fmt.Println("红鲤鱼与绿鲤鱼与驴")
			time.Sleep(time.Second * 1) // 等一秒再继续执行
		}
		fmt.Println("结束")
	*/

	// 示例3：
	/*

		fmt.Println("开始")
		number := 1
		for number < 5 {
			fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
			number = 10
		}
		fmt.Println("结束")
	*/

	// 示例4：
	/*
		fmt.Println("开始")
		number := 1
		for number < 5 {
			fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
			number = number + 1
		}
		fmt.Println("结束")

	*/

	// 示例5：布尔类型的变量
	/*
		fmt.Println("开始")
		flag := true
		for flag {
			fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
			flag = false
		}
		fmt.Println("结束")

	*/

}
```

#### 2.3 变量&条件

```go
for i:=1;i<10; {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
    i = i + 1
}
```

#### 2.4 变量&条件&变量赋值

```go
for i:=1;i<10;i=i+1 {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
}
// 简化为：
for i:=1;i<10;i++ {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
}
```

```go
for i := 1; i < 10; i = i + 2 {
    fmt.Println("钓鱼要掉刀鱼，刀鱼要到岛上钓")
}
```

扩展：对于 i=i+1简写 --> `i++`

```go
num := 10
fmt.Println(num)
num++ // 等价于 num = num + 1
fmt.Println(num)
```

```go
num := 10
fmt.Println(num)
num-- // 等价于 num = num - 1
fmt.Println(num)
```

#### 2.5 continue

在for循环中，当循环遇到continue关键字时，会停止当前循环，开始下一次循环。

```go
for{
    fmt.Println("Alex今天不在家，沛齐你来陪我呀！！！")
    continue
    fmt.Println("让苑昊也一起来")
}
```

案例1：使用循环输出 1 2 3 4 5 6 8 9 10，即：10以内除7以外的整数。

```go
for i:=1;i<=10;i++{
    if i == 7{
        continue
    }
    fmt.Println(i)
}
```

案例2：for循环嵌套

```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        fmt.Println(i,j)
    }
}

>>> 输出：
1 1
1 2
1 3
1 4
2 1
2 2
2 3
2 4
```

案例3：for循环嵌套 + continue

```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        if j == 3{
            continue
        }
        fmt.Println(i,j)
    }
}

>>> 输出：
1 1
1 2
1 4
2 1
2 2
2 4
```

#### 2.6 break

在for循环中时，循环中一旦遇到break，跳出循环。

```go
for{
    fmt.Println("王老汉、李老汉、张老汉")
    break
    fmt.Println("alex老婆满身大汗")
}
```

案例1：猜数字，设定一个理想数字比如：66，一直提示让用户输入数字，如果比66大，则显示猜测的结果大了；如果比66小，则显示猜测的结果小了;只有输入等于66，显示猜测结果正确，然后退出循环。

```go
fmt.Print("开始")
data := 66
for{
    var userInputNumber int
    fmt.Print("请输入数字：")
    fmt.Scanln(&userInputNumber)
    if userInputNumber > data {
        fmt.Println("大了")
    } else if userInputNumber < data {
        fmt.Println("小了")
    } else {
        fmt.Println("恭喜你猜对了")
        break
    }
}
fmt.Print("结束")
```

案例2：

```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        if j == 3{
            break
        }
        fmt.Println(i,j)
    }
}

>>> 输出：
1 1
1 2
2 1
2 2
```

```go
for i:=1;i<3;i++{
    // i=1
    // i=2
    for j:=1;j<5;j++{
        // j=1/2/3/4
        if j == 3{
            break
        }
        fmt.Println(i,j)
    }
    break
}

>>> 输出：
1 1
1 2
```

对for进行打标签，然后通过break和continue就可以实现多层循环的跳出和终止。

```go
f1:
	for i := 1; i < 3; i++ {
		// i=1
		// i=2
		for j := 1; j < 5; j++ {
			// j=1/2/3/4
			if j == 3 {
				continue f1
			}
			fmt.Println(i, j)
		}
	}

>>> 输出：
1 1
1 2
2 1
2 2
```

```go
f1:
	for i := 1; i < 3; i++ {
		// i=1
		// i=2
		for j := 1; j < 5; j++ {
			// j=1/2/3/4
			if j == 3 {
				break f1
			}
			fmt.Println(i, j)
		}
	}

>>> 输出：
1 1
1 2
```

### 3.goto语句

跳跃到指定的行，然后向下执行代码。

```go
package main

import "fmt"

func main() {
	var name string
	fmt.Print("请输入姓名：")
	fmt.Scanln(&name)

	if name == "wupeiqi" {
		// svip
		goto SVIP
	} else if name == "yuanhao" {
		// vip
		goto VIP
	}
	fmt.Println("预约...")
VIP:
	fmt.Println("等号...")
SVIP:
	fmt.Println("进入...")
}
```

### 4.字符串格式化

将数据格式化成为特定格式的字符串时，可以使用字符串格式化。

```go
package main

import "fmt"

func main() {
	var name, address, action string

	fmt.Print("请输入姓名：")
	fmt.Scanln(&name)

	fmt.Print("请输入位置：")
	fmt.Scanln(&address)

	fmt.Print("请输入行为：")
	fmt.Scanln(&action)

	result := fmt.Sprintf("我叫%s,在%s正在干%s", name, address, action)
	//result := "我叫" + name + "在" + address + "干" + action
	fmt.Println(result)
}

```

### 5.运算符

#### 5.1 算数运算符

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133268.png)

#### 5.2 关系运算符

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133685.png)

#### 5.3 逻辑运算符

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133060.png)

```go
if !true {
    fmt.Println("你是风儿我是沙，去你吗的风河沙")
}
```

#### 5.4 位运算符

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133355.png)

必知必会概念：

*   计算机中的 存储、运算、网络传输等任何的行为，本质上都是二进制的操作。例如：01010101。

    ```go
      A				                  B
    hello   -> 0101010010101  ->    hello
    ```
*   信息表现形式

    ```
    二进制表示：0101010010101   ->  hello
    十进制表示：1921            ->  hello
    ```
*   十进制和二进制的转换关系

    | 十进制 | 二进制  |
    | --- | ---- |
    | 0   | 0    |
    | 1   | 1    |
    | 2   | 10   |
    | 3   | 11   |
    | 4   | 100  |
    | 5   | 101  |
    | 6   | 110  |
    | 7   | 111  |
    | 8   | 1000 |
    | 9   | 1001 |
    | 10  | 1010 |
    | ... | ...  |

    *   二进制转换为十进制

        ```
        10101         ->   2**4 + 2**2 + 2**0 => 16 + 4 + 1 => 21
        101010010101  ->   2**11 + 2**9 + ....
        ```
    *   十进制转换成二进制

        ```
        99            -> 64 + 32 + 2 + 1  -> 2**6 + 2**5 + 2**1 + 2*0  -> 1100011
        ```

位运算指的是二进制之间的运算：

```go
// 1.按位进行与运算（全为1，才得1）
r1 := 5 & 99
5  -> 0000101
99 -> 1100011
      0000001   -> 1

// 2.按位进行或运算（只要有1，就得1）
r2 := 5 | 99
5  -> 0000101
99 -> 1100011
      1100111   -> 2**6 + 2**5 + 2**2 + 2**1 + 2**0 = 64 + 32 + 4 + 2 + 1 = 103

// 3.按位进行异或运算（上下不同，就得1）
r3 := 5 ^ 99
5  -> 0000101
99 -> 1100011
      1100110   -> 2**6 + 2**5 + 2**2 + 2**1 = 64 + 32 + 4 + 2 = 102

// 4.按位向左移动
r4 := 5 << 2
        5  -> 101
向左移动2位  -> 10100  -> 2**4 + 2**2 = 16 + 4 = 20

// 5.按位向右移动
r5 := 5 >> 1
        5  -> 101
向右移动1位  -> 10  -> 2**1 = 2

// 6.比较清除   // 以前面的值为基准，让前面的和后面的值的二进制位进行比较，如果两个位置都是1，则讲前面的值的那个位置置0
r6 := 5 &^ 99
5  -> 0000101
99 -> 1100011
      0000100     -> 2**2 = 4
```

#### 5.5 赋值运算符

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133751.png)

```go
age := 19
age = 99

age = age + 9  // age+=9
age = age - 9  // age-=9
age = age * 9  // age*=9
...
```

#### 运算符的优先级

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/202310151133012.png)

```
Precedence    Operator
    5             *  /  %  <<  >>  &  &^
    4             +  -  |  ^
    3             ==  !=  <  <=  >  >=
    2             &&
    1             ||
```

```go
v1 := 3 + 2 * 2
v2 := 8 == 5 & 99
```

注意：不要想办法去记住他，使用括号。

参考地址：

* https://golang.org/ref/spec#Arithmetic\_operators
* https://www.runoob.com/go/go-operators.html

叮嘱：不要太过于用心去背、记，主要认识即可。优先级记不住就用括号。

## 数据类型

> 写程序 等价于 写作文

数据类型，其实就是各种各样类型的数据。

Go语言中常见的数据类型有挺多，例如：

* 整型，用于表示整数。
* 浮点型，用于表示小数。
* 布尔型，用于表示真/假。
* 字符串，用于表示文本信息。
* 数组，用于表示多个数据（数据集合）
* 指针，用于表示内存地址的类型。
* 切片，用于表示多个数据（数据集合）
* 字典，用于表示键值对结合。
* 结构体，用于自定义一些数据集合。
* 接口，用于约束和泛指数据类型。

注意：关于“值类型”和“引用类型” [https://github.com/go101/go101/wiki/About-the-terminology-%22reference-type%22-in-Go](https://github.com/go101/go101/wiki/About-the-terminology-%22reference-type%22-in-Go)

### 今日概要

* 整型，用于表示整数。
* 浮点型，用于表示小数。
* 布尔型，用于表示真/假。
* 字符串，用于表示文本信息。
* 数组，用于表示多个数据（数据集合）\["长沙","东莞","惠州"]

### 1.整型

Go中的整型分为有符号和无符号两大类，有符号的包含负值，无符号不包含负值。

有符号整型：

* int8（-128 -> 127）
* int16（-32768 -> 32767）
* int32（-2,147,483,648 -> 2,147,483,647）
* int64（-9,223,372,036,854,775,808 -> 9,223,372,036,854,775,807）
* int
  * 在 32 位操作系统上使用 32 位（-2,147,483,648 -> 2,147,483,647） 2\*\*32
  * 在 64 位操作系统上使用 64 位（-9,223,372,036,854,775,808 -> 9,223,372,036,854,775,80）2\*\*64

无符号整数：

* uint8（0 -> 255）
* uint16（0 -> 65,535）
* uint32（0 -> 4,294,967,295）
* uint64（0 -> 18,446,744,073,709,551,615）
* uint
  * 在 32 位操作系统上使用32 位（0 -> 4,294,967,295） 2\*\*32
  * 64 位操作系统上使用 64 位（0 -> 18,446,744,073,709,551,615） 2\*\*64

不同整型可表示的数据范围不同，我们需要根据自己的需求来选择适合的类型。

#### 1.1 整型之间的转换

```go
data := intXXX(其他整型)
```

```go
var v1 int8 = 10
var v2 int16 = 18
v3 := int16(v1) + v2
fmt.Println(v3, reflect.TypeOf(v3))
```

注意：

* 地位转向高位，没问题。
*   高位转向低位，可能有问题

    ```go
    var v1 int16 = 130
    v2 := int8(v1)
    fmt.Println(v2)
    ```

#### 1.2 整型与字符串的转换

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

func main() {

	// 整型转换为字符串类型
	/*
		v1 := 19
		result := strconv.Itoa(v1)
		fmt.Println(result, reflect.TypeOf(result))
		var v2 int8 = 17
		data := strconv.Itoa(int(v2))
		fmt.Println(data,reflect.TypeOf(data))
	*/

	// 字符串转换为整型：转换后是int类型;可能存在错误
	/*
		v1 := "666"
		result, err := strconv.Atoi(v1)
		if err == nil {
			fmt.Println("转换成功", result,reflect.TypeOf(result))
		} else {
			fmt.Println("转换失败")
		}
	
	*/
}
```

#### 1.3 进制转换

* Go代码中：
  * 十进制，整型的方式存在。
  * 其他进制，是以字符串的形式存在。
* 整形，10进制数。

十进制转换为其他进制：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"reflect"
	"strconv"
)

func main() {
	v1 := 99
	// 整型(十进制）转换为:二进制、八进制、十六进制
	r1 := strconv.FormatInt(int64(v1), 16)
	fmt.Println(r1, reflect.TypeOf(r1))

}

```

其他进制转换为十进制：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"reflect"
	"strconv"
)

func main() {
	// data，要转换的文本
	// 2，把文档当做二进制去转换成 十进制（整型）
	// 16，转换的过程中对结果进行约束
	// 结果：如果转换成功，则将err设置为nil，result则永远以int64的类型返回。
	data := "1001000101"
	result, err := strconv.ParseInt(data, 2, 0)
	fmt.Print(result, err, reflect.TypeOf(result))
}
```

提醒：通过ParseInt将字符串转换为10进制时，本质上与Atoi是相同的。

#### 1.4 常见数学运算

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Abs(-19))                // 取绝对值
	fmt.Println(math.Floor(3.14))             // 向下取整
	fmt.Println(math.Ceil(3.14))              // 向上取整
	fmt.Println(math.Round(3.3478))           // 就近取整
	fmt.Println(math.Round(3.5478*100) / 100) // 保留小数点后两位
	fmt.Println(math.Mod(11, 3))              // 取余数，同11 % 3
	fmt.Println(math.Pow(2, 5))               // 计算次方，如：2的5次方
	fmt.Println(math.Pow10(2))                // 计算10次方，如：2的10次方
	fmt.Println(math.Max(1, 2))               // 两个值，取较大值
	fmt.Println(math.Min(1, 2))               // 两个值，取较小值
	// ...
}
```

#### 1.5 指针/nil/声明变量/new

*   声明变量

    ```go
    var v1 int 
    v2 := 999
    ```
*   指针

    ```go
    var v3 *int    
    v4 := new(int)   
    ```
*   new关键字

    ```
    new用于创建内存并进行内部数据的初始化，并返回一个指针类型。
    ```
*   nil

    ```
    nil指go语言中的空值。
    var v100 *int
    var v101 *int8
    ```

问题：

*   为什么要有指针？

    ```
    为了节省内存，不重复开辟空间去存储数据。
    ```
* int和\*int是两种不同的数据类型，不等。（之后专门讲指针细说）

#### 1.6 超大整型

**第一步：创建对象**

创建超大整型对象

```go
// 第一步：创建一个超大整型的一个对象
var v1 big.Int
var v2 big.Int

// 第二步：在超大整型对象中写入值
v1.SetInt64(9223372036854775807)
fmt.Println(v1)

v2.SetString("92233720368547758089223372036854775808", 10)
fmt.Println(v2)
```

```go
// 第一步：创建一个超大整型的一个对象
v3 := new(big.Int)
v4 := new(big.Int)

// 第二步：在超大整型对象中写入值
v3.SetInt64(9223372036854775807)
fmt.Println(v3)

v4.SetString("92233720368547758089223372036854775808", 10)
fmt.Println(v4)
```

推荐：使用指针的方式，即：使用new来进行创建和初始化。

**第二步：加减乘除**

超大对象进行加减乘除

```go
n1 := new(big.Int)
n1.SetInt64(89)

n2 := new(big.Int)
n2.SetInt64(99)

result := new(big.Int)
result.Add(n1, n2)

fmt.Println(result)
```

```go
n1 := big.NewInt(89)

n2 := big.NewInt(99)

result := new(big.Int)
result.Add(n1, n2)

fmt.Println(result)
```

其他：

```go
v1 := big.NewInt(11)
v2 := big.NewInt(3)
result := new(big.Int)

// 加
result.Add(v1, v2)
fmt.Println(result)
// 减
result.Sub(v1, v2)
fmt.Println(result)

// 乘
result.Mul(v1, v2)
fmt.Println(result)

// 除（地板除，只能得到商）
result.Div(v1, v2)
fmt.Println(result)

// 除，得商和余数
minder := new(big.Int)
result.DivMod(v1, v2, minder)
fmt.Println(result, minder)
```

**第三步：关于结果**

```go
n1 := new(big.Int)
n1.SetString("92233720368547758089223372036854775808", 10)

n2 := new(big.Int)
n2.SetString("11111192233720368547758089223372036854775808", 10)

result := new(big.Int)
result.Add(n1, n2)

fmt.Println(result.String())
```

**最后建议**

* 尽量new方式去初始化并返回一个指针类型的方式。
*   易错的点（int类型和\*int类型）

    ```go
    var v1 big.Int
    v1.SetString("92233720368547758089223372036854775808", 10)

    var v2 big.Int
    v2.SetString("2", 10)

    //result := new(big.Int)
    var result big.Int
    result.Add(&v1, &v2)
    fmt.Println(result.String())
    ```

#### 2.浮点型

浮点数，计算机中小数的表示方式，如：`3.14`

Go语言中提供了两种浮点型：

* float32，用32位（4个字节）来存储浮点型。
* float64，用64位（8个字节）来存储浮点型。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	var v1 float32
	v1 = 3.14
	v2 := 99.9
	v3 := float64(v1) + v2
	fmt.Println(v1, v2, v3)
}
```

**2.1 非精确**

float类型，计算机中小数的非精确的表示方式，如：`3.14`

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	var v1 float32
	v1 = 3.14
	v2 := 99.9
	v3 := float64(v1) + v2
	fmt.Println(v1, v2, v3)

	v4 := 0.1
	v5 := 0.2
	result := v4 + v5
	fmt.Println(result)

	v6 := 0.3
	v7 := 0.2
	data := v6 + v7
	fmt.Println(data)
}
```

```
3.14 99.9 103.04000010490418
0.30000000000000004
0.5
```

**2.2 float底层存储原理**

```go
var price float32 = 0.29
```

**第一步：浮点型转换为二进制**

* 整数部分，直接转换为二进制（10进制转换为2进制），即：`100111`
*   小数部分，让小数部分乘以2，结果小于1则将结果继续乘以2，结果大于1则讲结果-1继续乘以2，结果等于1则结束。

    ```
    0.29 * 2 = 0.58       // 小于1，则继续乘
    0.58 * 2 = 1.16		  // 大于1，则减1继续乘
    0.16 * 2 = 0.32		  // 小于1，则继续乘
    0.32 * 2 = 0.64       // 小于1，则继续乘
    0.64 * 2 = 1.28       // 大于1，则减1继续乘
    0.28 * 2 = 0.56       // 小于1，则继续乘
    0.56 * 2 = 1.12       // 大于1，则减1继续乘
    0.12 * 2 = 0.24       // 小于1，则继续乘    
    0.24 * 2 = 0.48       // 小于1，则继续乘
    0.48 * 2 = 0.96       // 小于1，则继续乘
    0.96 * 2 = 1.92       // 大于1，则减1继续乘
    0.92 * 2 = 1.84       // 大于1，则减1继续乘
    0.84 * 2 = 1.68       // 大于1，则减1继续乘
    0.68 * 2 = 1.36       // 大于1，则减1继续乘
    0.36 * 2 = 0.72       // 小于1，则继续乘
    0.72 * 2 = 1.44       // 大于1，则减1继续乘
    0.44 * 2 = 0.88       // 小于1，则继续乘
    0.88 * 2 = 1.76       // 大于1，则减1继续乘
    0.76 * 2 = 1.52       // 大于1，则减1继续乘
    0.52 * 2 = 1.04       // 大于1，则减1继续乘
    0.04 * 2 = 0.08       // 小于1，则继续乘
    0.08 * 2 = 0.16       // 小于1，则继续乘
    0.16 * 2 = 0.32       // 小于1，则继续乘（与第三行相同，这样会一直循环执行下去）
    ...

    将相乘之后等结果的整数部分拼接起来，所以 0.29的 二进制表示：010010100011110101110000101000111...
    ```

所以，最终39.29的二进制表示为：`100111.010010100011110101110000101000111...`

**第二步：科学计数法表示**

`100111.010010100011110101110000101000111...`

$$
1.00111010010100011110101110000101000111... * 2^5
$$

**第三步：存储**

以float32为例来进行存储，用32位来存储浮点型。

* sign，用1位来表示浮点数正负，0表示正数；1表示负数。
* exponent，用8位来表示共有256种（0\~255），含正负值（-127 \~ 128）。例如：5想要存储到exponent位的话，需要让 5 + 127 = 132，再讲132转换二进制，存储到exponent。（132的二进制是：01000010）
* fraction，存储小数点后的所有数据。

float64和float32类似，只是用于表示各部分的位数不同而已，其中：`sign=1位`、`exponent=11位`、`fraction=52位`，也就意味着可以表示的范围更大了。

**2.3 decimal**

Go语言内部没有decimal。

第三方包，则需要在本地的Go环境中先安装再使用。第三方包源码地址：https://github.com/shopspring/decimal 。

**第一步：安装第三发的包**

```
go get github.com/shopspring/decimal 
```

命令执行完成之后，在 `$GOPATH/src`的目录下就会出现 `github/shopspring/decimal`的目录，这就是第三方模块安排的位置。

**第二步：使用decimal包**

```go
package main

import (
	"fmt"
	"github.com/shopspring/decimal"
)

func main() {

	var v1 = decimal.NewFromFloat(0.0000000000019)
	var v2 = decimal.NewFromFloat(0.29)

	var v3 = v1.Add(v2)

	var v4 = v1.Sub(v2)

	var v5 = v1.Mul(v2)

	var v6 = v1.Div(v2)
	
    fmt.Println(v3, v4, v5, v6) // 输出：0.2900000000019（也可以调用String方法）
    
    
	var price = decimal.NewFromFloat(3.4626)
	var data1 = price.Round(1) 		// 保留小数点后1位（四舍五入）
	var data2 = price.Truncate(1)	// 保留小数点后1位
	fmt.Println(data1, data2) // 输出：3.5  3.4
}
```

### 3.布尔类型

表示真假，一般是和条件等配合使用，用于满足某个条件时，执行某个操作。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"strconv"
)

func main() {
	// 字符串 转换 布尔类型
	// true:"1", "t", "T", "true", "TRUE", "True"
	// false:"0", "f", "F", "false", "FALSE", "False"
	//false,err错误信息
	v1, err := strconv.ParseBool("t")
	fmt.Println(v1, err)

	// 布尔类型 转换 字符串
	v2 := strconv.FormatBool(false)
	fmt.Println(v2)
}

```

### 4.字符串

在编写程序时，使用字符串来进行文本的处理，例如：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	var name string = "alex"
	fmt.Printf(name)

	title := "生活要想过得去，头上总得带点绿"
	fmt.Printf(title)
}
```

#### 4.1 字符串的底层存储

计算机中所有的操作和数据最终都是二进制，即：1000100001011...

Go语言中的字符串是utf-8编码的序列。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
    // unicode字符集：文字 -> 码点（ucs4, 4个字节表示）
    // utf-8编码，对unicode字符集的码点进行编码最终得到：1000100001
	var name string = "武沛齐"
    fmt.Printf(name)
}
```

课上代码示例：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"strconv"
	"unicode/utf8"
)

func main() {
	// 1. 本质是utf-8编码的序列
	var name string = "武沛齐"

	// 武 => 11100110 10101101 10100110
	fmt.Println(name[0], strconv.FormatInt(int64(name[0]), 2))
	fmt.Println(name[1], strconv.FormatInt(int64(name[1]), 2))
	fmt.Println(name[2], strconv.FormatInt(int64(name[2]), 2))

	// 武 => 11100110 10110010 10011011
	fmt.Println(name[3], strconv.FormatInt(int64(name[3]), 2))
	fmt.Println(name[4], strconv.FormatInt(int64(name[4]), 2))
	fmt.Println(name[5], strconv.FormatInt(int64(name[5]), 2))

	// 武 => 11101001 10111101 10010000
	fmt.Println(name[6], strconv.FormatInt(int64(name[6]), 2))
	fmt.Println(name[7], strconv.FormatInt(int64(name[7]), 2))
	fmt.Println(name[8], strconv.FormatInt(int64(name[8]), 2))

	// 2. 获取字符串的长度：9（字节长度）
	fmt.Println(len(name))

	// 3. 字符串转换为一个"字节集合"
	byteSet := []byte(name)
	fmt.Println(byteSet) // [230,173,166,230,178,155,233,189,144]

	// 4. 字节的集合转换为字符串
	byteList := []byte{230, 173, 166, 230, 178, 155, 233, 189, 144}
	targetString := string(byteList)
	fmt.Println(targetString)

	// 5. 将字符串转换为 unicode字符集码点的集合    6b66 ->  武  6c9b->沛   9f50->齐
	tempSet := []rune(name)
	fmt.Println(tempSet) // [27494 27803 40784]
	fmt.Println(tempSet[0], strconv.FormatInt(int64(tempSet[0]), 16))
	fmt.Println(tempSet[1], strconv.FormatInt(int64(tempSet[1]), 16))
	fmt.Println(tempSet[2], strconv.FormatInt(int64(tempSet[2]), 16))

	// 6. "rune集合" 转换 为字符串
	runeList := []rune{27494, 27803, 40784}
	targetName := string(runeList)
	fmt.Println(targetName)

	// 7. 长度的处理（获取字符长度）
	runeLength := utf8.RuneCountInString(name)
	fmt.Println(runeLength)
}
```

#### 4.2 字符串常见功能

字符串属于在程序中最常见用的数据类型，所以Go中为字符串提供了很多常见的操作。

**4.2.1 获取长度**

```go
package main

import (
   "fmt"
   "unicode/utf8"
)

func main() {
   var name string = "武沛齐"

   fmt.Println( len(name) )                    // 获取 字节 长度，输出：8
   fmt.Println( utf8.RuneCountInString(name) ) // 获取字符长度，输出：3
}
```

**4.2.2 是否以xx开头**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "武沛齐"

   result := strings.HasPrefix(name, "武")

   fmt.Println(result) // 输出：true
}
```

**4.2.3 是否以xx结尾**

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	name := "武沛齐"

	result := strings.HasSuffix(name, "齐")

	fmt.Println(result) // 输出：true
}
```

**4.2.4 是否包含**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "抬老子的意大利炮来"
   result := strings.Contains(name, "老子")

   fmt.Println(result) // 输出：true
}
```

**4.2.5 变大写**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "wupeiqi"

   result := strings.ToUpper(name)

   fmt.Println(result) // 输出：WUPEIQI
}
// 注意：result是大写；name依然是小写。
```

**4.2.6 变小写**

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	name := "WUPEIQI"

	result := strings.ToLower(name)

	fmt.Println(result) // 输出：wupeiqi
}

```

**4.2.7 去两边**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "wupeiqi"

   result1 := strings.TrimRight(name, "qi") // 去除右边的qi
   result2 := strings.TrimLeft(name, "w")   // 去除左边的w
   result3 := strings.Trim(name, "w")       // 去除两边的w

   fmt.Println(result1, result2, result3) // 输出：wupe upeiqi upeiqi
}
```

**4.2.8 替换**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "wupeipeiqi"

   result1 := strings.Replace(name, "pei", "PE", 1)  // 找到pei替换为PE，从左到右找第一个替换
   result2 := strings.Replace(name, "pei", "PE", 2)  // 找到pei替换为PE，从左到右找前两个替换
   result3 := strings.Replace(name, "pei", "PE", -1) // 找到pei替换为PE，替换所有

   fmt.Println(result1, result2, result3)
}
```

**4.2.9 分割**

```go
package main

import (
   "fmt"
   "strings"
)

func main() {
   name := "抬老子的意大利的炮来"
   result := strings.Split(name, "的")

   // 根据`的`进行切割，获取一个切片（类似于一个数组）
   fmt.Println(result) // [ 抬老子, 意大利, 炮来 ]
}
```

**4.2.10 拼接**

可以使用 `+` 让两个字符串进行拼接，但这样的拼接效率会非常的低，不建议使用，建议大家使用以下的方式：

```go
package main

import (
	"bytes"
	"fmt"
	"strings"
)

func main() {
	// 不建议
	message := "我爱" + "北京天安门"
	fmt.Println(message)

	// 建议：效率高一些
	dataList := []string{"我爱", "北京天安门"}
	result := strings.Join(dataList, "")
	fmt.Println(result) // 我爱北京天安门

	// 建议：效率更高一些（go 1.10之前）
	var buffer bytes.Buffer
	buffer.WriteString("你想")
	buffer.WriteString("我干")
	buffer.WriteString("他")
	data := buffer.String()
	fmt.Print(data)

	// 建议：效率更更更更高一些（go 1.10之后）
	var builder strings.Builder
	builder.WriteString("哈哈哈")
	builder.WriteString("去你的吧")
	value := builder.String()
	fmt.Print(value)
}
```

**4.2.11 string转换为int**

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	num := "666"

	// 内部调用的就是 ParseInt
	var data, _ = strconv.Atoi(num)
	fmt.Println(data)
    
    // 整型转字符串（strconv.ParseInt 和 strconv.FormatInt 可用处理进制转换）
    // 十进制：整型； 其他进制：字符串形式 
    var result, err = strconv.ParseInt(num, 10, 32)
	fmt.Println(result, err)
}
```

**4.2.12 int转换为string**

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	var result = strconv.Itoa(888)
	fmt.Println(result)
}
```

**4.2.13 字符串 和 “字节集合”**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"strconv"
	"unicode/utf8"
)

func main() {

	var name string = "武沛齐"

	// 字符串转换为一个"字节集合"
	byteSet := []byte(name)
	fmt.Println(byteSet) // [230,173,166,230,178,155,233,189,144]

	// 字节的集合转换为字符串
	byteList := []byte{230, 173, 166, 230, 178, 155, 233, 189, 144}
	targetString := string(byteList)
	fmt.Println(targetString)

}
```

**4.2.14 字符串 和 “rune集合”**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"strconv"
	"unicode/utf8"
)

func main() {

	var name string = "武沛齐"

	// 将字符串转换为 unicode字符集码点的集合    6b66 ->  武  6c9b->沛   9f50->齐
	tempSet := []rune(name)
	fmt.Println(tempSet) // [27494 27803 40784]
	fmt.Println(tempSet[0], strconv.FormatInt(int64(tempSet[0]), 16))
	fmt.Println(tempSet[1], strconv.FormatInt(int64(tempSet[1]), 16))
	fmt.Println(tempSet[2], strconv.FormatInt(int64(tempSet[2]), 16))

	// "rune集合" 转换 为字符串
	runeList := []rune{27494, 27803, 40784}
	targetName := string(runeList)
	fmt.Println(targetName)
}
```

**4.2.15 string 和 字符**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"unicode/utf8"
)

func main() {
	// 数字转字符串
	v1 := string(65)
	fmt.Println(v1) // A
    
    v2 := string(27494)
	fmt.Println(v2) // 武
    
	// 字符串转数字
	v3, size := utf8.DecodeRuneInString("A")
	fmt.Println(v3, size) // 65    1
    
    v4, size := utf8.DecodeRuneInString("武")
	fmt.Println(v4, size) // 27494 3

}
```

应用场景：生成一个随机数，然后调用string得到一个随机的字符。

#### 4.3 索引切片和循环

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	var name string = "武沛齐"

	// 1. 索引获取字节
	v1 := name[0]
	fmt.Println(v1)  // 230

	// 2. 切片获取字节区间
	v2 := name[0:3]
	fmt.Println(v2)  // 武

	// 3. 手动循环获取所有字节
    /*
        0 230
        1 173
        2 166
        3 230
        4 178
        5 155
        6 233
        7 189
        8 144
    */
	for i := 0; i < len(name); i++ {
		fmt.Println(i, name[i]) 
	}

	// 4. for range 循环获取所有字符
    /*
        0 27494 武
        3 27803 沛
        6 40784 齐
	*/
	for index, item := range name {
        fmt.Println(index, item, string(item))
	}

	// 5.转换成rune集合 [27494,27803,40784]
	dataList := []rune(name)
	fmt.Println(dataList[0], string(dataList[0]))

}
```

### 5.数组

数组，定长且元素类型一致的数据集合。

```go
// 方式一：先声明再赋值（声明时内存中已开辟空间，内存初始化的值是0）
var numbers [3]int
numbers[0] = 999
numbers[1] = 666
numbers[2] = 333

// 方式二：声明+赋值
var names = [2]string{"武沛齐","alex"}

// 方式三：声明+赋值 + 指定位置
var ages = [3]int{0:87,1:73,2:99}

// 方式四：省略个数
var names = [...]string{"武沛齐","alex"}
var ages = [...]int{  0:87,  2:99 }
```

```go
// 声明 指针类型的数组（指针类型），不会开辟内存初始化数组中的值，numbers = nil
var numbers *[3]int

// 声明数组并初始化，返回的是 指针类型的数组（指针类型）
numbers := new([3]int)
```

#### 5.1 数组内存管理

数组，定长且元素类型一致的数据集合。

必备知识点：

* 数组的内存是连续的。
* 数组的内存地址实际上就是数组第一个元素的内存地址。
*   每个字符串的内部存储：`len` + `str`

    ```go
    type stringStruct struct {
    	str unsafe.Pointer
    	len int
    }
    ```

示例1：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	nums := [3]int8{11, 22, 33}

	fmt.Printf("数组的内存地址：%p \n", &nums)
	fmt.Printf("数组第1个元素的内存地址：%p \n", &nums[0])
	fmt.Printf("数组第2个元素的内存地址：%p \n", &nums[1])
	fmt.Printf("数组第3个元素的内存地址：%p \n", &nums[2])
}

>>> 输出
数组的内存地址：0xc00001604a 
数组第1个元素的内存地址：0xc00001604a 
数组第2个元素的内存地址：0xc00001604b 
数组第3个元素的内存地址：0xc00001604c 
```

示例2：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	nums := [3]int32{11, 22, 33}

	fmt.Printf("数组的内存地址：%p \n", &nums)
	fmt.Printf("数组第1个元素的内存地址：%p \n", &nums[0])
	fmt.Printf("数组第2个元素的内存地址：%p \n", &nums[1])
	fmt.Printf("数组第3个元素的内存地址：%p \n", &nums[2])
}

>>> 输出
数组的内存地址：0xc0000b4004 
数组第1个元素的内存地址：0xc0000b4004 
数组第2个元素的内存地址：0xc0000b4008 
数组第3个元素的内存地址：0xc0000b400c 
```

示例3：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	names := [2]string{"武沛齐", "alex"}
	fmt.Printf("数组的内存地址：%p \n", &names)
	fmt.Printf("数组第1个元素的内存地址：%p \n", &names[0])
	fmt.Printf("数组第2个元素的内存地址：%p \n", &names[1])

}

>>> 输出：
数组的内存地址：0xc000128020 
数组第1个元素的内存地址：0xc000128020 
数组第2个元素的内存地址：0xc000128030
```

#### 5.2 可变和拷贝

可变，数组的元素可以被更改（长度和类型都不可以修改）。

```go
names := [2]string{"武沛齐", "alex"}
names[1] = "苑昊"
```

注意：字符串不可以被修改。 "武沛齐" "武陪齐"

拷贝，变量赋值时重新拷贝一份。

```go
name1 := [2]string{"武沛齐", "alex"}
name2 := name1

name1[1] = "苑昊"

fmt.Println(name1,name2)   // [武沛齐 苑昊]   [武沛齐 alex]
```

#### 5.3 长度索引切片和循环

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	// 1. 长度
	//name := [2]string{"武沛齐", "alex"}
	//fmt.Println(len(name))

	// 2. 索引
	//name := [2]string{"武沛齐", "alex"}
	//data := name[0]
	//fmt.Println(data)
	//name[0] = "eric"
	//fmt.Println(name)

	// 3. 切片
	//nums := [3]int32{11, 22, 33}
	//data := nums[0:2] // 获取   0 <= 下标 < 2
	//fmt.Println(data)

	// 4. 循环
	//nums := [3]int32{11, 22, 33}
	//for i:=0;i<len(nums);i++{
	//	fmt.Println(i, nums[i] )
	//}

	// 5.for range 循环
	nums := [3]int32{11, 22, 33}
	for key, item := range nums {
		fmt.Println(key, item)
	}

	for key := range nums {
		fmt.Println(key)
	}

	for _,item := range nums {
		fmt.Println(item)
	}

}
```

#### 5.4 数组嵌套

```go
// [0,0,0]
//var nestData [3]int

// [ [  [0,0,0],[0,0,0]  ],[  [0,0,0],[0,0,0]  ],[  [0,0,0],[0,0,0]  ], ]
//var nestData [3][2][3]int

// [  [0,0,0],[0,0,0]  ]
//var nestData [2][3]int
//nestData[0] = [3]int{11, 22, 33}
//nestData[1][1] = 666
//fmt.Println(nestData)

//nestData := [2][3]int{[3]int{11, 22, 33}, [3]int{44, 55, 66}}
//fmt.Println(nestData)
```

## 数据类型

Go语言中常见的数据类型有很多，例如：

* 整型，用于表示整数。
* 浮点型，用于表示小数。
* 布尔型，用于表示真/假。
* 字符串，用于表示文本信息。
* 数组，用于表示多个数据（数据集合）
* **指针，用于表示内存地址的类型。**
* **切片，用于表示多个数据（数据集合）**
* **字典，用于表示键值对结合。**
* 结构体，用于自定义一些数据集合。
* 接口，用于约束和泛指数据类型。
* 切片，用于表示多个数据（数据集合），可以理解为动态数组。 \[alex,18,3]
* 字典，键值对。例如：{ "name":"武沛齐"," age":"18", "len":"21" }
* 指针，用于表示内存地址的类型。

### 1. 切片

切片，动态数组。

切片是Go中重要的数据类型，每个切片对象内部都维护着：数组指针、切片长度、切片容量 三个数据。

```go
type slice struct {
	array unsafe.Pointer
	len   int
	cap   int
}
```

在向切片中追加的数据个数大于容量时，内部会自动扩容且每次扩容都当前容量的2倍（当容量超过1024时每次扩容则只增加 1/4容量）。

#### 1.1 创建切片

```go
// 创建切片
var nums []int

// 创建切片
var data = []int{11,22,33}
data:= []int{11,22,33}

// 创建切片
// make只用于 切片、字典、channel
var users = make([]int,1,3)
```

```go
// 切片的指针类型
var v1 = new([]int)

// 指针类型(nil)
var v2 *[]int
```

#### 1.2 自动扩容

```go
v1 := make([]int,1,3)

fmt.Println(len(v1),cap(v1))

// 其他
data := make([]int,3)
```

```go
v1 := make([]int,1,3)

v2 := append(v1,66)

fmt.Println(v1)  // [0 ]
fmt.Println(v2)  // [0,66]

v1[0] = 999
fmt.Println(v1)  // [999 ]
fmt.Println(v2)  // [999,66]

// 需求：有一个切片，请往一个切片中追加一个数据。
v3 := make([]int,1,3)
v3 = append(v3,999)
```

```go
v1 := []int{11,22,33}
v2 := append(v1,44)

v1[0] = 999

fmt.Println(v1) // [999 22 33]
fmt.Println(v2) // [11 22 33 44]
```

#### 1.3 常见操作

**1.3.1 长度和容量**

```go
v1 := []int{11,22,33}
fmt.Println(len(v1), cap(v1))
```

**1.3.2 索引**

```go
v1 := []string{"alex","李杰","老男孩"}
v1[0]
v1[1]
v1[2]

v2 := make([]int,2,5)
v2[0]
v2[1]
v2[2]  // 报错


v2[0] = 999
```

**1.3.3 切片**

```go
v1 := []int{11,22,33,44,55,66}

v2 := v1[1:3]
v3 := v1[1:]
v4 := v1[:3]

// 注意：通过切片切出来的数据和原切片内部存储的数据地址相同
```

**1.3.4 追加**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
)

func main() {
	v1 := []int{11,22,33}

	v2 := append(v1,44)

	v3 := append(v1,55,66,77,88)

	v4 := append(v1, []int{100,200,300}...)

	fmt.Println(v2)
	fmt.Println(v3)
	fmt.Println(v4)
}

>>> 输出
[11 22 33 44]
[11 22 33 55 66 77 88]
[11 22 33 100 200 300]
```

**1.3.5 删除**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	v1 := []int{11, 22, 33, 44, 55, 66}
	deleteIndex := 2

	// 切片获取到 {11,22,44、55、66}
	// 又获取到 {44, 55, 66}，将44、55、66要追加到
	result := append(v1[:deleteIndex], v1[deleteIndex+1:]...)
	fmt.Println(result) // [11 22 44 55 66]
	fmt.Println(v1)     //[11 22 44 55 66 66]
}
```

注意：使用切片时不太会使用删除。【链表】

**1.3.6 插入**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	v1 := []int{11, 22, 33, 44, 55, 66}
	insertIndex := 3 // 在索引3的位置插入99

	result := make([]int, 0, len(v1)+1)
	result = append(result, v1[:insertIndex]...)
	result = append(result,99)
	result = append(result,v1[insertIndex:]...)
	fmt.Println(result)
}

```

注意：效率低下。【链表】

**1.3.7 循环**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	v1 := []int{11, 22, 33, 99, 55, 66}

	for i := 0; i < len(v1); i++ {
		fmt.Println(i, v1[i])
	}

	for index, value := range v1 {
		fmt.Println(index, value)
	}
}
```

#### 1.4 切片嵌套

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	v1 := []int{11, 22, 33, 99, 55, 66}
	v2 := [][]int{[]int{11, 22, 33, 44}, []int{44, 55}}
	v3 := [][2]int{[2]int{1, 2}, [2]int{4, 5}}

	fmt.Println(v1)
	fmt.Println(v2)
	fmt.Println(v3)

	v1[0] = 111111
	v2[0][2] = 222222
	v3[1][0] = 99999

	fmt.Println(v1)
	fmt.Println(v2)
	fmt.Println(v3)
}
```

#### 1.5 变量赋值

*   整型

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := 1
    	v2 := v1

    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc0000b4008
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc0000b4010
    }
    ```
*   布尔类型

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := false
    	v2 := v1

    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc00012a002
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc00012a003
    }
    ```
*   浮点型

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := 3.14
    	v2 := v1

    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc000016050
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc000016058
    }

    ```
*   字符串

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := "武沛齐"
    	v2 := v1

    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc000010200
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc000010210 
    }
    ```

    注意：字符串内部元素不可被修改。
*   数组

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := [2]int{6, 9}
    	v2 := v1
    	fmt.Println(v1, v2)
    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc0000b4010
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc0000b4020

    	v1[0] = 11111
    	fmt.Println(v1, v2)
    }

    ```
*   切片

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import "fmt"

    func main() {
    	v1 := []int{6, 9}
    	v2 := v1
    	fmt.Println(v1, v2)              // [6 9] [6 9]
    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc0000a6020
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc0000a6040

    	v1[0] = 11111
    	fmt.Println(v1, v2) // [11111 9] [11111 9]
    }

    如果扩容，那么内部存储数据的数组就会重新开辟区域。
    ```

    ```go
    package main

    import "fmt"

    func main() {
    	v1 := []int{6, 9}
    	v2 := v1
    	fmt.Println(v1, v2)              // [6 9] [6 9]
    	fmt.Printf("v1的内存地址：%p \n", &v1) // 0xc0000a6020
    	fmt.Printf("v2的内存地址：%p \n", &v2) // 0xc0000a6040

    	v1 = append(v1, 999)
    	fmt.Println(v1, v2) // [11111 9] [11111 9]
    }

    ```

总结，目前所学的所有的数据类型中，在修改切片的内部元素时，会造成所有的赋值的变量同时修改（不扩容）。

扩展：`引用类型和值类型`。

### 2.字典类型（Map）

在学习任何的编程语言时，一般都会一种数据类型称为：字典(dict)或映射(map)，以键值对为元素的数据集合。例如：

```go
{
	"age":"18",
	"name":"武沛齐",
	"email":"wupeiqi@live.com"
}
```

这种类型最大的特点就是查找速度非常快，因为他的底层存储是基于哈希表存储的（不同语言还会有一些差异）。

以`取模+拉链法`来快速了解下哈希表存储原理

这种结构之所以快，是因为根据key可以直接找到数据存放的位置；而其他的数据类型是需要从前到后去逐一比对，相对来说比较耗时。

以上只是基本的存储模型，而各个编程语言中的字典都会在此基础上进行相应的修改和优化（后续会深入讲解Golang中的map实现机制）。

Map的特点：

* 键不能重复
* 键必须可哈希（目前我们已学的数据类型中，可哈希的有：int/bool/float/string/array）
* 无序

接下来关于map我会从两个维度来进行讲解：

* 常见使用
* 底层原理剖析（面试常问）

#### 2.1 声明&初始化

```go
// userInfo := map[string]string{}
userInfo := map[string]string{"name":"武沛齐","age":"18"}

userInfo["name"]  // 武沛齐
userInfo["age"] = "20"
userInfo["email"] = "wupeiqi@live.com"
```

```go
// data := make(map[int]int, 10)
data := make(map[int]int)
data[100] = 998
data[200] = 999
```

```go
data := make(map[string]int)
data["100"] = 998
data["200"] = 999

// 声明，nil
var row map[string]int
row = data
```

```go
data := make(map[string]int)
data["100"] = 998
data["200"] = 999

// 声明，nil
value := new(map[string]int)
// value["k1"] = 123  # 报错
value = &data
```

注意：键不重复 & 键必须可哈希（int/bool/float/string/array）

```go
v1 := make(map[[2]int]float32)
v1[[2]int{1,1}] = 1.6
v1[[2]int{1,2}] = 3.4

v2 := make(map[[2]int][3]string )
v2[[2]int{1,1}] = [3]string{"武沛齐","alex","老妖"}
```

#### 2.2 常用操作

**2.2.1 长度和容量**

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
value := len(data)  // 2
```

```go
// 根据参数值（10），计算出合适的容量。
// 一个map 中会包含很多桶，每个桶中可以存放8个键值对。
info := make(map[string]string, 10)

info["n1"] = "武沛齐"
info["n2"] = "alex"

v1 := len(info)  // 2
// v2 := cap(info)  // 报错
```

**2.2.2 添加**

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
data["n3"] = "eric"
```

**2.2.3 修改**

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
data["n1"] = "eric"
```

**2..2.4 删除**

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
delete(data,"n2")
```

**2.2.5 查看**

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
data["n1"]
```

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
for key,value := range data{
    fmt.Println(key,value)
}
```

```go
data := map[string]string{"n1":"武沛齐","n2":"alex"}
for key := range data{
    fmt.Println(key) 
}
```

```go
data := map[string]string{"n1": "武沛齐", "n2": "alex"}
for _, value := range data {
    fmt.Println(value)
}
```

**2.2.6 嵌套**

```go
v1 := make(map[string]int)
v2 := make(map[string]string)
v3 := make(map[string]...)
v4 := make(map[string][2]int)
v5 := make(map[string][]int)
v6 := make(map[string]map[int]int)
```

```go
v7 := make(map[string][2]map[string]string)
v7["n1"] = [2]map[string]string{ map[string]string{"name":"武沛齐","age":"18"},map[string]string{"name":"alex","age":"78"}}
v7["n2"] = [2]map[string]string{ map[string]string{"name":"eric","age":"18"},map[string]string{"name":"seven","age":"78"}}

// 伪代码
v7 = {
    n1:[
        {"name":"武沛齐","age":"18"},
        {"name":"alex","age":"78"}
    ],
    n2:[
        {"name":"eric","age":"18"},
        {"name":"seven","age":"78"}
    ]
}
```

前提：键不重复 & 键必须可哈希

```go
v8 := make(map[int]int)
v9 := make(map[string]int)
v10 := make(map[float32]int)
v11 := make(map[bool]int)
v12 := make(map[ [2]int ]int)
v13 := make(map[ []int ]int) // 错误,不可哈希
v14 := make(map[ map[int]int ]int) // 错误，不可哈希
v15 := make(map[ [2][]int ]int) // 报错
v16 := make(map[ [2]map[string]string ]int) // 报错
```

**2.2.7 变量赋值**

```go
v1 := map[string]string{"n1":"武沛齐","n2":"alex"}
v2 := v1

v1["n1"] = "wupeiqi"

ftm.Println(v1) // {"n1":"wupeiqi","n2":"alex"}
ftm.Println(v2) // {"n1":"wupeiqi","n2":"alex"}
```

特别提醒：无论是否存在扩容都指向同一个地址。

#### 2.3 Map底层原理剖析

Golang中的Map有自己的一套实现原理，其核心是由`hmap`和`bmap`两个结构体实现。

**2.3.1 初始化**

```go
// 初始化一个可容纳10个元素的map
info = make(map[string]string,10)
```

* 第一步：创建一个hmap结构体对象。
* 第二步：生成一个哈希因子hash0 并赋值到hmap对象中（用于后续为key创建哈希值）。
*   第三步：根据hint=10，并根据算法规则来创建 B，当前B应该为1。

    ```
    hint            B
    0~8				0
    9~13            1
    14~26           2
    ...
    ```
*   第四步：根据B去创建去创建桶（bmap对象）并存放在buckets数组中，当前bmap的数量应为2.

    * 当B<4时，根据B创建桶的个数的规则为：$2^B$（标准桶）
    * 当B>=4时，根据B创建桶的个数的规则为：$2^B$ + $2^{B-4}$（标准桶+溢出桶）

    注意：每个bmap中可以存储8个键值对，当不够存储时需要使用溢出桶，并将当前bmap中的overflow字段指向溢出桶的位置。

**2.3.2 写入数据**

```go
info["name"] = "武沛齐"
```

在map中写入数据时，内部的执行流程为：

* 第一步：结合哈希因子和键 `name`生成哈希值 `011011100011111110111011011`。
*   第二步：获取哈希值的`后B位`，并根据后B为的值来决定将此键值对存放到那个桶中（bmap）。

    ```
    将哈希值和桶掩码（B个为1的二进制）进行 & 运算，最终得到哈希值的后B位的值。假设当B为1时，其结果为 0 ：
    哈希值：011011100011111110111011010
    桶掩码：000000000000000000000000001
    结果：  000000000000000000000000000 = 0

    通过示例你会发现，找桶的原则实际上是根据后B为的位运算计算出 索引位置，然后再去buckets数组中根据索引找到目标桶（bmap)。
    ```
*   第三步：在上一步确定桶之后，接下来就在桶中写入数据。

    ```
    获取哈希值的tophash（即：哈希值的`高8位`），将tophash、key、value分别写入到桶中的三个数组中。
    如果桶已满，则通过overflow找到溢出桶，并在溢出桶中继续写入。

    注意：以后在桶中查找数据时，会基于tophash来找（tophash相同则再去比较key）。
    ```
* 第四步：hmap的个数count++（map中的元素个数+1）

**2.3.3 读取数据**

```go
value := info["name"]
```

在map中读取数据时，内部的执行流程为：

* 第一步：结合哈希引子和键 `name`生成哈希值。
* 第二步：获取哈希值的`后B位`，并根据后B为的值来决定将此键值对存放到那个桶中（bmap）。
*   第三步：确定桶之后，再根据key的哈希值计算出tophash（高8位），根据tophash和key去桶中查找数据。

    ```
    当前桶如果没找到，则根据overflow再去溢出桶中找，均未找到则表示key不存在。
    ```

**2.3.4 扩容**

在向map中添加数据时，当达到某个条件，则会引发字典扩容。

扩容条件：

* map中数据总个数 / 桶个数 > 6.5 ，引发翻倍扩容。
* 使用了太多的溢出桶时（溢出桶使用的太多会导致map处理速度降低）。
  * B <=15，已使用的溢出桶个数 >= $2^B$ 时，引发等量扩容。
  * B > 15，已使用的溢出桶个数 >= $2^{15}$ 时，引发等量扩容。

```go
func hashGrow(t *maptype, h *hmap) {
	// If we've hit the load factor, get bigger.
	// Otherwise, there are too many overflow buckets,
	// so keep the same number of buckets and "grow" laterally.
	bigger := uint8(1)
	if !overLoadFactor(h.count+1, h.B) {
		bigger = 0
		h.flags |= sameSizeGrow
	}
	oldbuckets := h.buckets
	newbuckets, nextOverflow := makeBucketArray(t, h.B+bigger, nil)
	...
}
```

当扩容之后：

* 第一步：B会根据扩容后新桶的个数进行增加（翻倍扩容新B=旧B+1，等量扩容 新B=旧B）。
* 第二步：oldbuckets指向原来的桶（旧桶）。
* 第三步：buckets指向新创建的桶（新桶中暂时还没有数据）。
* 第四步：nevacuate设置为0，表示如果数据迁移的话，应该从原桶（旧桶）中的第0个位置开始迁移。
* 第五步：noverflow设置为0，扩容后新桶中已使用的溢出桶为0。
* 第六步：extra.oldoverflow设置为原桶（旧桶）已使用的所有溢出桶。即：`h.extra.oldoverflow = h.extra.overflow`
* 第七步：extra.overflow设置为nil，因为新桶中还未使用溢出桶。
* 第八步：extra.nextOverflow设置为新创建的桶中的第一个溢出桶的位置。

**2.3.5 迁移**

扩容之后，必然要伴随着数据的迁移，即：将旧桶中的数据要迁移到新桶中。

**翻倍扩容**

如果是翻倍扩容，那么迁移规就是将旧桶中的数据分流至新的两个桶中（比例不定），并且桶编号的位置为：同编号位置 和 翻倍后对应编号位置。

那么问题来了，如何实现的这种迁移呢？

首先，我们要知道如果翻倍扩容（数据总个数 / 桶个数 > 6.5），则新桶个数是旧桶的2倍，即：map中的B的值要+1（因为桶的个数等于$2^B$，而翻倍之后新桶的个数就是$2^B$ \* 2 ，也就是$2^{B+1}$，所以 `新桶的B的值=原桶B + 1` ）。

迁移时会遍历某个旧桶中所有的key（包括溢出桶），并根据key重新生成哈希值，根据哈希值的 `底B位` 来决定将此键值对分流道那个新桶中。

扩容后，B的值在原来的基础上已加1，也就意味着通过多1位来计算此键值对要分流到新桶位置，如上图：

* 当新增的位（红色）的值为 0，则数据会迁移到与旧桶编号一致的位置。
* 当新增的位（红色）的值为 1，则数据会迁移到翻倍后对应编号位置。

例如：

```
旧桶个数为32个，翻倍后新桶的个数为64。
在重新计算旧桶中的所有key哈希值时，红色位只能是0或1，所以桶中的所有数据的后B位只能是以下两种情况：
	- 000111【7】，意味着要迁移到与旧桶编号一致的位置。
	- 100111【39】，意味着会迁移到翻倍后对应编号位置。
	
特别提醒：同一个桶中key的哈希值的低B位一定是相同的，不然不会放在同一个桶中，所以同一个桶中黄色标记的位都是相同的。
```

**等量扩容**

如果是等量扩容（溢出桶太多引发的扩容），那么数据迁移机制就会比较简单，就是将旧桶（含溢出桶）中的值迁移到新桶中。

这种扩容和迁移的意义在于：当溢出桶比较多而每个桶中的数据又不多时，可以通过等量扩容和迁移让数据更紧凑，从而减少溢出桶。

### 3.指针

指针，是一种数据类型，用于表示数据的内存地址。

```go
// 声明一个 字符串类型 的变量（默认初始化值为空字符串）。
var v1 string

// 声明一个 字符串的指针类型 的变量（默认初始化值为nil）。
var v2 *string 

var v3 int

var v4 *int
```

```go
// 声明一个 字符串类型 的变量，值为 武沛齐。
var name string = "武沛齐"

// 声明一个 字符串的指针类型 的变量，值为 name 对应的内存地址。
var pointer *string = &name

var age int = 18
var x1 *int = &age
```

#### 3.1 指针的意义

相当于创建了一个地址的`引用`，以后根据这个引用再去获取他里面的值。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	v1 := "武沛齐"
	v2 := &v1
	fmt.Println(v1, v2, *v2) // 武沛齐 0xc00008e1e0 武沛齐
  
  v1 = "alex"
  fmt.Println(v1, v2, *v2) // alex 0xc00008e1e0 alex
}

```

#### 3.2 指针的应用场景

场景1：

```go
v1 := "武沛齐"
v2 := v1
v1 = "alex"

fmt.Println(v1,v2) // alex 武沛齐
```

```go
v1 := "武沛齐"
v2 := &v1
v1 = "alex"
fmt.Println(v1,*v2) // alex  alex
```

场景2：

```go
package main

import "fmt"

func changeData(data string) {
	data = "哈哈哈哈哈"
}

func main() {
	name := "武沛齐"
  // 本质上会将name的值拷贝一份，并赋值给data
	changeData(name)
  fmt.Println(name) // 武沛齐
}
```

```go
package main

import "fmt"

func changeData(ptr *string) {
	*ptr = "哈哈哈哈哈"
}

func main() {
	name := "武沛齐"
	changeData(&name)
  fmt.Println(name) // 哈哈哈哈哈
}
```

场景3：

```go
package main

import "fmt"

func main() {
	var username string
	fmt.Printf("请输入用户名：")
	
  // 提示用户输入，当用户输入之后，将输入的值赋值给内存地址对应的区域中。
	fmt.Scanf("%s", &username)

	if username == "武沛齐" {
		fmt.Println("登录成功")
	} else {
		fmt.Println("登录失败")
	}
}
```

#### 3.3 指针的指针

```go
name := "武沛齐"

// 声明一个指针类型变量p1，内部存储name的内存地址
var p1 *string = &name

// 声明一个指针的指针类型变量p2，内部存储指针p1的内存地址
var p2 **string = &p1

// 声明一个指针的指针的指针类型变量p3，内部存储指针p2的内存地址
var p3 ***string = &p2
```

因为有指针的指针存在，所以在使用指针进行重置值时，也需要将相应的\*号设置好，例如：

```go
package main

import "fmt"

func main() {
   name := "武沛齐"

   // 声明一个指针类型变量p1，内部存储name的内存地址
   var p1 *string = &name
  
   *p1 = "张三" // 将name的内存中的值由 武沛齐 改为 张三

   // 声明一个指针的指针类型变量p2，内部存储指针p1的内存地址
   var p2 **string = &p1
   **p2 = "啦啦啦" // 将name的内存中的值由 张三 改为 啦啦啦

   var p3 ***string = &p2
   ***p3 = "我靠" // 将name的内存中的值由 啦啦啦 改为 我靠
}
```

#### 3.4 指针小高级操作

*   数组的地址 == 数组的第一个元素的地址。

    ```go
    dataList := [3]int8{11, 22, 33}

    fmt.Printf("数组的地址：%p；数组第一个元素的地址：%p \n", &dataList, &dataList[0])
    // &dataList 和 &dataList[0] 的内存中存储的数据虽然相同，但他们是两个不同类型的指针。
    // &dataList 是 *[3]int8 类型
    // &dataList[0] 是 *int8 类型
    ```
*   指针的计算

    ```go
    /*
     @Author:武沛齐  微信号：wupeiqi666
     @Description: 老男孩IT教育 & 路飞学城
     @Video:  https://space.bilibili.com/283478842
    */
    package main

    import (
    	"fmt"
    	"unsafe"
    )

    func main() {

    	dataList := [3]int8{11, 22, 33}

    	// 1.获取数组第一个元素的地址（指针）
    	var firstDataPtr *int8 = &dataList[0]

    	// 2.转换成Pointer类型
    	ptr := unsafe.Pointer(firstDataPtr)

    	// 3.转换成uintptr类型，然后进行内存地址的计算（即：地址加1个字节，意味着取第2个索引位置的值）。
    	targetAddress := uintptr(ptr) + 1

    	// 4.根据新地址，重新转换成Pointer类型
    	newPtr := unsafe.Pointer(targetAddress)

    	// 5.Pointer对象转换为 int8 指针类型
    	value := (*int8)(newPtr)

    	// 6.根据指针获取值
    	fmt.Println("最终结果为：", *value)
    }

    ```

## 结构体和接口

Go语言中常见的数据类型有很多，例如：

* 整型，用于表示整数。
* 浮点型，用于表示小数。
* 布尔型，用于表示真/假。
* 字符串，用于表示文本信息。
* 数组，用于表示多个数据（数据集合）
* 指针，用于表示内存地址的类型。
* 切片，用于表示多个数据（数据集合）
* 字典，用于表示键值对结合。
* **结构体，用于自定义一些数据集合。**
* **接口，用于约束和泛指数据类型。**
* 结构体，用于自定义一些数据集合。
* 接口，用于约束和泛指数据类型。

### 1.结构体

什么是结构体？

> 结构体是一个复合类型，用于表示一组数据。
>
> 结构体由一系列属性组成，每个属性都有自己的类型和值。

```go
// 定义
type Person struct {
    name  string
    age   int
    email string
}

// 初始化
var p1 = Person{"武沛齐", 19, "wupeiqi@live.com"}

// 结构体中取值
fmt.Println(p1.name, p1.age, p1.email)

p1.age = 20

fmt.Println(p1.name, p1.age, p1.email)
```

```go
type 结构体名称 struct {
    字段 类型
    ...
}
```

#### 1.1 定义

```go
type Person struct {
    name  string
    age   int
    hobby []string
}
```

```go
type Address struct {  
    city,state string
    age int
}
```

```go
type Address struct {  
    city,state string
}

type Person struct {  
    name string
    age int
    ad Address
}
```

```go
type Address struct {
    city, state string
}

type Person struct {
    name    string
    age     int
	Address // 匿名字段 Address Address
}
```

#### 1.2 初始化

或称根据结构体创建一个对象。

```go
// 定义一个结构体（类型），每个结构体包含 name、age、hobby 三个元素
type Person struct {
    name  string
    age   int
    hobby []string
}

//方式1：先后顺序
var p1 = Person{"武沛齐", 19, []string{"篮球", "足球"}}
fmt.Println(p1.name, p1.age, p1.hobby)

//方式2：关键字
var p2 = Person{name: "武沛齐", age: 19, hobby: []string{"饺子", "嫂子"}}
fmt.Println(p2.name, p2.age, p2.hobby)

//方式3：先声明再赋值
var p3 Person
p3.name = "武沛齐"
p3.age = 18
p3.hobby = []string{"女人", "篮球"}
fmt.Println(p3.name, p3.age, p3.hobby)

```

```go
type Address struct {  
    city,state string
    age int
}
// 同上
```

```go
type Address struct {  
    city,state string
}
type Person struct {  
    name string
    age int
    address Address
}

//方式1：先后顺序
var p1 = Person{"武沛齐", 19, Address{"北京", "中国"}}
fmt.Println(p1.name, p1.age, p1.address.city, p1.address.state)

//方式2：关键字
var p1 = Person{name: "武沛齐",age: 19, address: Address{city: "北京", state: "中国"}}
fmt.Println(p1.name, p1.age, p1.address.city, p1.address.state)

//方式3：先声明再赋值
var p3 Person
p3.name = "武沛齐"
p3.age = 50
p3.address = Address{
    city:  "北京",
    state: "BJ",
}
fmt.Println(p3.name, p3.age, p3.address.city, p3.address.state)

```

```go
// 定义一个结构体（类型），每个结构体包含 name、age、hobby 三个元素
type Address struct {
    city, state string
}
type Person struct {
    name    string
    age     int
    Address // 匿名字段，那么默认Person就包含了Address的所有字段
}

//方式1：先后顺序
p1 := Person{"武沛齐", 19, Address{"北京", "中国"}}
fmt.Println(p1.name, p1.age, p1.city, p1.state)


//方式2：关键字
p2 := Person{name: "武沛齐", age: 19, Address: Address{city: "北京", state: "中国"}}
fmt.Println(p2.name, p2.age, p2.city, p2.state,p2.Address.city, p2.Address.state)

//方式3：先声明再赋值
var p3 Person
p3.name = "武沛齐"
p3.age = 50
p3.Address = Address{
    city:  "北京",
    state: "BJ",
}
fmt.Println(p3.name, p3.age, p3.address.city, p3.address.state)
// 或
var p4 Person
p4.name = "武沛齐"
p4.age = 50
p4.city = "北京"
p4.state = "BJ"
fmt.Println(p3.name, p3.age, p3.Address.city, p3.Address.state)
```

#### 1.3 结构体指针

**1.3.1 创建**

```go
type Person struct {
    name  string
    age   int
}

// 初始化结构体（创建一个结构体对象）
p1 := Person{"武沛齐", 18}
fmt.Println(p1.name, p1.age)

// 初始化结构体指针
// var p2 *Person = &Person{"武沛齐", 18}
p2 := &Person{"武沛齐", 18}
fmt.Println(p2.name, p2.age)

var p3 *Person = new(Person)
p3.name = "武沛齐"
p3.age = 18

fmt.Println(p3.name, p3.age)
```

**1.3.2 内存管理**

```go
type Person struct {
    name  string
    age   int
}

// 初始化结构体
p1 := Person{"武沛齐", 18}
fmt.Println(p1.name, p1.age)

// 初始化结构体指针
p2 := &Person{"武沛齐", 1}
fmt.Println(p2.name, p2.age)
```

#### 1. 赋值

**1.4.1 赋值拷贝**

```go
type Person struct {
    name string
    age  int
}

p1 := Person{name: "武沛齐", age: 18}
p2 := p1 // 内部将p1重新拷贝一份

fmt.Println(p1) // {武沛齐 18}
fmt.Println(p2) // {武沛齐 18}

p1.name = "alex"

fmt.Println(p1) // {alex 19}
fmt.Println(p2) // {武沛齐 19}
```

**1.4.2 结构体指针赋值**

```go
type Person struct {
    name string
    age  int
}

p1 := &Person{"武沛齐", 18}
p2 := p1

fmt.Println(p1) // &{武沛齐 18}
fmt.Println(p2) // &{武沛齐 18}
p1.name = "alex"
fmt.Println(p1) // &{alex 18}
fmt.Println(p2) // &{alex 18}
```

基于结合结构体和结构体指针的特性，基于指针实现数据变化后同步遍布。

```go
type Person struct {
    name string
    age  int
}

p1 := Person{name: "二狗子", age: 19}
p2 := &p1

fmt.Println(p1) // {二狗子 19}
fmt.Println(p2) // &{二狗子 19}

p1.name = "alex"

fmt.Println(p1) // {alex 19}
fmt.Println(p2) // &{alex 19}
```

**1.4.3 嵌套赋值拷贝**

在存在结构体嵌套时，赋值会拷贝一份所有的数据。

```go
type Address struct {
	city, state string
}

type Person struct {
	name    string
	age     int
	address Address
}

p1 := Person{name:"二狗子",age:19,address: Address{"北京", "BJ"}}
p2 := p1

fmt.Println(p1.address) // {"北京" "BJ"}
fmt.Println(p2.address) // {"北京" "BJ"}

p1.address.city = "上海"

fmt.Println(p1.address) // {"上海" "BJ"}
fmt.Println(p2.address) // {"北京" "BJ"}
```

**1.4.4 谁不拷贝？**

其实本质上都拷贝了，只不过由于数据存储方式的不同，导致拷贝的有些是数据，有些是内存地址（指针）。

* 感觉拷贝：字符串、数组、整型等。
* 感觉不拷贝：map、切片。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {

	type Person struct {
		name    string
		age     int
		hobby   [2]string
		num     []int
		parent  map[string]string
	}

	p1 := Person{
		name:   "二狗子",
		age:    19,
		hobby:  [2]string{"裸奔", "大保健"}, // 拷贝
		num:    []int{69, 19, 99, 38}, // 未拷贝 (内部维护指针指向数据存储的地方)
		parent: map[string]string{"father": "Alex", "mother": "Monika"}, // 未拷贝 (内部维护指针指向数据存储的地方)
	}
	p2 := p1

	fmt.Println(p1)
	fmt.Println(p2)
	p1.parent["father"] = "武沛齐"
	fmt.Println(p1)
	fmt.Println(p2)
}
```

注意：对于那些默认拷贝的情况，可以改变为指针类型，让数据实现同步修改。

```go
type Address struct {
    city, state string
}
type Person struct {
    name    string
    age     int
    hobby   *[2]string
    num     []int
    parent  map[string]string
    address Address
}

p1 := Person{
    name:   "二狗子",
    age:    19,
    hobby:  &[2]string{"裸奔", "大保健"},
    num:    []int{69, 19, 99, 38},
    parent: map[string]string{"father": "Alex", "mother": "Monika"},
}
p2 := p1
p1.hobby[0] = "洗澡"

fmt.Println(p1.hobby) // &[洗澡 大保健]
fmt.Println(p2.hobby) // &[洗澡 大保健]
```

#### 1.5 结构体标签

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"reflect"
)

func main() {
	type Person struct {
		name string "姓名"
		age  int32  "年龄"
		blog string "博客"
	}

	p1 := Person{name: "武沛齐", age: 18, blog: "https://www.pythonav.com"}

	p1Type := reflect.TypeOf(p1)
    
	// 方式1
	filed1 := p1Type.Field(0)
	fmt.Println(filed1.Tag) // 姓名   filed1.Name -> name

	// 方式2
	filed2, _ := p1Type.FieldByName("blog")
	fmt.Println(filed2.Tag) // 

	// 循环获取
	fieldNum := p1Type.NumField() // 总共有多少个字段 3
    // 循环：0 1 2 
	for index := 0; index < fieldNum; index++ {
		field := p1Type.Field(index)
		fmt.Println(field.Name, field.Tag) //    name  姓名;    age 年龄  ;   blog 博客
	}
}
```

### 2.函数

可以把函数当做一个代码块，用于实现某个功能。并且提高代码的重用性和可读性。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

// 定义函数
func SendEmail()  {
	fmt.Println("发送邮件了...")
}

func main() {
	// 1000行 or 10000行
	// ...
	// 执行函数
	SendEmail()
	// ...
	// 10行代码可以实现发邮件
}
```

```go
func 函数名(参数) 返回值 {
    函数体
}
```

```go
package main

import "fmt"

func SendEmail(email string) bool {
   fmt.Println(email, "你有新邮件来了")
   return true
}

func main() {
   result := SendEmail("wupeiqi@qq.com")
   if result {
      fmt.Println("发送成功")
   } else {
      fmt.Println("发送失败")
   }
}
```

关于函数名需要注意：函数名只能是字母数字下划线组合且数字不能开头（驼峰式命名 `SendEmail` `sendEmail`）。

#### 2.1 参数

**2.1.1 多个参数**

```go
package main

import "fmt"

func add(num1 int, num2 int) (int, bool) {
   result := num2 + num1
   return result, true
}

func main() {
   data, flag := add(1, 8)
   fmt.Println(data, flag)
}

>>> 输出：
9 true
```

注意：传值时会拷贝一份数据（等同于赋值拷贝）。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func SendEmail(arg [2]int)  {
	arg[0] = 666
}

func main() {
	dataList := [2]int{11,22}
	SendEmail(dataList)
	fmt.Println(dataList) // [11,22]
}
```

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func SendEmail(arg *[2]int)  {
	arg[0] = 666
}

func main() {
	dataList := [2]int{11,22}
	SendEmail(&dataList)
	fmt.Println(dataList) // [666,22]
}

```

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func SendEmail(arg []int)  {
	arg[0] = 666
}

func main() {
	dataList := []int{11,22}
	SendEmail(dataList)
	fmt.Println(dataList) // [666,22]
}
```

**2.1.2 指针参数**

```go
package main

import "fmt"

func changeData(dataList *[3]string) {
	dataList[1] = "李杰"
}

func main() {
	userList := [3]string{"武沛齐", "Alex", "老妖"}
	changeData(&userList)

	fmt.Println(userList)
}

>>> 输出：
[武沛齐 李杰 老妖]
```

数组是值类型，参数传递时会重新拷贝一份，为了避免拷贝可以使用指针类型做参数。

**2.1.3 函数做参数**

```go
package main

import "fmt"

func add100(arg int) (int,bool) {
	return arg + 100, true
}

func proxy(data int, exec func(int) (int, bool)) int {
	data, flag := exec(data)
	if flag {
		return data
	} else {
		return 9999
	}
}

func main() {
	result := proxy(123, add100)
	fmt.Println(result) // 223

}
```

```go
package main

import "fmt"

func add100(arg int) (int, bool) {
   return arg + 100, true
}

type f1 func(arg int) (int, bool)

func proxy(data int, exec f1) int {
   data, flag := exec(data)
   if flag {
      return data
   } else {
      return 9999
   }
}

func main() {
   result := proxy(123, add100)
   fmt.Println(result)

}
```

**2.1.4 变长参数**

```go
package main

import "fmt"

func do(num ...int) int {
   sum := 0
   for _, value := range num {
      sum += value
   }
   return sum
}

func main() {
   r1 := do(1, 2, 3, 3)
   r2 := do(0, 1, 1)
   fmt.Println(result)
}
```

注意事项：边长参数只能放在最后且只能有一个。

#### 2.2 返回值

**2.2.1 多个返回值**

```go
package main

import "fmt"

func add100(arg int) (int, bool, int) {
   return arg + 100, true, 888
}

func main() {
   v1, v2, v3 := add100(555)
   fmt.Println(v1, v2, v3)
}
```

**2.2.1 返回函数**

```go
package main

import (
	"fmt"
)

func exec(num1 int, num2 int) string {
	fmt.Println("执行函数了")
	return "成功"
}

type f1 func(int, int) string

func getFunction() f1 {
	return exec
}

func main() {
	function := getFunction()
	result := function(111, 222)
	fmt.Println(result)
}

```

**2.2.2 匿名函数&返回函数**

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func F1(n1 int, n2 int) func(int) string {

	return func(n1 int) string {
		fmt.Println("匿名函数")
		return "匿名"
	}
}

func main() {
	// 匿名函数
	v1 := func(n1 int, n2 int) int {
		return 123
	}
	data := v1(11, 22)
	fmt.Println(data)

	value := func(n1 int, n2 int) int {
		return 123
	}(11, 22)
	fmt.Println(value)

}
```

```go
package main

import "fmt"

func proxy() func() int {
	v1 := func() int {
		return 100
	}
	return v1
}

func main() {
	function := proxy()
	result := function()
	fmt.Println(result)
}
```

#### 2.3 闭包

学函数，少不了闭包。下面用两个示例了解闭包的作用。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	var functionList []func()

	for i := 0; i < 5; i++ {
		function := func() {
			fmt.Println(i)
		}
		functionList = append(functionList, function)
	}

	functionList[0]()
	functionList[1]()
	functionList[2]()
}

```

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

func main() {
	// 存储着5个函数
	var functionList []func()

	for i := 0; i < 5; i++ {
		function := func(arg int) func() {
			return func() {
				fmt.Println(arg)
			}
		}(i)
		functionList = append(functionList, function)
	}

	// 运行函数
	functionList[0]()
	functionList[1]()
	functionList[2]()
}
```

#### 2.4 defer

用于在一个函数执行完成之后自动触发的语句，一般用于结束操作之后释放资源。

示例1：

```go
package main

import "fmt"

func do() int {
	fmt.Println("风吹")
	defer fmt.Println("函数执行完毕了")  // 如果在这行之前执行return，那么defer就不再执行
	fmt.Println("屁屁凉")
	return 666
}

func main() {
	ret := do()
	fmt.Println(ret)
}

```

注意：在函数return之后/执行结束之前自动调用defer语句。

示例2：

```go
package main

import "fmt"

func do() int {
   fmt.Println("风吹")
   defer fmt.Println("函数执行完毕了")
   defer fmt.Println("再来一个")
   fmt.Println("屁屁凉")
   return 666
}

func main() {
   ret := do()
   fmt.Println(ret)
}
```

当存在多个defer时，最终函数执行完毕后会按照倒序的方式去执行。

示例3：

```go
package main

import "fmt"

func other(a1 int, a2 int) {
   fmt.Println("defer函数被执行了")
}

func do() int {
   fmt.Println("风吹")
   defer fmt.Println("函数执行完毕了")
   defer other(1, 22)
   fmt.Println("屁屁凉")
   return 666
}

func main() {
   ret := do()
   fmt.Println(ret)
}
```

#### 2.5 自执行函数

```go
result := func(arg int) int {
    return arg + 100
}(123)

fmt.Println(result) // 223
```

### 3.再看结构体

#### 3.1 结构体做参数和返回值

结构体做参数和返回值时，在执行时候都会被重新拷贝一份，如果不想被拷贝，则可以通过指针的形式进行处理。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

type Person struct {
	name string
	age  int
}

var P Person = Person{"wupeiqi", 18}

func doSomething() Person {
	return P
}

func main() {
	data := doSomething()
	P.name = "alex"
    fmt.Println(data) // {wupeiqi 18}
	fmt.Println(P)    // {alex 18}
}

```

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Description: 老男孩IT教育 & 路飞学城
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

type Person struct {
	name string
	age  int
}

var P Person = Person{"wupeiqi", 18}

func doSomething() *Person {
	return &P
}

func main() {
	data := doSomething()
	P.name = "alex"
	fmt.Println(data) // &{alex 18}
	fmt.Println(P)    // {alex 18}
}
```

#### 3.2 类型方法

项目开发中可以为type声明的类型编写一些方法，从而实现`对象.方法`的操作。

```go
package main

import "fmt"

// 声明类型
type MyInt int

// 为MyInt类型自定义一个指针方法
// 可以是指针/可以是类型：*MyInt   MyInt
// 不使用对象，可以用 _ 代替
func (_ *MyInt) DoSomething(a1 int, a2 int) int {
	return a1 + a2
}

func do(a1 int,a2 int) int{
    return a1 + a2
}

func main() {
	var v1 MyInt = 1
	result := v1.DoSomething(1, 2)
	fmt.Println(result)
}
```

结构体也是基于type声明的类型，所以也可以使用此方式为结构体定义一些方法。

```go
package main

import "fmt"

type Person struct {
	name string
	age  int
	blog string
}

// 为Person结构体类型自定义一个指针方法
// 注意：此处如果不是指针类型的话，再执行方法时结构体对象就会被重复拷贝一份。
func (p *Person) DoSomething(a1 int, a2 int) int {
	return a1 + a2 + p.age
}

func main() {
	p1 := Person{name: "武沛齐", age: 18, blog: "https://www.pythonav.com"}
	// 调用Person的DoSomething方法
	result := p1.DoSomething(1, 2)
	fmt.Println(result)
}
```

注意：在方法名之前，`func` 关键字之后的括号中指定 receiver。如果方法不需要使用 `recv` 的值，可以用 **\_** 替换它。`recv` 就像是面向对象语言中的 `this` 或 `self`，但是 Go 中并没有这两个关键字。随个人喜好，你可以使用 `this` 或 `self` 作为 receiver 的名字。

#### 3.3 方法继承

如果结构体之前存在`匿名`嵌套关系，则 `子结构体`可以继承`父结构体`中的方法。

```go
package main

import "fmt"

type Base struct {
   name string
}
type Son struct {
   Base    // 匿名的方式，如果改成 base Base 则无法继承Base的方法。
   age int
}

// Base结构体的方法
func (b *Base) m1() int {
   return 666
}

// Son结构体的方法
func (s *Son) m2() int {
   return 999
}

func main() {
    son := Son{age: 18, Base: Base{name: "武沛齐"}}
	result1 := son.m1()
	result2 := son.m2()
	fmt.Println(result1, result2)
}
```

如果Son结构体中还有与其他结构体嵌套，那么他可以继承所有嵌套结构体中的方法。

#### 3.4 结构体工厂

Go 语言不支持面向对象编程语言中那样的构造方法，但是可以很容易的在 Go 中实现 “构造工厂”方法。为了方便通常会为类型定义一个工厂，按惯例，工厂的名字以 new 或 New 开头。假设定义了如下的 File 结构体类型：

```go
type File struct {
    fd      int     
    name    string  
}

// 20...
f := File{10, "xxxxxx"}
```

```go
type File struct {
    fd      int     
    name    string  
}

func NewFile(fd int, name string) *File {
	// 20...
    return &File{fd, name}
}

func main() {
	f1 := NewFile(10, "./test.txt")
    f2 := File{10, "xxxxxx"}
}
```

在 Go 语言中常常像上面这样在工厂方法里使用初始化来简便的实现构造函数。

**强制使用工厂方法**，让结构体变为私有，工厂方法变为共有，这样强制所有代码在实例化结构体是都是用工厂方法。

可以l用包导入时首字母大写共有的方式来实现。

```go
// 私有
type matrix struct {
    ...
}

// 共有
func NewMatrix(params) *matrix {
    m := new(matrix) // 初始化 m
    return m
}
```

```
package main
import "matrix"
...
// wrong := new(matrix.matrix)     // 编译失败（matrix 是私有的）
right := matrix.NewMatrix(...)  // 实例化 matrix 的唯一方式
```

### 4.接口

Go语言中的接口是一种特殊的数据类型，定义格式如下：

```go
type 接口名称 interface{
    方法名称() 返回值
}
```

例如：

```go
type Base interface {
	f1()                   // 定义方法，无返回值
	f2() int               // 定义方法，返回值int类型
	f3() (int, bool)       // 定义方法，2个返回值分别是 int、bool类型
	f4(n1 int, n2 int) int // 定义方法，需要两个参数，1个返回值
}

type empty interface {}  // interface{} 
```

接口中的方法只定义，不能编写具体的实现逻辑。

#### 4.1 接口的作用

在程序开发中接口一般有两大作用：代指类型 & 约束。

**4.1.1 空接口，代指任意类型**

示例1：

```go
package main

import (
	"fmt"
	"reflect"
)

// 定义空接口
type Base interface {
	
}

func main() {
    //定义一个切片，内部可以存放任意类型。
	dataList := make([]Base, 0)  // 推荐简写为：dataList := make([]interface{}, 0)
    
    // 切片中添加 字符串类型
	dataList = append(dataList, "武沛齐")
	// 切片中添加 整型
	dataList = append(dataList, 18)
    // 切片中添加 浮点型
	dataList = append(dataList, 99.99)
}
```

示例2：

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Video:  https://space.bilibili.com/283478842
*/
package main

import (
	"fmt"
	"reflect"
)

type Person struct {
	name string
	age  int
}

func something(arg interface{}) {
	fmt.Println(arg)
}

func main() {
	something("武沛齐")
	something(666)
	something(4.15)
	something(Person{name: "wupeiqi", age: 18})
}
```

由于接口只是代指这些数据类型（在内部其实是转换为了接口类型），想要再获取数据中的值时，需要再将接口转换为指定的数据类型。

```go
/*
 @Author:武沛齐  微信号：wupeiqi666
 @Video:  https://space.bilibili.com/283478842
*/
package main

import "fmt"

type Person struct {
	name string
	age  int
}

func something(arg interface{}) {
	// 接口转换为Person成功，ok=True；否则ok=True
	tp, ok := arg.(Person)
	if ok {
		fmt.Println(tp.name, tp.age)
	} else {
		fmt.Println("转换失败")
	}
}

func main() {
	something(Person{name: "wupeiqi", age: 18})
    something("武沛齐")
}
```

```go
package main

import (
	"fmt"
)

type Person struct {
	name string
	age  int
}

type Role struct {
	title string
	count int
}

func something(arg interface{}) {

	// 多个类型转换，将arg接口对象转换为。（断言）
	switch tp := arg.(type) {
	case Person:
		fmt.Println(tp.name)
	case Role:
		fmt.Println(tp.title)
	case string:
		fmt.Println(tp)
	default:
		fmt.Println(tp)
	}
}

func main() {
	something("武沛齐")
	something(666)
	something(4.15)
	something(Person{name: "wupeiqi", age: 18})
	something(Role{title: "管理员", count: 2})
}
```

**4.1.2 非空接口，规范&约束**

一般定义非空接口，都是用于约束结构体中必须含有某个方法，例如：

示例1：

```go
package main

import "fmt"

// 定义接口
type IBase interface {
	f1() int
}

// 定义结构体Person
type Person struct {
	name string
}

// 为结构体Person定义方法
func (p Person) f1() int {
	return 123
}

// 定义结构体User
type User struct {
	name string
}

// 为结构体User定义方法
func (p User) f1() int {
	return 666
}

// 基于接口的参数，可以实现传入多中类型（多态），也同时具有约束对象必须实现接口方法的功能
func DoSomething(base IBase) {
    result := base.f1() //直接调用  接口.f1()  -> 找到其对应的类型并执行其方法
	fmt.Println(result)
}

func main() {

	per := Person{name: "武沛齐"}
	user := User{name: "wupeiqi"}

	DoSomething(per)
	DoSomething(user)
}
```

示例2：

```go
package main

import "fmt"

// 定义接口
type IBase interface {
   f1() int
}

// 定义结构体
type Person struct {
   name string
}

// 为结构体定义方法
func (p *Person) f1() int {
   return 123
}

// 定义结构体
type User struct {
   name string
}

// 为结构体定义方法
func (p *User) f1() int {
   return 666
}

// 基于接口的参数，可以实现传入多中类型（多态），也同时具有约束对象必须实现接口方法的功能
func DoSomething(base IBase) {
   result := base.f1() // 由于base的约束，此处智能执行IBase中约束的接口。
   fmt.Println(result)
}

func main() {

   per := &Person{name: "武沛齐"} // 创建结构体对象并获取其指针对象
   user := &User{name: "wupeiqi"}

   DoSomething(per)
   DoSomething(user)
}
```

#### 4.2 底层实现

**4.2.1 空接口**

接口是Go的一种数据类型，在上文也已经了解到Go的空接口可以代指任意类型，从而实现参数、”容器“中可以处理多种数据类型。

Go语言底层对空接口的实现：

```go
type eface struct {
   _type *_type			// 存储类型相关信息
   data  unsafe.Pointer // 存储数据
}
```

如果在代码中出现`其他对象`赋值给空接口，其实就是将其他对象相关的值存放到eface的 `_type`和`data`中，内部源码：

```go
// The conv and assert functions below do very similar things.
// The convXXX functions are guaranteed by the compiler to succeed.
// The assertXXX functions may fail (either panicking or returning false,
// depending on whether they are 1-result or 2-result).
// The convXXX functions succeed on a nil input, whereas the assertXXX
// functions fail on a nil input.

func convT2E(t *_type, elem unsafe.Pointer) (e eface) {
   if raceenabled {
      raceReadObjectPC(t, elem, getcallerpc(), funcPC(convT2E))
   }
   if msanenabled {
      msanread(elem, t.size)
   }
   x := mallocgc(t.size, t, true)
   // TODO: We allocate a zeroed object only to overwrite it with actual data.
   // Figure out how to avoid zeroing. Also below in convT2Eslice, convT2I, convT2Islice.
   typedmemmove(t, x, elem)
   e._type = t
   e.data = x
   return
}
```

注意：`_type`是一个结构体内部存储挺多的信息，这里统称为类型相关的信息。

示例1：

```go
package main

func main() {
	num := 666
	var object interface{}
	// 将num的类型int存储到 _type 中；值8存储到data中
	object = num
}
```

示例2：

```go
package main

func DoSomething(arg interface{}) {
   // 将 num的类型int 存储到 _type 中；值8存储到data中;
}

func main() {
   num := 666
   DoSomething(num)
}
```

示例3：

```go
package main

type Person struct {
   name string
   age  int
}

func DoSomething(arg interface{}) {
   // 将 info的类型Person 存储到 _type 中；值{name: "武沛齐", age: 18}存储到data中;
}

func main() {
   info := Person{name: "武沛齐", age: 18}
   DoSomething(info)
}
```

**4.2.2 非空接口**

非空接口会定义一些方法来实现约束，所以在底层实现和空接口有些不同。

```go
type iface struct {
   tab  *itab           // 类型和方法相关
   data unsafe.Pointer  // 数据
}

type itab struct {
	inter *interfacetype // 接口信息，如：接口中定义的方法。
	_type *_type         // 类型
	hash  uint32
	_     [4]byte
	fun   [1]uintptr
}

type interfacetype struct {
	typ     _type
	pkgpath name
	mhdr    []imethod   // 接口的方法
}
```

### 总结

Go语言中常见的数据类型有很多，例如：

* 整型，用于表示整数。
* 浮点型，用于表示小数。
* 布尔型，用于表示真/假。
* 字符串，用于表示文本信息。
* 数组，用于表示多个数据（数据集合）
* 指针，用于表示内存地址的类型。
* 切片，用于表示多个数据（数据集合）
* 字典，用于表示键值对结合。
* 结构体，用于自定义一些数据集合。
* 接口，用于约束和泛指数据类型。

除此之外，还学习 函数，以及为结构体定义方法。
