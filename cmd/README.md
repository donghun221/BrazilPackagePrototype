# `/cmd`

Go服务main入口。<br><br>一个Go项目中可以有多个main.go，此时，在cmd目录下，可创建多个子目录，代表具体子项目，例如，`/cmd/myapp`。名称要与启动的项目名称一致，例如，`cmd/cache_service`。<br><br> 不要在cmd目录下设置过多的代码，如果代码段，及.go文件为内部不可重用，并且非开源，则放到`/internal`目录中。如果.go文件可以被其他工程复用，则放到/pkg目录中。

Examples:

* https://github.com/heptio/ark/tree/master/cmd (just a really small `main` function with everything else in packages)
* https://github.com/moby/moby/tree/master/cmd
* https://github.com/prometheus/prometheus/tree/master/cmd
* https://github.com/influxdata/influxdb/tree/master/cmd
* https://github.com/kubernetes/kubernetes/tree/master/cmd

