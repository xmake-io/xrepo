<div align="center">
  <a href="https://xmake.io">
    <img width="160" heigth="160" src="https://tboox.org/static/img/xmake/logo256c.png">
  </a>

  <h1>xrepo</h1>

  <div>
    <a href="https://www.reddit.com/r/xmake/">
      <img src="https://img.shields.io/badge/chat-on%20reddit-ff3f34.svg?style=flat-square" alt="Reddit" />
    </a>
    <a href="https://gitter.im/xmake-io/xmake?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge">
      <img src="https://img.shields.io/gitter/room/xmake-io/xmake.svg?style=flat-square&colorB=96c312" alt="Gitter" />
    </a>
    <a href="https://t.me/tbooxorg">
      <img src="https://img.shields.io/badge/chat-on%20telegram-blue.svg?style=flat-square" alt="Telegram" />
    </a>
    <a href="https://jq.qq.com/?_wv=1027&k=5hpwWFv">
      <img src="https://img.shields.io/badge/chat-on%20QQ-ff69b4.svg?style=flat-square" alt="QQ" />
    </a>
    <a href="https://github.com/xmake-io/xrepo/blob/master/LICENSE.md">
      <img src="https://img.shields.io/github/license/xmake-io/xrepo.svg?colorB=f48041&style=flat-square" alt="license" />
    </a>
    <a href="https://xmake.io/#/about/sponsor">
      <img src="https://img.shields.io/badge/donate-us-orange.svg?style=flat-square" alt="Donate" />
    </a>
  </div>

  <p>一个基于 Xmake 的跨平台 C/C++ 包管理器</p>
</div>

## 项目支持

