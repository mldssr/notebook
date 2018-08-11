# Go 环境配置

## 基本安装

## VSCode
直接安装微软的 Go 插件，不过还需要其他工具，如下图，会在你打开某个Go代码时自动提示。

```
Installing 10 tools at E:\Lxx\workspace_go\bin
  gocode
  gopkgs
  go-outline
  go-symbols
  guru
  gorename
  dlv
  godef
  goreturns
  golint
```

结果失败了6个：
```
Installing github.com/mdempsky/gocode SUCCEEDED
Installing github.com/uudashr/gopkgs/cmd/gopkgs SUCCEEDED
Installing github.com/ramya-rao-a/go-outline FAILED
Installing github.com/acroca/go-symbols FAILED
Installing golang.org/x/tools/cmd/guru FAILED
Installing golang.org/x/tools/cmd/gorename FAILED
Installing github.com/derekparker/delve/cmd/dlv SUCCEEDED
Installing github.com/rogpeppe/godef SUCCEEDED
Installing github.com/sqs/goreturns FAILED
Installing github.com/golang/lint/golint FAILED

6 tools failed to install.

go-outline:
Error: Command failed: D:\Go\bin\go.exe get -u -v github.com/ramya-rao-a/go-outline
github.com/ramya-rao-a/go-outline (download)
Fetching https://golang.org/x/tools/go/buildutil?go-get=1
https fetch failed: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/go/buildutil: unrecognized import path "golang.org/x/tools/go/buildutil" (https fetch: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
github.com/ramya-rao-a/go-outline (download)
Fetching https://golang.org/x/tools/go/buildutil?go-get=1
https fetch failed: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/go/buildutil: unrecognized import path "golang.org/x/tools/go/buildutil" (https fetch: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)

go-symbols:
Error: Command failed: D:\Go\bin\go.exe get -u -v github.com/acroca/go-symbols
github.com/acroca/go-symbols (download)
Fetching https://golang.org/x/tools/go/buildutil?go-get=1
https fetch failed: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/go/buildutil: unrecognized import path "golang.org/x/tools/go/buildutil" (https fetch: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
github.com/acroca/go-symbols (download)
Fetching https://golang.org/x/tools/go/buildutil?go-get=1
https fetch failed: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/go/buildutil: unrecognized import path "golang.org/x/tools/go/buildutil" (https fetch: Get https://golang.org/x/tools/go/buildutil?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)

guru:
Error: Command failed: D:\Go\bin\go.exe get -u -v golang.org/x/tools/cmd/guru
Fetching https://golang.org/x/tools/cmd/guru?go-get=1
https fetch failed: Get https://golang.org/x/tools/cmd/guru?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/cmd/guru: unrecognized import path "golang.org/x/tools/cmd/guru" (https fetch: Get https://golang.org/x/tools/cmd/guru?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
Fetching https://golang.org/x/tools/cmd/guru?go-get=1
https fetch failed: Get https://golang.org/x/tools/cmd/guru?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/cmd/guru: unrecognized import path "golang.org/x/tools/cmd/guru" (https fetch: Get https://golang.org/x/tools/cmd/guru?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)

gorename:
Error: Command failed: D:\Go\bin\go.exe get -u -v golang.org/x/tools/cmd/gorename
Fetching https://golang.org/x/tools/cmd/gorename?go-get=1
https fetch failed: Get https://golang.org/x/tools/cmd/gorename?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/cmd/gorename: unrecognized import path "golang.org/x/tools/cmd/gorename" (https fetch: Get https://golang.org/x/tools/cmd/gorename?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
Fetching https://golang.org/x/tools/cmd/gorename?go-get=1
https fetch failed: Get https://golang.org/x/tools/cmd/gorename?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/cmd/gorename: unrecognized import path "golang.org/x/tools/cmd/gorename" (https fetch: Get https://golang.org/x/tools/cmd/gorename?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)

goreturns:
Error: Command failed: D:\Go\bin\go.exe get -u -v github.com/sqs/goreturns
github.com/sqs/goreturns (download)
Fetching https://golang.org/x/tools/imports?go-get=1
https fetch failed: Get https://golang.org/x/tools/imports?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/imports: unrecognized import path "golang.org/x/tools/imports" (https fetch: Get https://golang.org/x/tools/imports?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
github.com/sqs/goreturns (download)
Fetching https://golang.org/x/tools/imports?go-get=1
https fetch failed: Get https://golang.org/x/tools/imports?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/tools/imports: unrecognized import path "golang.org/x/tools/imports" (https fetch: Get https://golang.org/x/tools/imports?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)

golint:
Error: Command failed: D:\Go\bin\go.exe get -u -v github.com/golang/lint/golint
github.com/golang/lint (download)
Fetching https://golang.org/x/lint?go-get=1
https fetch failed: Get https://golang.org/x/lint?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/lint: unrecognized import path "golang.org/x/lint" (https fetch: Get https://golang.org/x/lint?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
github.com/golang/lint (download)
Fetching https://golang.org/x/lint?go-get=1
https fetch failed: Get https://golang.org/x/lint?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.
package golang.org/x/lint: unrecognized import path "golang.org/x/lint" (https fetch: Get https://golang.org/x/lint?go-get=1: dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.)
```

仔细看一看，发现是因为无法获取 https://golang.org/x/tools 和 https://golang.org/x/lint ，也就是 https://golang.org/x/ 连不上。好在其在 github 有镜像 `https://github.com/golang/`，例如，上述两个镜像地址分别为 `https://github.com/golang/tools.git` 和 `https://github.com/golang/lint.git`。在 `$GOPATH/src/golang.org/x/` 下 `git clone` 相应的库，然后再安装即可成功。再安装时去掉 `-u` 选项会快一点，例如 `go get -v github.com/ramya-rao-a/go-outline`，不然会强制更新包和依赖包，依然需要连接 `golang.org`，然后超时失败，不过因为源码已经 `git clone` 下来了，连接失败后依然会继续剩下的安装过程，最终结果一样，只不过多了个超时的过程，会慢一点。


## 使用代理加速
`go get` 下载github的包时，采用的是 `http` 协议，可能会比较慢，可以使用代理加速这一过程，使 `go` 的自动安装依赖可以进行下去，省去好多事情。  
代理分为 Win 命令行、Linux 终端和 Git 代理，本身已有 `shadowsocks` 监听在 `127.0.0.1:1080`，我在 Windows 下试了命令行 socks5 代理，不好使，也尝试过用 `cow` 把 `socks5` 转成 `http` 代理，再为 Win 命令行 或 Git 设置 http 代理，也不好使。最后发现还是直接设置 Git socks5 代理好使。

```
# Win 命令行 SOCKS5 代理
set http_proxy=socks5://127.0.0.1:1080
set https_proxy=socks5://127.0.0.1:1080

# Win 命令行取消 SOCKS5 代理
set http_proxy=
set https_proxy=

# Git SOCKS5 代理
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080

# Git 取消 SOCKS5 代理
git config --global --unset http.proxy
git config --global --unset https.proxy

# 只对github.com
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080

# 取消代理
git config --global --unset http.https://github.com.proxy
```