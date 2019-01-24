# 标准GO语言【Brazil】工程包布局
这是标准【Brazil】GO语言工程包布局，并非GO官方的宣布的布局格式，出自于流行GO项目的布局格式。

## BrazilPakcage 目录

| 目录名称 | 介绍 |
|--|--|
| `/api` | PorotoBuf, JSON Schema, OpenAPI/Swagger Specs 文件。 |
| `/assets` | 其他Assets，如图片，Logo。 |
| `/build` | 用于打包&持续集成。<br><br>存放Cloud(AMI), 容器(Docker)等相关文件。<br><br>存放CI相关的配置&脚本文件。例如`/build/ci/jenkins/build.jenkins` |
| `/cmd` | Go服务main入口。<br><br>一个Go项目中可以有多个main.go，此时，在cmd目录下，可创建多个子目录，代表具体子项目，例如，`/cmd/myapp`。名称要与启动的项目名称一致，例如，`cmd/cache_service`。<br><br> 不要在cmd目录下设置过多的代码，如果代码段，及.go文件为内部不可重用，并且非开源，则放到`/internal`目录中。如果.go文件可以被其他工程复用，则放到/pkg目录中。|
| `/configs` | 存放Config文件。<br><br>BrazilPackage 会默认创建`/service/service/service.toml`， `/service/app/myapp.toml` 两种不同的Config类型，如果需要创建自己的Config类型，可以创建`/service/private/myconfig.xxx`类型的文件。|
| `/deployments` | 存放持续部署相关的配置&脚本文件，如spinnaker/kubernetes配置文件。 |
| `/docs` | 设计，部署等文档。 |
| `/examples` | 存放事例。 |
| `/githooks` | 存放Git Hooks相关文件。 |
| `/init` | 系统初始化需要的参数/脚本文件。 |
| `/internal` | 存放私有Lib代码，即，不想其他项目调用的代码段。<br><br> 应用程序的代码放在`/internal/app/myapp`中，可复用的代码放到`/internal/pkg/myprivlib`中。|
| `/pkg` | 公用Lib，例如，calc_digest这种功能代码段。 |
| `/scripts` | 对于不同平台的Build，分析，安装等操作的脚本。 |
| `/test` | ⚠️ 这里【不是】存放测试文件<br><br> 存放测试需要的文件，如，JSON 入参文件等。|
| `/third_party` | 存放第三方Lib。 |
| `/tools` | 工具类，如，debug_tools.go。 |
| `/vendor` | 项目的依赖包，可用dep或者module倒入依赖。 |
| `/web` | Web应用目录，如静态类文件，服务端模版等。 |
| `/website` | 存放Web相关的文件。 |

> ⚠️ 在 GO 项目中不要使用 Java 类型的 /src 布局。
> 
> Some Go projects do have a  `src`  folder, but it usually happens when the devs came from the Java world where it's a common pattern. If you can help yourself try not to adopt this Java pattern. You really don't want your Go code or Go projects to look like Java :-)
>
> Don't confuse the project level  `/src`  directory with the  `/src`  directory Go uses for its workspaces as described in  [`How to Write Go Code`](https://golang.org/doc/code.html). The  `$GOPATH`  environment variable points to your (current) workspace (by default it points to  `$HOME/go`  on non-windows systems). This workspace includes the top level  `/pkg`,  `/bin`  and  `/src`  directories. Your actual project ends up being a sub-directory under  `/src`, so if you have the  `/src`  directory in your project the project path will look like this:  `/some/path/to/workspace/src/your_project/src/your_code.go`. Note that with Go 1.11 it's possible to have your project outside of your  `GOPATH`, but it still doesn't mean it's a good idea to use this layout pattern.