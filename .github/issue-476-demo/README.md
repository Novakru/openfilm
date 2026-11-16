# Issue #476：初步排查演示

测试时间：2026-11-16（Asia/Shanghai）。Windows，OpenFilm 0.3.2，源代码提交 `0bc08008d933af7d42ef73a53cae384e2f54e6eb`。

- `openrouter-real.gif`：原版 OpenFilm 经 OpenRouter / FLUX.3 完成真实生图。无参考图和三张参考图各一次，均 HTTP 200。右侧为本地只读采集的真实后台请求／响应摘要，不是 OpenRouter 官网控制台。三张发送图片经 SHA-256 核对，画布保存结果与 API 返回图片一致。GIF 注明并省略了约 20.4 秒中间等待；图片没有替换为模拟响应。
- `google-request-only.gif`：Google 直连分支的本地请求构造检查。使用独立测试配置启用该分支，捕获原版适配器准备发送的请求，在网络发送前中止。未调用 Google API，没有真实云端生图结果，也没有模拟成功响应。画面中的中止提示由检查工具产生，不是 Google 返回的错误。画布连接三张图片，构造的请求仅含文本，与代码中的 `refs: 0` 对应。

两段 GIF 均由真实 Chromium 操作录屏转换，鼠标为连续移动的录制辅助指针，实际点击由 Playwright 执行。仅为录制预留旁侧观察面板；产品源代码未修改。

## 参考照片与许可

照片缩放、补边至 640×480，用于同一提示词的参考图测试；生成图片为模型对这些照片内容的重新组合。

1. 小黄鸭 — Pieter de derde，2022-12-06。[原始文件](https://commons.wikimedia.org/wiki/File:1_Yellow_rubber_duck.jpg)，[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)。
2. 红色咖啡杯 — Daderot。[原始文件](https://commons.wikimedia.org/wiki/File:Coffee_-_Massachusetts.jpg)，[CC0](https://creativecommons.org/publicdomain/zero/1.0/)。
3. 向日葵 — H. Zell，2012-07-29。[原始文件](https://commons.wikimedia.org/wiki/File:Helianthus_annuus_inflorescence.jpg)，[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)。

演示中对上述照片的使用及改编按 CC BY-SA 4.0 分享，并保留各原图作者及原许可信息。此目录仅为 issue 演示素材，不属于功能修复代码。
