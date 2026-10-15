# 基于 new-meta.ini 的 Siri Intelligence 扩展

文件：[new-meta-siri.ini](new-meta-siri.ini)。日期：2026-10-15。

已克隆来源仓库 [usbog232/clashmetadingyue](https://github.com/usbog232/clashmetadingyue)，基于提交 `dc4ce21d9a69e275d1fa06e70501ff69be56c950` 的 `new-meta.ini` 修改。原模板各项规则、选择器和节点筛选保持原文，仅新增 Siri 规则块与一个策略组；可复现补丁见 [new-meta-siri.patch](new-meta-siri.patch)。来源仓库未附 LICENSE，来源署名保留在文件内；本仓库不对来源内容新增授权声明。

## 新策略组

“🍎 Siri Intelligence”默认跟随原模板的“🤖 ChatGPT”，也能选择全部节点、美国、日本、台湾、新加坡、香港、冷门节点及自动选择。建议两组固定到同一个可用节点；延迟最低并不等于 Siri 最稳定。源模板地区组在没有匹配节点时可能由转换器填入 DIRECT，应在导入后确认实际选项和节点，不能选择空地区组。

优先级为：**Siri 专用规则 → 原模板所有规则（包括私网、直连补丁、国内、ChatGPT、Apple、Cloudflare 等）**。这样可以避免 Siri 域名先被 GEOSITE,cn 或通用补丁判为直连。UI 中 Siri 组位于 Apple 组之前。

## 启用的 11 条条件

| 类型 | 域名 | 依据 / 范围 |
| --- | --- | --- |
| DOMAIN | guzzoni.apple.com | Apple 官方：Siri、听写 |
| DOMAIN-SUFFIX | smoot.apple.com | Apple 官方：Siri / Spotlight 等搜索服务 |
| DOMAIN | apple-relay.cloudflare.com | Apple 官方：PCC |
| DOMAIN | apple-relay.fastly-edge.com | Apple 官方：PCC |
| DOMAIN | cp4.cloudflare.com | Apple 官方：PCC |
| DOMAIN | apple-relay.apple.com | Apple 官方：Apple Intelligence 扩展 |
| DOMAIN | apple-relay.mask.apple-dns.net | v2fly、MetaCubeX / dler 社区维护源的中继补充 |
| DOMAIN | gspe1-ssl.ls.apple.com | 社区维护源：网络地区检测，也影响地图、部分设备地区功能等 |
| DOMAIN-SUFFIX | siri.apple.com | v2fly Apple 清单中的 probe / seed 等主机合并为 Siri 专用后缀 |
| DOMAIN | guzzoni-apple-com.v.aaplimg.com | v2fly Apple 清单中的 Siri 别名 |
| DOMAIN | apple-relay.akamaized.net | 社区使用者报告的中继补充，非 Apple 官方完整网络清单，需结合请求日志验证 |

DOMAIN-SUFFIX 同时覆盖根域名和所有子域名。前六项来自官方网络文档，其余是社区补充，证据等级不同。

## ChatGPT 与共享域名

Siri 的 ChatGPT 扩展主要在 Apple 端经扩展中继交接。普通 OpenAI / ChatGPT 网站和 App 请求仍使用原模板的“🤖 ChatGPT”组；Siri 组默认跟随它，保持相同出口。仅凭域名规则无法可靠区分“从 Siri 发起的 OpenAI 请求”和“普通 ChatGPT 请求”，因此没有把整个 OpenAI 分类强行挪走。

模板内还提供两条默认注释的兼容项：`gateway.icloud.com`、`apps.mzstatic.com`。前者也用于 CloudKit / Voice Control 等服务，后者是共享应用资源；它们不是 Siri 专用域名。只有请求日志证明相关连接失败时才考虑启用。没有将整个 apple.com、icloud.com、Cloudflare、Google、Azure 或 Apple 的 17.0.0.0/8 网络划给 Siri。

Apple 当前已公布 Siri AI Beta 的使用要求，但未公布可确保覆盖一切新链路的独立域名全集。此模板以目前可核对的 Siri/PCC/扩展端点为基础，不能承诺未来无需维护，也不能代替设备、系统、语言和地区资格。

## 使用

本文件是 **subconverter 外部配置模板**，不是完整节点订阅。在 OpenClash 的在线订阅转换设置中，原始订阅保持使用自己的节点地址，自定义模板地址改为本文件的 Raw 地址，然后更新订阅。需要 Meta/Mihomo 内核及匹配的 GeoSite / GeoIP 数据。

本版本沿用源模板的 DNS 配置边界：INI 自身不设置 DNS，也没有附加 DNS 底稿。路由器上的 DNS 覆写、DNS 接管和 IPv6 路径仍需单独配置和检查；不能把 Siri 分流检查通过理解为 DNS 防泄漏验收。

导入后检查 Siri 组选择的实际节点，再分别测试：Siri 普通语音、打字请求 ChatGPT、语音请求 ChatGPT；在连接日志确认对应域名命中 Siri Intelligence。如果某连接落到 Apple / DIRECT，可根据具体请求补充窄范围规则。无需安装 HTTPS 解密证书，不改写地区检测响应。

## 验证

- 已确认源仓库可克隆，并保存源提交、文件 SHA256 和可复现补丁。
- 原模板移除本次新增块后可逐字恢复；新增后共 37 个策略组、48 个 ruleset 条目。
- 五个原模板远程规则源下载成功；实际 subconverter v0.9.0 转换成功。
- 11 条 Siri 条件均位于转换结果最前面，13 个代表性主机（含子域名及别名）命中检查通过；原 Apple、ChatGPT、Cloudflare 规则保留。
- 官方 Mihomo v1.19.32 配置检查通过，采用 MetaCubeX 维护的 GeoSite 数据核验原模板各分类。
- 尚未在用户真实订阅、软路由、手机及 Siri AI Beta 上完成功能验收。

## 域名依据

- [Apple 企业网络端点](https://support.apple.com/en-us/101555)：官方 Siri/PCC/扩展端点；官方亦说明 CDN CNAME 会变化，并未提供完整列表。
- [Apple Siri AI 使用要求](https://support.apple.com/en-us/127893)：当前 Beta、语言与地区限制。
- [v2fly Apple Intelligence](https://github.com/v2fly/domain-list-community/blob/master/data/apple-intelligence)、[Apple 主机清单](https://github.com/v2fly/domain-list-community/blob/master/data/apple)：补充中继、地区检测及语音主机。
- [Sukka Apple Intelligence](https://github.com/SukkaW/Surge/blob/master/Source/non_ip/apple_intelligence.conf)、[dler 规则](https://github.com/dler-io/Rules/blob/main/QuantumultX/Tail.conf)：交叉核对社区中继规则。
- [维护仓库中的使用者报告](https://github.com/Loyalsoldier/v2ray-rules-dat/issues/504)：akamaized 补充和共享兼容端点的低置信度依据，不视为官方保证。
