---
name: sau
description: |
  社交媒体自动发布统一入口。一个 skill 覆盖 7 个平台：抖音、快手、小红书、Bilibili、视频号、百家号、TikTok。
  触发方式：/sau、「登录抖音」「上传视频到快手」「发小红书图文」「检查B站账号」等自然语言。
  Unified social media auto-upload entry. One skill for 7 platforms.
  Trigger: /sau, "login douyin", "upload video to kuaishou", "post xiaohongshu note", etc.
---

# sau — 社交媒体自动发布路由器

根据用户意图，路由到对应平台和操作。说人话就行，不用记命令。

## 路由表

| 用户意图 | 平台 | 操作 | 详细文档 |
|---------|------|------|---------|
| 抖音 / douyin | douyin | login / check / upload-video / upload-note | [references/douyin-cli.md](references/douyin-cli.md) |
| 快手 / kuaishou | kuaishou | login / check / upload-video / upload-note | [references/kuaishou-cli.md](references/kuaishou-cli.md) |
| 小红书 / xiaohongshu / xhs | xiaohongshu | login / check / upload-video / upload-note | [references/xiaohongshu-cli.md](references/xiaohongshu-cli.md) |
| B站 / Bilibili / bili | bilibili | login / check / upload-video | [references/bilibili-cli.md](references/bilibili-cli.md) |
| 视频号 / 微信视频号 | video-channel | Python 脚本调用 | [references/video-channel-cli.md](references/video-channel-cli.md) |
| 百家号 / baijiahao | baijiahao | Python 脚本调用 | [references/baijiahao-cli.md](references/baijiahao-cli.md) |
| TikTok / tk / 国际版 | tiktok | Python 脚本调用 | [references/tiktok-cli.md](references/tiktok-cli.md) |

## 平台接入状态

| 平台 | CLI 已接入 | 登录方式 |
|------|-----------|---------|
| 抖音 | `sau douyin` | 浏览器扫码，agent 可代跑 |
| 快手 | `sau kuaishou` | 浏览器扫码，agent 可代跑 |
| 小红书 | `sau xiaohongshu` | 浏览器扫码，agent 可代跑 |
| Bilibili | `sau bilibili` | biliup 二维码，**用户必须在本地终端执行** |
| 视频号 | 未接入 | 微信扫码，走 Python 脚本 |
| 百家号 | 未接入 | 手动浏览器登录，走 Python 脚本 |
| TikTok | 未接入 | 浏览器登录（Firefox），走 Python 脚本 |

## 快速命令

### 登录

```bash
# 抖音 / 快手 / 小红书 — agent 可直接跑
sau douyin login --account <name>
sau kuaishou login --account <name>
sau xiaohongshu login --account <name>

# Bilibili — 必须让用户自己在本地终端跑
# 不要在非交互环境代跑
sau bilibili login --account <name>
```

### 检查账号状态

```bash
sau douyin check --account <name>
sau kuaishou check --account <name>
sau xiaohongshu check --account <name>
sau bilibili check --account <name>
```

### 上传视频

```bash
sau douyin upload-video --account <name> --file <video> --title "标题"
sau kuaishou upload-video --account <name> --file <video> --title "标题"
sau xiaohongshu upload-video --account <name> --file <video> --title "标题"
sau bilibili upload-video --account <name> --file <video> --title "标题" --desc "简介" --tid 249
```

### 上传图文

```bash
sau douyin upload-note --account <name> --images 1.png 2.png --title "标题"
sau kuaishou upload-note --account <name> --images 1.png 2.png 3.png --title "标题"
sau xiaohongshu upload-note --account <name> --images 1.png 2.png --title "标题"
```

### 定时发布

加 `--schedule "YYYY-MM-DD HH:MM"` 即可切换为定时发布。

```bash
sau douyin upload-video --account <name> --file demo.mp4 --title "标题" --schedule "2026-05-10 18:00"
```

## 工作流

1. 从用户输入识别**平台** + **操作**
2. 查路由表，确认平台是否已接入 CLI
3. **已接入 CLI**：直接构造 `sau <platform> <action>` 命令执行
4. **未接入 CLI**：读对应 reference 文档，引导用户走 Python 脚本
5. 如果登录产生二维码图片，**直接展示图片给用户**，不要只返回路径
6. 如果命令失败，读 [references/troubleshooting.md](references/troubleshooting.md)

## 登录注意事项

**关键区分**：

- **抖音/快手/小红书**：agent 可以代跑登录命令。二维码生成后直接展示图片给用户扫码。
- **Bilibili**：必须用户自己在本地真实终端执行 `sau bilibili login --account <name>`。如果二维码显示不完整，打开当前目录的 `qrcode.png` 扫码。agent **不要**在非交互环境硬跑。
- **视频号/百家号/TikTok**：走 Python 脚本，需要用户手动操作浏览器。

## 执行前检查

- 确认 `sau` 可调用，不行就先 `source .venv/bin/activate`
- 确认 patchright Chromium 已安装
- 如果 `sau` 完全不可用，读 [references/runtime-requirements.md](references/runtime-requirements.md) 安装

## 元数据约定

- 视频：`--title` + `--desc` + `--tags`
- 图文：`--title` + `--note` + `--tags`
- Bilibili 额外必填：`--tid`（分区 ID）

## 参考文档

按需读取，不要一次全加载：

- [运行前提](references/runtime-requirements.md)
- [抖音 CLI](references/douyin-cli.md)
- [快手 CLI](references/kuaishou-cli.md)
- [小红书 CLI](references/xiaohongshu-cli.md)
- [Bilibili CLI](references/bilibili-cli.md)
- [视频号](references/video-channel-cli.md)
- [百家号](references/baijiahao-cli.md)
- [TikTok](references/tiktok-cli.md)
- [故障排查](references/troubleshooting.md)
