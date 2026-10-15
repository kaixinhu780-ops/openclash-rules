# OpenClash 在线订阅转换模板

## new-meta.ini 的 Siri 扩展版本

另提供基于用户指定的 usbog232/clashmetadingyue/new-meta.ini 的 [new-meta-siri.ini](new-meta-siri.ini)，新增“🍎 Siri Intelligence”和 11 条优先匹配的 Siri/PCC/扩展规则，另有“🧩 Muse AI”固定出口及 555 条 Meta 共享域名覆盖。[Muse 使用与边界](new-meta-siri-muse说明.md)。[来源、域名说明及使用方法](new-meta-siri说明.md)。此版本的 DNS 仍需在 OpenClash 中单独设置。

> 2026-10-15 DNS 修复：普通查询和 DIRECT 域名解析统一经“👆 手动选择”访问海外加密 DNS；仅节点引导使用直连加密 DNS。更新订阅后必须检查 OpenClash 最终运行配置，详见 [DNS修复说明](DNS修复说明.md)。

> 当前策略（2026-10-15 社交分组恢复）：Muse 专用域名最先匹配；Instagram、WhatsApp、Facebook 社交规则随后匹配；Meta 共享域名集最后补充。共享规则不再优先覆盖这三个平台。广告拦截仍在前面。
>
> 小火箭：Instagram → 📸 Instagram，WhatsApp → 📞 WhatsApp，Facebook → 🌐 国外社交。OpenClash：按已有合并分组，三者 → 🌐 国外社交。共享登录或 CDN 仅能按域名判定用途，Muse 若涉及这些端点，也会采用社交策略；需要一致出口时，让相应社交策略与 Muse 选择同一节点。


用于软路由 OpenClash 的 subconverter 外部配置模板。当前包含 30 个策略组；Muse、ChatGPT、Claude、Gemini 独立分组，抖音、剪映、微信、QQ 归国内媒体，TikTok 独立分流。

## 直接使用

在 OpenClash「配置订阅」中，填写自己的机场原始订阅，开启「在线订阅转换」，模板名称选「自定义模板」，将下方地址填入「自定义模板地址」：

```text
https://raw.githubusercontent.com/kaixinhu780-ops/openclash-rules/main/openclash-subconverter.ini
```

转换地址使用你信任的 subconverter 后端。本模板包含 223 条 ruleset 配置，后端 `max_allowed_rulesets` 需为 `0`（不限）或至少 `223`。

模板已引用本仓库的 [DNS/嗅探基础配置](openclash-dns-base.yaml)，建议使用较新的 Meta/Mihomo 内核。软路由仍需启用 DNS 接管并核对 OpenClash 覆写设置。

## 文件

- [订阅转换模板](openclash-subconverter.ini)
- [DNS/嗅探基础配置](openclash-dns-base.yaml)
- [完整使用说明](在线转换使用说明.md)
- [AI 域名清单与来源](国外AI域名清单.md)

> 💡 如果你需要适用于 **Clash Verge / Clash Verge Rev** 的分流模板，请访问专属独立仓库：[clash-verge-rules](https://github.com/kaixinhu780-ops/clash-verge-rules)。

仓库不包含节点、订阅凭据或账号密码。模板引用第三方维护的公开规则，来源见说明文件。

## 已完成的验证

实际 subconverter 转换、100 个代表性域名命中、分组引用与 Mihomo 配置检查通过。尚未在用户软路由、真实订阅或 App 中完成联网验收。

2026-10-15：Muse 扩展至 555 条 Meta 共享域名条件，Facebook/Instagram/WhatsApp 等命中请求也跟随 Muse。详见 [Muse扩展说明](Muse扩展说明.md)。

本次 Muse 扩展已基于远端 v1.3 后的 main 合并，保留远端 DNS 底稿、分组合并与香港手动选择。当前模板为 30 个策略组、223 个 ruleset 条目；前文旧版验证记录不代表当前分组数量。