通过成为赞助者来支持该项目。您的logo将显示在此处，并带有指向您网站的链接。🙏 [[成为赞助商](https://xmake.io/#/zh-cn/about/sponsor)]

<a href="https://opencollective.com/xmake#backers" target="_blank"><img src="https://opencollective.com/xmake/backers.svg?width=890"></a>

## 简介

xrepo 是一个基于 [Xmake](https://github.com/xmake-io/xmake) 的跨平台 C/C++ 包管理器。

它基于 xmake 提供的运行时，但却是一个完整独立的包管理程序，相比 vcpkg/homebrew 此类包管理器，xrepo 能够同时提供更多平台和架构的 C/C++ 包。

并且还支持多版本语义选择，另外它还是一个去中心化的分布式仓库，不仅仅提供了官方的 [xmake-repo](https://github.com/xmake-io/xmake-repo) 仓库，还支持用户自建多个私有仓库。

同时，xrepo 也支持从 vcpkg/homebrew/conan 等第三方包管理器中安装包，并提供统一一致的库链接信息，方便与第三方项目的集成对接。

如果你想要了解更多，请参考：[在线文档](https://xrepo.xmake.io/#/zh-cn/getting_started), [Github](https://github.com/xmake-io/xrepo) 以及 [Gitee](https://gitee.com/tboox/xrepo)

![](https://xrepo.xmake.io/assets/img/xrepo.gif)

## 安装

我们只需要安装上 xmake 就可以使用 xrepo 命令，关于 xmake 的安装，我们可以看下：[xmake 安装文档](https://xmake.io/#/zh-cn/guide/installation)。

## 支持平台

* Windows (x86, x64)
* macOS (i386, x86_64, arm64)
* Linux (i386, x86_64, cross-toolchains ..)
* *BSD (i386, x86_64)
* Android (x86, x86_64, armeabi, armeabi-v7a, arm64-v8a)
* iOS (armv7, armv7s, arm64, i386, x86_64)
* MSYS (i386, x86_64)
* MinGW (i386, x86_64, arm, arm64)
* Cross Toolchains

## 支持的包管理仓库

* 官方自建仓库 [xmake-repo](https://github.com/xmake-io/xmake-repo) (tbox >1.6.1)
* [用户自建仓库](https://xmake.io/#/zh-cn/package/remote_package?id=%e4%bd%bf%e7%94%a8%e8%87%aa%e5%bb%ba%e7%a7%81%e6%9c%89%e5%8c%85%e4%bb%93%e5%ba%93)
* Conan (conan::openssl/1.1.1g)
* Vcpkg (vcpkg:ffmpeg)
* Homebrew/Linuxbrew (brew::pcre2/libpcre2-8)
* Pacman on archlinux/msys2 (pacman::libcurl)
* Clib (clib::clibs/bytes@0.0.4)
* Dub (dub::log 0.4.3)

## 分布式仓库支持

除了可以直接从官方仓库：[xmake-repo](https://github.com/xmake-io/xmake-repo) 检索安装包之外，
我们还可以添加任意多个自建的仓库，甚至可以完全隔离外网，仅仅在公司内部网络维护私有包的安装集成。

只需要通过下面的命令，添加上自己的仓库地址：

```console
$ xrepo add-repo myrepo https://github.com/mygroup/myrepo
```

## 与 xmake 的工程无缝集成

```lua
add_requires("tbox >1.6.1", "libuv master", "vcpkg::ffmpeg", "brew::pcre2/libpcre2-8")
add_requires("conan::openssl/1.1.1g", {alias = "openssl", optional = true, debug = true})
target("test")
    set_kind("binary")
    add_files("src/*.c")
    add_packages("tbox", "libuv", "vcpkg::ffmpeg", "brew::pcre2/libpcre2-8", "openssl")
```

下面是与 xmake 集成的整体架构和编译流程。

<img src="https://xmake.io/assets/img/index/package_arch.png" width="650px" />

## 快速上手

### 安装包

#### 基本使用

```console
$ xrepo install zlib tbox
```

#### 安装指定版本包

完整支持 Semantic Versioning (语义版本)。

```console
$ xrepo install "zlib 1.2.x"
$ xrepo install "zlib >=1.2.0"
```

#### 安装指定平台包

```console
$ xrepo install -p iphoneos -a arm64 zlib
$ xrepo install -p android [--ndk=/xxx] zlib
$ xrepo install -p mingw [--mingw=/xxx] zlib
$ xrepo install -p cross --sdk=/xxx/arm-linux-musleabi-cross zlib
```

#### 安装调试版本包

```console
$ xrepo install -m debug zlib
```

#### 安装动态库版本包

```console
$ xrepo install -k shared zlib
```

#### 安装指定配置包

```console
$ xrepo install -f "vs_runtime=MD" zlib
$ xrepo install -f "regex=true,thread=true" boost
```

#### 安装第三方包管理器的包

```console
$ xrepo install brew::zlib
$ xrepo install vcpkg::zlib
$ xrepo install conan::zlib/1.2.11
$ xrepo install pacman:libpng
$ xrepo install dub:log
```

### 查找包的库使用信息

```console
$ xrepo fetch pcre2
{
  {
    linkdirs = {
      "/usr/local/Cellar/pcre2/10.33/lib"
    },
    links = {
      "pcre2-8"
    },
    defines = {
      "PCRE2_CODE_UNIT_WIDTH=8"
    },
    includedirs = "/usr/local/Cellar/pcre2/10.33/include"
  }
}
```

```console
$ xrepo fetch --ldflags openssl
-L/Users/ruki/.xmake/packages/o/openssl/1.1.1/d639b7d6e3244216b403b39df5101abf/lib -lcrypto -lssl
```

```console
$ xrepo fetch --cflags openssl
-I/Users/ruki/.xmake/packages/o/openssl/1.1.1/d639b7d6e3244216b403b39df5101abf/include
```

```console
$ xrepo fetch -p [iphoneos|android] --cflags "zlib 1.2.x"
-I/Users/ruki/.xmake/packages/z/zlib/1.2.11/df72d410e7e14391b1a4375d868a240c/include
```

```console
$ xrepo fetch --cflags --ldflags conan::zlib/1.2.11
-I/Users/ruki/.conan/data/zlib/1.2.11/_/_/package/f74366f76f700cc6e991285892ad7a23c30e6d47/include -L/Users/ruki/.conan/data/zlib/1.2.11/_/_/package/f74366f76f700cc6e991285892ad7a23c30e6d47/lib -lz
```

### 导出安装后的包

xrepo 可以快速导出已经安装后的包，包括对应的库文件，头文件等等。

```console
$ xrepo export -o /tmp/output zlib
```

### 搜索支持的包

```console
$ xrepo search zlib "pcr*"
    zlib:
      -> zlib: A Massively Spiffy Yet Delicately Unobtrusive Compression Library (in xmake-repo)
    pcr*:
      -> pcre2: A Perl Compatible Regular Expressions Library (in xmake-repo)
      -> pcre: A Perl Compatible Regular Expressions Library (in xmake-repo)
```

### 查看包环境信息

```console
$ xrepo env --show luajit
{
  OLDPWD = "/mnt/tbox",
  HOME = "/home/ruki",
  PATH = "/home/ruki/.xmake/packages/l/luajit/2.1.0-beta3/fbac76d823b844f0b91abf3df0a3bc61/bin:/tmp:/tmp/arm-linux-musleabi-cross/bin:~/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
  TERM = "xterm",
  PWD = "/mnt/xmake",
  XMAKE_PROGRAM_DIR = "/mnt/xmake/xmake",
  HOSTNAME = "e6edd61ff1ab",
  LD_LIBRARY_PATH = "/home/ruki/.xmake/packages/l/luajit/2.1.0-beta3/fbac76d823b844f0b91abf3df0a3bc61/lib",
  SHLVL = "1",
  _ = "/mnt/xmake/scripts/xrepo.sh"
}
```

### 加载执行包环境并运行命令

```console
$ xrepo env luajit
LuaJIT 2.1.0-beta3 -- Copyright (C) 2005-2017 Mike Pall. http://luajit.org/
JIT: ON SSE2 SSE3 SSE4.1 BMI2 fold cse dce fwd dse narrow loop abc sink fuse
>
```

```console
$ xrepo env -b "luajit 2.x" luajit
$ xrepo env -p iphoneos -b "zlib,libpng,luajit 2.x" cmake ..
```

### 进入包 shell 环境

我们可以通过在当前目录下，添加 xmake.lua 文件，定制化一些包配置，然后进入特定的包 shell 环境。

```lua
add_requires("zlib 1.2.11")
add_requires("python 3.x", "luajit")
```

```console
$ xrepo env shell
> python --version
> luajit --version
```

### 查看包信息

```console
$ xrepo info zlib
The package info of project:
    require(zlib):
      -> description: A Massively Spiffy Yet Delicately Unobtrusive Compression Library
      -> version: 1.2.11
      -> urls:
         -> http://zlib.net/zlib-1.2.11.tar.gz
            -> c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1
         -> https://downloads.sourceforge.net/project/libpng/zlib/1.2.11/zlib-1.2.11.tar.gz
            -> c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1
      -> repo: xmake-repo https://gitee.com/tboox/xmake-repo.git master
      -> cachedir: /Users/ruki/.xmake/cache/packages/2010/z/zlib/1.2.11
      -> installdir: /Users/ruki/.xmake/packages/z/zlib/1.2.11/d639b7d6e3244216b403b39df5101abf
      -> searchdirs:
      -> searchnames: zlib-1.2.11.tar.gz
      -> fetchinfo: 1.2.11, system
          -> version: 1.2.11
          -> links: z
          -> linkdirs: /usr/local/Cellar/zlib/1.2.11/lib
          -> includedirs: /usr/local/Cellar/zlib/1.2.11/include
      -> platforms: iphoneos, mingw@windows, macosx, mingw@linux,macosx, android@linux,macosx, windows, linux
      -> requires:
         -> plat: macosx
         -> arch: x86_64
         -> configs:
            -> debug: false
            -> vs_runtime: MT
            -> shared: false
      -> configs:
      -> configs (builtin):
         -> debug: Enable debug symbols. (default: false)
         -> shared: Enable shared library. (default: false)
         -> cflags: Set the C compiler flags.
         -> cxflags: Set the C/C++ compiler flags.
         -> cxxflags: Set the C++ compiler flags.
         -> asflags: Set the assembler flags.
         -> vs_runtime: Set vs compiler runtime. (default: MT)
            -> values: {"MT","MD"}
```

### 卸载所有的包

我们可以通过下面的命令，批量卸载删除已经安装的包，支持模式匹配：

```bash
$ xrepo remove --all
$ xrepo remove --all zlib pcr*
```

## 联系方式

* 邮箱：[waruqi@gmail.com](mailto:waruqi@gmail.com)
* 主页：[xmake.io](https://xmake.io/#/zh-cn/)
* 社区：[Reddit论坛](https://www.reddit.com/r/xmake/)
* 聊天：[Telegram群组](https://t.me/tbooxorg), [Gitter聊天室](https://gitter.im/xmake-io/xmake?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
* 源码：[Github](https://github.com/xmake-io/xmake), [Gitee](https://gitee.com/tboox/xmake)
* QQ群：343118190(技术支持), 662147501
* 微信公众号：tboox-os

