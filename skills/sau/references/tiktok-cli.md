# TikTok

> CLI 未接入，当前通过 Python 脚本直接调用。

## 核心模块

- `uploader/tk_uploader/main.py` — 使用 playwright + Firefox 驱动
- `uploader/tk_uploader/tk_config.py` — TikTok 页面定位器配置

## 支持功能

- 登录（浏览器登录 + cookie 保存）
- Cookie 校验（访问 TikTok Studio 检查登录状态）
- 视频上传

## 调用方式

直接引用模块：

```python
from uploader.tk_uploader.main import (
    tiktok_setup,
    cookie_auth as tiktok_cookie_auth,
)
```

或参考 `examples/` 下的 TikTok 示例脚本。

## 登录说明

- 使用 Firefox 浏览器（非 Chromium）
- 登录时打开 TikTok 页面，用户可通过 Gmail/手机等方式登录
- 登录完成后自动保存 cookie

## 注意事项

- TikTok 上传目标地址：`https://www.tiktok.com/tiktokstudio/upload?lang=en`
- 需要能正常访问 TikTok 的网络环境
