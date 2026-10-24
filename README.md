# YouTube Shadowrocket

基于 [Maasea/sgmodule](https://github.com/Maasea/sgmodule) 的 YouTube 小火箭适配配置。

已有实际使用反馈：能够拦截部分 YouTube 广告，仍可能漏掉少量广告。效果可能随 YouTube、账号、地区及客户端版本变化。

## 安装

在 Shadowrocket 中打开 **配置 → 模块 → 右上角 +**，粘贴以下地址并下载：

```text
https://raw.githubusercontent.com/chiypa/youtube-shadowrocket/main/YouTube.Enhance.Shadowrocket.sgmodule
```

启用本模块，并停用其他处理相同 YouTube 请求的模块，避免重复处理。

## HTTPS 解密

本模块需要对指定的 YouTube 域名进行 HTTPS 解密，才能运行请求和响应脚本。

1. 在当前使用的配置中打开 **HTTPS 解密**。
2. 按小火箭提示生成并安装 CA 证书。
3. 在 iOS **设置 → 通用 → 关于本机 → 证书信任设置**中，完全信任刚安装的 Shadowrocket 证书。
4. 确认两个远程脚本已下载成功。模块有三条脚本配置，其中两条共用同一文件。
5. 重新连接小火箭，彻底退出 YouTube 后重新打开。

只在自己的设备上安装、信任自己生成的证书。证书和私钥不随本项目分发。

## 本项目的调整

- 将上游模板参数改为固定值，并保留 `argument` 的整体引号写法。
- 修正 `initplayback` 规则，使 `ack` 位于第一个查询参数时也能匹配。
- 保留原适配配置中的广告域名拦截规则和 UDP 443 阻断规则。
- 日常版默认设置 `debug:false`，减少调试输出。

当前固定设置：关闭字幕翻译，隐藏上传及选段按钮，保留 Shorts 按钮。

去广告处理脚本仍直接引用 Maasea 的上游文件，本仓库没有复制或自行实现脚本核心。远程脚本随上游更新，本仓库没有固定其版本。

## 速度与排查

- 日常使用可关闭小火箭的代理日志记录；关闭本模块的调试输出不等于关闭小火箭自己的日志。
- 解密和脚本处理会增加处理开销。
- 本模块保留的 UDP 443 阻断规则适用于所有目标域名，会影响其他应用使用该端口的流量，并可能带来连接回退开销。
- 若感觉变慢，先保持节点、网络和模块不变，对比开启与关闭日志记录的体验。
- 若仍有广告，先检查 HTTPS 解密、证书信任及脚本下载状态，再检查脚本运行日志。

请勿直接公开完整代理日志、访问记录、代理订阅链接、证书或私钥。反馈问题时可提供系统和应用版本、广告类型及已去除个人信息的错误信息。

## 验证范围

2026-10-22 的适配配置收到用户反馈：去广告有效，但仍有少量漏拦。2026-10-24 整理发布文件并默认关闭调试输出。参数已做静态检查；本次发布整理没有重新进行手机端测试。

## 致谢与许可证

- 原项目及处理脚本：[Maasea/sgmodule](https://github.com/Maasea/sgmodule)
- 原始模块：[YouTube.Enhance.sgmodule](https://github.com/Maasea/sgmodule/blob/master/YouTube.Enhance.sgmodule)
- 本仓库：[chiypa/youtube-shadowrocket](https://github.com/chiypa/youtube-shadowrocket)

基于 Apache License 2.0 发布，保留上游来源并注明配置修改。详见 [LICENSE](LICENSE) 和 [NOTICE](NOTICE)。
