# new-meta-siri.ini：Muse AI 固定出口扩展

更新日期：2026-10-15。在线模板文件仍为 [new-meta-siri.ini](new-meta-siri.ini)，在此前 Siri 扩展版本上增加 Muse；不是对另一份 openclash-subconverter.ini 的修改。

## 使用顺序

1. 更新订阅并重新生成配置。
2. “🧩 Muse AI”选择“🔒 Muse 固定出口”。
3. 在“🔒 Muse 固定出口”中手动选择一个已确认可用的实际节点；使用期间保持选择稳定。不要把“固定节点名称”等同于服务商保证固定出口 IP，应自行确认节点是否会轮换出口。
4. 每次更新订阅后重新检查实际选择。没有匹配节点时此组只留下 REJECT；也可以主动选择 REJECT 禁用匹配请求。

Muse 主组和固定出口组均没有 DIRECT、Default、自动测速或地区组引用。这样避免新增 Muse 策略通过其他组间接选到直连，也避免因自动测速而主动切换出口。原模板其他应用组的设置保留。

## 覆盖与优先级

- 显式保护 muse.ai、meta.ai、metaaivm.com（含全部子域名）及 auth.meta.com。
- 使用 GEOSITE,meta，随本地 GeoSite 数据更新扩展已收录的 Meta 分类。
- 再使用维护源递归展开的 [555 条 Meta 共享域名快照](rules/MuseMeta.yaml)，补充 Facebook、Facebook 开发者服务、Instagram、Messenger、WhatsApp、Threads、Oculus/Quest、共享 CDN、Meta 登录和 Llama 等域名。该快照不是官方 Muse 网络白名单，也不表示逐一验证域名所有权。
- 每项 Muse 条件后有同条件的 REJECT，供不支持 UDP 的代理不能处理该条件时阻止后续规则转入 DIRECT；没有给全局网络添加“拒绝全部 UDP”之类的规则。

顺序是 **Siri 专用规则 → Muse 显式条件/Meta 分类/共享快照及对应 REJECT → 原模板的 Adobe、私网、国内、直连补丁和其他业务规则**。

**此版本命中共享域名的 Facebook、Instagram、WhatsApp 等请求也会改走 Muse 固定出口，优先于它们原有的社交组。** 域名规则无法判断同一共享域名当前是由 Muse 还是普通社交 App 使用，这是扩大覆盖的实际影响。

没有把整个 Cloudflare、AWS、Azure、Google 域名或整个 ASN 作为 Muse 流量，因为那会影响大量无关服务。也没有把未知第三方连接全部认定为 Muse。

## 风险边界

这是降低已收录连接错误直连和出口切换风险的配置，**不能承诺绝对零 IP 泄漏，也不能保证避免封号**。尚未收录的域名、无主机名的 IP 请求、浏览器/应用自带解析、IPv6、没有经过 OpenClash 的设备流量，仍受设备和路由器配置影响。原模板的通用兜底仍允许用户选择 DIRECT，它无法识别一条未知请求是否来自 Muse；重要使用场景应检查实际出口和连接日志，不能只看 Muse 组名称。

本 INI 没有自动提供 DNS 底稿，DNS 接管、覆写、IPv6 和设备网关需要在 OpenClash/路由器侧核验。代理/内核停止后的网络行为也不由这些域名规则保证。

账号能否使用服务还取决于服务资格及其他风控信号。此配置不修改账号信息或地区检测响应，也不安装解密证书。

## 验证

- 原有 37 个分组定义逐项保留，新增 Muse 和固定出口辅助组后共 39 组、60 个 ruleset 条目。
- 实际 subconverter 转换成功；原 11 条 Siri 条件仍在最前面。
- 555 条共享域名及 9 项登录、CDN、嵌套 VM 和社交测试主机命中 Muse。
- 转换后的固定出口只能选择实际节点或 REJECT，没有 DIRECT 或其他组的间接引用；模拟无匹配节点时只有 REJECT。
- Mihomo v1.19.32 配置检查通过，GeoSite,meta 能被实际加载。
- 未在用户节点、手机、账号或软路由上完成出口抓包验收；没有把静态检查说成实机防泄漏证明。

## 来源

- [Meta 官方 Muse 架构说明](https://research.meta.ai/blog/security-and-safety-for-ai-agents-our-approach-with-muse)：客户端连接云端 VM，并提供社交连接器；未公开完整的客户端域名白名单。
- [v2fly 的 Meta 分类](https://github.com/v2fly/domain-list-community/blob/master/data/meta)：专用域名及 Meta 共享分类；快照来源与许可见 [Muse 扩展说明](Muse扩展说明.md)和 rules/SOURCE-LICENSE。
- [Siri 扩展说明](new-meta-siri说明.md)：上游模板来源和 Siri 域名依据。
