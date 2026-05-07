# 视频号（微信视频号）

> CLI 未接入，当前通过 Python 脚本直接调用。

## 核心模块

- `uploader/tencent_uploader/main.py` — 使用 patchright 驱动

## 支持功能

- 登录（二维码扫码）
- Cookie 校验
- 视频上传（支持定时发布）
- 图文上传

## 调用方式

直接引用模块：

```python
from uploader.tencent_uploader.main import (
    tencent_setup,
    cookie_auth as tencent_cookie_auth,
    TencentVideo,
)
```

或参考 `examples/` 下的视频号示例脚本。

## 登录说明

- 登录会打开浏览器，通过微信扫码完成
- Cookie 文件存储在 `cookies/tencent_uploader/` 目录下
- 如果需要查看二维码，agent 应直接展示图片给用户
