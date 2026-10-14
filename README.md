# OpenClash 在线订阅转换模板

用于软路由 OpenClash 的 subconverter 外部配置模板。当前包含 36 个策略组；Muse、ChatGPT、Claude、Gemini 独立分组，抖音、剪映、微信、QQ 归国内媒体，TikTok 独立分流。

## 直接使用

在 OpenClash「配置订阅」中，填写自己的机场原始订阅，开启「在线订阅转换」，模板名称选「自定义模板」，将下方地址填入「自定义模板地址」：

```text
https://raw.githubusercontent.com/kaixinhu780-ops/openclash-rules/main/openclash-subconverter.ini
```

转换地址使用你信任的 subconverter 后端。本模板包含 429 条 ruleset 配置，后端 `max_allowed_rulesets` 需为 `0`（不限）或至少 `429`。

模板已引用本仓库的 [DNS/嗅探基础配置](openclash-dns-base.yaml)，建议使用较新的 Meta/Mihomo 内核。软路由仍需启用 DNS 接管并核对 OpenClash 覆写设置。

## 文件

- [订阅转换模板](openclash-subconverter.ini)
- [DNS/嗅探基础配置](openclash-dns-base.yaml)
- [完整使用说明](在线转换使用说明.md)
- [AI 域名清单与来源](国外AI域名清单.md)

仓库不包含节点、订阅凭据或账号密码。模板引用第三方维护的公开规则，来源见说明文件。

## 已完成的验证

实际 subconverter 转换、100 个代表性域名命中、分组引用与 Mihomo 配置检查通过。尚未在用户软路由、真实订阅或 App 中完成联网验收。
