# Muse / Meta 扩展说明

更新日期：2026-10-15。按用户要求，小火箭与 OpenClash 均将 Meta 共享服务域名归入“🧩 Muse”。

## 覆盖范围与影响

除原有 muse.ai、meta.ai、metaaivm.com、auth.meta.com 外，Llama 也改归 Muse，并引入 555 条去重域名条件的 Meta 分类快照。其中包含 meta.com、atmeta.com，以及维护源收录的 Facebook、Facebook 开发者平台、Instagram、Messenger、Threads、WhatsApp、Oculus/Quest 相关域名。

这些是维护者的广义分流分类，不是 Meta 官方提供的 Muse 专用网络清单，也不代表已逐一核验所有域名的实际所有权或用途。无法保证覆盖运行时所有第三方连接，云端 Agent 对第三方服务的访问也不等同于本地设备的连接。

**命中共享域名的 Facebook、Instagram、WhatsApp 等请求会改用 Muse 出口，优先于原社交分组。** 原社交组保留供其他未被共享域名集命中的规则使用；若想恢复社交组控制，需要撤掉这条共享规则，或将更窄的社交例外放在它前面。

广告拦截在共享扩展规则之前；不会为了覆盖 Meta 而放行所有广告或追踪连接。没有使用 DOMAIN-KEYWORD,meta、整个 Cloudflare/AWS/Azure 域名等宽泛条件，也未把整个 Meta ASN/IP 段强制归 Muse。

## 来源与维护

维护源：[v2fly/domain-list-community 的 meta 分类](https://github.com/v2fly/domain-list-community/blob/master/data/meta)，递归展开 facebook、facebook-dev、instagram、messenger、oculus、threads、whatsapp。普通条目转换为 DOMAIN-SUFFIX，full 条目转换为 DOMAIN。

发布文件包含 Shadowrocket 的 rules/MuseMeta.list 和 OpenClash 使用的 rules/MuseMeta.yaml（各仓库发布适合自己的格式）。源许可保存在 rules/SOURCE-LICENSE；域名集使用固定快照，后续需要重新核验并更新，不会自动跟随维护源新增。

## 使用与验证

更新对应在线配置并使用配置；小火箭首次使用时确认新增远程规则下载成功，OpenClash 需重新转换/更新订阅。Muse 固定选择可用节点，再验证登录、对话、附件及共享社交功能。域名命中检查和内核配置校验不能代替手机、软路由及账号的实际使用验收。
