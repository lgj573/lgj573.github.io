---
layout: post
title: npm install 错误2
category: 前端
tags: [ionic , npm]
description: npm install 碰到的问题2
---

# 尝试和选择

```
gyp ERR! configure error
gyp ERR! stack Error: Command failed: C:\Python27\python.EXE -c import sys; print "%s.%s.%s" % sys.version_info[:3];
gyp ERR! stack
gyp ERR! stack     at ChildProcess.exithandler (child_process.js:294:12)
gyp ERR! stack     at ChildProcess.emit (events.js:198:13)
gyp ERR! stack     at maybeClose (internal/child_process.js:982:16)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:259:5)
gyp ERR! System Windows_NT 10.0.18362
gyp ERR! command "C:\\Program Files\\nodejs\\node.exe" "F:\\ionic\\final\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebuild" "--verbose" "--libsass_ext=" "--libsass_cflags=" "--libsass_ldflags=" "--libsass_library="
gyp ERR! cwd F:\ionic\final\node_modules\@ionic\app-scripts\node_modules\node-sass
gyp ERR! node -v v10.19.0
gyp ERR! node-gyp -v v3.8.0
gyp ERR! not ok
```
重新安装python
```
MSBUILD : error MSB3428: 未能加载 Visual C++ 组件“VCBuild.exe”。要解决此问题，1) 安装 .NET Framework 2.0 SDK；2) 安装 Microsoft Visual Studio 2005；或 3) 如果将该组件安装到了其他位置，请将其位置添加到系统路径中。 [F:\ionic\final\node_modules\@ionic\app-scripts\node_modules\node-sass\build\binding.sln]
已完成生成项目“F:\ionic\final\node_modules\@ionic\app-scripts\node_modules\node-sass\build\binding.sln”(默认目标)的操作 - 失败。
```

运行 npm install --global --production windows-build-tools ，npm install -g node-gyp，要用以管理员身份运行

 