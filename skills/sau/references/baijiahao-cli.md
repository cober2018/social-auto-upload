# 百家号

> CLI 未接入，当前通过 Python 脚本直接调用。

## 核心模块

- `uploader/baijiahao_uploader/main.py` — 使用 playwright 驱动

## 支持功能

- 登录（浏览器 `page.pause()` 手动登录）
- Cookie 校验
- 视频上传

## 调用方式

直接引用模块：

```python
from uploader.baijiahao_uploader.main import (
    baijiahao_cookie_gen,
    cookie_auth as baijiahao_cookie_auth,
)
```

或参考 `examples/` 下的百家号示例脚本。

## 登录说明

- 登录使用 `page.pause()` 暂停浏览器，用户需手动操作完成登录
- 登录完成后点击调试器「继续」，程序自动保存 cookie
- 必须由用户在本地有头模式下操作，agent 不应代跑
