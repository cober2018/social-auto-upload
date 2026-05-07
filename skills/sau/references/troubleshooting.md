# 故障排查

## 找不到 `sau` 命令

```bash
source .venv/bin/activate
sau --help
```

或：

```bash
uv run sau --help
.venv/bin/sau --help
```

如果还没安装：

```bash
uv pip install -e .
```

## cookie 无效或已过期

```bash
sau <platform> check --account <account>
```

如果返回 `invalid`，重新登录：

```bash
sau <platform> login --account <account>
```

## 二维码处理

- 抖音/快手/小红书：agent 应直接把二维码图片展示给用户扫码，不要只返回路径
- Bilibili：必须由用户在本地终端执行 `sau bilibili login --account <name>`，二维码显示不完整时打开 `qrcode.png`

## 上传参数缺失

视频上传最少需要：`--account`、`--file`、`--title`
图文上传最少需要：`--account`、`--images`、`--title`

## 图片限制

- 抖音：最多 35 张，不支持 GIF
- 快手：建议传真实不同文件，不要重复路径
- 小红书：`--note` 可选，`--title` 建议始终传入

## 定时发布格式

```
--schedule "YYYY-MM-DD HH:MM"
```

## Bilibili 特有

- `--tid` 必填（分区 ID）
- 程序自动下载/更新 `biliup`，无需手动安装
- 如果国内网络下载慢，可用 `https://gh-proxy.org/` 辅助

## 未接入 CLI 的平台

视频号、百家号、TikTok 目前只能通过 Python 脚本调用，参考 `uploader/<platform>/main.py` 和 `examples/`。
