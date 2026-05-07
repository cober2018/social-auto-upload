# 运行前提

默认假设当前环境已经具备：

- 已安装 `social-auto-upload`（`uv pip install -e .`）
- 可以调用 `sau` 命令，或至少有等效调用方式
- 已为 `patchright` 安装 Chromium

## 安装

```bash
cd social-auto-upload
uv venv
source .venv/bin/activate   # macOS/Linux
uv pip install -e .
```

## 安装 patchright 浏览器

macOS / Linux：

```bash
PLAYWRIGHT_DOWNLOAD_HOST="https://npmmirror.com/mirrors/playwright" patchright install chromium
```

Windows PowerShell：

```powershell
$env:PLAYWRIGHT_DOWNLOAD_HOST="https://npymirror.com/mirrors/playwright"; patchright install chromium
```

## 配置文件

```bash
cp conf.example.py conf.py
```

## 调用方式

如果 `sau` 不在 PATH 中：

```bash
# 激活虚拟环境
source .venv/bin/activate

# 或直接用 uv
uv run sau --help

# 或直接调用
.venv/bin/sau --help
```

## 无头和有头模式

- `--headless`：无头模式（默认）
- `--headed`：有头模式，浏览器可见
