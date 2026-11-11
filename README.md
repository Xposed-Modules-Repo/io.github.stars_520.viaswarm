# ViaSwarm

[![LSPosed](https://img.shields.io/badge/LSPosed-supported-green)](https://modules.lsposed.org/)
[![Android](https://img.shields.io/badge/Android-7.0%2B-blue)](https://www.android.com/)

**把「鼠标集群动画」（cursor swarm）注入 Via 浏览器的 LSPosed 模块。**

打开任意网页，右下角出现一个绿色按钮，点一下，一群多人协作光标涌进来，把你的页面拆成蓝图再逐格重画出来。

---

## 这是什么

这个模块做两件事：在 Via 的 WebView 加载完页面后注入一段 JavaScript，然后给你一个按钮来控制它。

- 作用域只有一个：`mark.via`
- hook 点只有一个：`p4.j#onPageFinished(WebView, String)`
- 不做网络请求，不写文件，不申请额外权限

## 效果

核心是鼠标集群动画（cursor swarm）：

1. 扫描当前页面，把每个元素的位置、尺寸、文字、边框、颜色、媒体记成一份蓝图
2. 清空页面
3. 一群虚拟光标从画面外飞进来，用十字准星画矩形、用打字机逐字写文本、用钢笔工具画线，把页面一块一块重建

看到的效果是「页面被一群人现场重新实现」。

## 使用方法

1. 安装本模块
2. 在 **LSPosed** 中启用，作用域勾选 **Via**
3. 强制停止 Via，重新打开
4. 打开任意网页，右下角出现绿色按钮，点击即可

按钮再次点击会切换成 Stop。

## 环境要求

| 项 | 要求 |
|---|---|
| 设备 | 已 root，装了 LSPosed（Zygisk 或 Riru 都行） |
| 系统 | Android 7.0 及以上（minSdk 24） |
| 目标 | Via 浏览器 7.2.1（versionCode 20260706） |

## 模块信息

| 项 | 值 |
|---|---|
| 包名 | `io.github.stars_520.viaswarm` |
| 版本 | 1.0 (versionCode 1) |
| 作用域 | `mark.via` |
| 许可证 | MIT |
| 作者 | Stars. |
| Xposed API | legacy API 82 |

## 关于安全

模块本身不联网、不写文件、不收集数据。注入的脚本全部本地执行，没有 `fetch` / `XMLHttpRequest` / `eval` / `localStorage`，页面内容和浏览记录不出设备。

源码完全公开，可自行审阅：[Stars-520/ViaSwarm](https://github.com/Stars-520/ViaSwarm)

## 失效了怎么办

Via 更新后混淆名会变，hook 点 `p4.j` 可能对不上。改法：

1. 用 `jadx` 反编译新版 Via
2. 搜 `onPageFinished`，找到对应的混淆类名
3. 改 `Hook.java` 里的目标类名，重新构建

## 许可

MIT
<!-- refreshed:2026-11-11T09:09:27Z -->
