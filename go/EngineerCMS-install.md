# EengineerCMS 环境配置

需要安装的 package 如下：
```
go get -v github.com/astaxie/beego
go get -v github.com/beego/bee
go get -v github.com/3xxx/engineercms
go get -v github.com/beego/admin/src/lib
go get -v github.com/casbin/beego-orm-adapter
go get -v github.com/casbin/casbin
go get -v github.com/Knetic\govaluate
go get -v github.com/lib/pq
go get -v github.com/mattn/go-sqlite3
go get -v github.com/pborman/uuid
go get -v github.com/pkg/errors
go get -v github.com/tealeg/xlsx
go get -v golang.org/x/crypto
go get -v gopkg.in/yaml.v2
```
由于这些包之间存在一些依赖关系，如果顺利，安装`engineercms`时即可把剩下的包都装上。若遇到网络错误，可以手动下载这些包到相应目录，然后进入那个目录，执行`go install`。

以下展示了安装`engineercms`的所涉及的依赖关系。
```
lxx@DESKTOP-MIL81G4 MINGW64 /e/Lxx/workspace_go/src/github.com
$ go get -u -v github.com/3xxx/engineercms
github.com/3xxx/engineercms (download)
github.com/astaxie/beego (download)
github.com/beego/admin (download)
github.com/mattn/go-sqlite3 (download)
Fetching https://gopkg.in/yaml.v2?go-get=1
Parsing meta tags from https://gopkg.in/yaml.v2?go-get=1 (status code 200)
get "gopkg.in/yaml.v2": found meta tag get.metaImport{Prefix:"gopkg.in/yaml.v2", VCS:"git", RepoRoot:"https://gopkg.in/yaml.v2"} at https://gopkg.in/yaml.v2?go-get=1
gopkg.in/yaml.v2 (download)
Fetching https://golang.org/x/crypto/acme/autocert?go-get=1
https fetch failed: Get https://golang.org/x/crypto/acme/autocert?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
golang.org/x/crypto (download)
Fetching https://golang.org/x/crypto/acme?go-get=1
https fetch failed: Get https://golang.org/x/crypto/acme?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
github.com/casbin/beego-orm-adapter (download)
github.com/casbin/casbin (download)
github.com/lib/pq (download)
github.com/Knetic/govaluate (download)
github.com/pkg/errors (download)
github.com/pborman/uuid (download)
github.com/tealeg/xlsx (download)
github.com/astaxie/beego/validation
github.com/mattn/go-sqlite3
github.com/astaxie/beego/utils/pagination
github.com/astaxie/beego/httplib
github.com/pborman/uuid
github.com/tealeg/xlsx
github.com/3xxx/engineercms/models
github.com/3xxx/engineercms/controllers
github.com/3xxx/engineercms/routers
github.com/3xxx/engineercms
```

可能遇到的问题
````
C:\Users\lxx>go get -v github.com/astaxie/beego
Fetching https://golang.org/x/crypto/acme/autocert?go-get=1
https fetch failed: Get https://golang.org/x/crypto/acme/autocert?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/crypto/acme/autocert: unrecognized import path "golang.org/x/crypto/acme/autocert" (https fetch: Get https://golang.org/x/crypto/acme/autocert?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
````

解决方案：
```
mkdir $GOPATH/src/golang.org/x
cd $GOPATH/src/golang.org/x
git clone git@github.com:golang/crypto.git
go install crypto
```
