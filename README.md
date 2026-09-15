# dsh-helper — 一台电脑，并行无限实例

[English](README.en.md) · [用户指南](docs/user-guide.zh-CN.md) · [Releases](https://github.com/x102201/dsh-helper/releases)

![演示](docs/assets/video/dsh-helper-demo.gif)

[下载完整演示视频（mp4）](docs/assets/video/dsh-helper-demo.mp4)

我这边常年多条业务并行。默认只有一套 dsh，能力集中装进同一工作空间后会互相冲突——所以做成了这个：
**一个桌面窗口里，并行运行任意多个互不干扰的 DeepSeek Harness。每个实例 = 一整套独立的 dsh。**

---

## 一、隔离：一套 dsh 无法承载两套工作负载

### 痛点

我这边常年三条业务并行：客户消息、代码、测试与报告。

默认只有一套 dsh（一份 `DSH_HOME`）。插件全部装进同一个工作空间，工具列表一长，模型就开始选错工具——不是配置问题，是三套互不相关的能力集中进一套预设，**结构上无法承载**。

Agent 预设无法拆开并行：**一次会话只能挂载一套**，开过一轮再切换会被锁定。

> 依据 DeepSeek Harness：[《Agent Presets and Personas》](https://deepseekdocs.com/en/docs/features/persona) · [架构说明《A session's agent is composed from a preset》](https://github.com/deepseek-ai/deepseek-harness/blob/master/.agents/notes/implemented/architecture/2026-08-03-per-session-agent-presets.md)

### 解法

不要把全部工作负载集中进一个 dsh。
**每个实例 = 一整套独立的 dsh**（独立进程、独立端口、独立 `DSH_HOME`），不是同一个运行时里的标签页。

左侧客服、右侧开发、下方测试——需要几套就运行几套，插件互不冲突。

![分屏实机](docs/assets/zh-CN/screenshot-main-light.png)

> 隔离之后各自独立运行，边界很清楚。但真实业务并不是三条互不相交的线——
> 客户侧的变更终究要传到开发侧。这是第二节要讲的。

---

## 二、协作：多个专职实例，同一工作区

**每一个 dsh 就是一个专职实例**：客服、开发、测试各承担一类工作负载。插件按实例隔离——这是第一节。

但这三个实例推进的是同一份交付。拆到三台电脑等于三倍硬件、目录分散、无法在同一工作区查看。**专职实例需要在同一工作区并行，而不是一台机器一个实例。**

在一台电脑的工作区里并行：**三个实例共用同一个项目目录**；插件隔离，文件共享。分屏调度——左侧提交变更，右侧更新同一份说明，下方按清单验收。

这不是三个无关窗口并排，是同一工作区里三个专职实例推进**同一版本**。

![专职实例：同一工作区 vs 一台机器一个实例](docs/assets/zh-CN/collab-model.svg)

---

## 三、交付：配置好几个实例，就导出几个包

**环境即产品，导出即交付。**

花了好几天，才把客服、开发、测试三个专职实例一起跑通——插件、预设、流程逐步对齐。

然后需要交付给他人。真正卡住的不是「会不会用」，而是**每次交付都像再做一遍工程**：

1. **无法复原** — 过几天连自己都说不清哪几个插件、哪份预设才是这一套；给对方部署，结果对不上，又耗掉几天
2. **无法交付** — 说明文档装不全；拷贝目录又面临不受控的二次分发
3. **无法规模化** — 第二个、第三个客户还要再远程部署一遍，**部署时间远大于配置时间**，无法规模化交付

**`.dshpack`：** 把已经配置好的那一个实例（一整套 dsh）导出为文件。导入即可运行；可绑定机器码 / 密码，可禁止再导出——交付的是成品，不是部署劳务。

配置好几个专职实例，就导出几个包。一份 `.dshpack` 仍是一份 dsh；导入后出现在侧栏，工作区分屏由使用方自行安排。

![制品流程](docs/assets/zh-CN/dshpack-flow.svg)

---

## 用户指南

1. [概念](docs/user-guide.zh-CN.md#概念)
2. [安装](docs/user-guide.zh-CN.md#安装)
3. [第一次启动](docs/user-guide.zh-CN.md#第一次启动)
4. [工作间](docs/user-guide.zh-CN.md#工作间)
5. [制品（.dshpack）](docs/user-guide.zh-CN.md#制品dshpack)
6. [数据、迁移与卸载](docs/user-guide.zh-CN.md#数据迁移与卸载)
7. [设置参考](docs/user-guide.zh-CN.md#设置参考)
8. [排错](docs/user-guide.zh-CN.md#排错)
