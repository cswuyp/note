一、windows下安装golang开发环境  
（1）配置GOROOT变量，在系统变量中点击新建，变量值是golang安装文件夹目录  
（2）配置Path变量，选中Path点编辑即可，在变量值后面追加;%GOROOT%\bin    
（3）配置GOPATH变量，系统变量中点击新建，变量值是你的golang工作目录  
golang工作目录（gowork）下创建三个文件夹，分别为：  
src存放源代码的目录，新建项目都在该目录下。  
pkg编译过后生成的包文件存放目录。  
bin编译后生产的可执行文件  

二、Visual Studio Code中安装go插件  
Visual Studio Code是一款非常强大的开发工具。在Visual Studio Code上配置GoLang开发环境，会使得开发更加便捷。  
我们打开Visual Studio Code,打开GoLang项目所在文件夹，这时候Visual Studio Code会提示我们要安装插件，如果  
我们点击install会执行指令 go get -u golang.org/x下载对应插件，因为有墙所以在这里直接点击install是无法下  
载成功的了，我们需要到github上下载对应的包，我们需要以管理员的身份打开cmd，然后把golang.org/x换成  
github.com/x  集成安装命令，拷贝到cmd窗口就可完成安装：    
```
go get -u -v github.com/nsf/gocode
go get -u -v github.com/rogpeppe/godef
go get -u -v github.com/golang/lint/golint
go get -u -v github.com/lukehoban/go-find-references
go get -u -v github.com/lukehoban/go-outline
go get -u -v sourcegraph.com/sqs/goreturns
go get -u -v golang.org/x/tools/cmd/gorename
go get -u -v github.com/tpng/gopkgs
go get -u -v github.com/newhook/go-symbols
go get -u -v github.com/ramya-rao-a/go-outline
```
这款插件的特性包括：
Colorization 代码着彩色  
Completion Lists 代码自动完成（使用gocode）  
Snippets  代码片段  
Quick Info 快速提示信息（使用godef）  
Goto Definition 跳转到定义（使用godef）  
Find References  搜索参考引用（使用go-find-references）  
File outline 文件大纲（使用go-outline）  
Workspace symbol search 工作区符号搜索（使用 go-symbols）  
Rename 重命名（使用gorename）  
Build-on-save 保存构建（使用go build和go test）  
Format 代码格式化（使用goreturns或goimports或gofmt）  
Add Imports  添加引用（使用 gopkgs）  
Debugging 调试代码（使用delve）  
以上都下载成功后，我们打开%GOPATH%\src\bin目录会发现有一些已经安装了，有一些还未安装，我们需要把未安装的插件都安装了  
切换到GOPATH目录下，执行相关的go install 命令，  
假如%GOPATH%\src\bin目录下没有go-outline.exe则 执行指令 go install github.com/ramya-rao-a/go-outline  

安装完vscode的插件后我们还需要安装Go编程语言的各种包和工具的源代码  
进行如下命令进行目录切换：  
cd %GOPATH%\src\github.com\golang  
我这里的GOPATH是在D:\gowork  
如果src目录下面没有github.com\golang请自行创建  
完成目录切换后，开始下载插件包：  
git clone https://github.com/golang/tools.git tools  
当下载完成后，你会发现%GOPATH%\src\github.com\golang多了一个tools目录  
需要把tools目录下的所有文件拷贝到%GOPATH%\src\golang.org\x\tools下，如果没有自行创建  
当然如果你是windows环境，如果你当前是在%GOPATH%\src\golang.org\x\tools  
目录下，你可以直接使用如下命令进行拷贝：  
xcopy /s /e %GOPATH%\src\github.com\golang\tools

下载golang单元测试插件：    
go get -u github.com/cweill/gotests  
gotests使编写Go测试变得容易。它是一个Golang命令行工具，可以根据目标源文件的函数和方法签名生成表驱动的测试。  
将自动导入测试文件中的任何新依赖项  

以上搞定后就可以进行开发了，开发中需要需要用到新的库打开cmd窗口执行指令 go -u gitbuh.com/xx/xx就可完成安装
