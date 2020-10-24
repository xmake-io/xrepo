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

xRepo 是一个基于 [Xmake](https://github.com/xmake-io/xmake) 的跨平台 C/C++ 包管理器。

如果你想要了解更多，请参考：[在线文档](https://xmake.io/#/zh-cn/getting_started), [Github](https://github.com/xmake-io/xrepo) 以及 [Gitee](https://gitee.com/tboox/xrepo)

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

## 快速上手

### 安装包

#### 基本使用

```console
$ xrepo install zlib tbox
```

#### 安装指定版本包

```console
$ xrepo install "zlib 1.2.x"
$ xrepo install "zlib >= 1.2.0"
```

#### 安装指定平台包

```console
$ xrepo install -p iphoneos -a arm64 zlib
$ xrepo install -p android [--ndk=/xxx] zlib
$ xrepo install -p mingw [--mingw=/xxx] zlib
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
$ xrepo install --configs="vs_runtime=MD" zlib
$ xrepo install --configs="regex=true,thread=true" boost
```

#### 安装第三方包管理器的包

```console
$ xrepo install brew::zlib
$ xrepo install vcpkg::zlib
$ xrepo install conan::zlib/1.2.11
$ xrepo install clib::zlib
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
$ xrepo fetch -p [iphoneos|android] --cflags zlib
-I/Users/ruki/.xmake/packages/z/zlib/1.2.11/df72d410e7e14391b1a4375d868a240c/include
```

## 联系方式

* 邮箱：[waruqi@gmail.com](mailto:waruqi@gmail.com)
* 主页：[xmake.io](https://xmake.io/#/zh-cn/)
* 社区：[Reddit论坛](https://www.reddit.com/r/xmake/)
* 聊天：[Telegram群组](https://t.me/tbooxorg), [Gitter聊天室](https://gitter.im/xmake-io/xmake?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
* 源码：[Github](https://github.com/xmake-io/xmake), [Gitee](https://gitee.com/tboox/xmake)
* QQ群：343118190(技术支持), 662147501
* 微信公众号：tboox-os

