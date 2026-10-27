# test1 DNS 与默认出口

此变更修复国外/兜底默认直连和测漏域名缺口，并为转换产物提供独立DNS基础配置。它不自动修改任何路由器。

## 使用入口

在线转换的远程配置：

```text
https://raw.githubusercontent.com/kaixinhu780-ops/openclash-rules/main/test1-merged-groups.ini
```

INI 的 `clash_rule_base` 引用本仓库 `test1-dns-base.yaml`。转换器必须允许自定义远程基础配置并能下载该文件；不要把基础YAML当作独立节点订阅。使用自己的节点订阅，公开文件不含节点、账号或凭据。

## 修复的具体行为

- “🌍 国外域名”和“🐟 漏网之鱼”首项改为“🚀 手动选择”。全局直连仍可手动选，但不再是这两个组的新配置默认值；客户端保存的历史选择可能继续有效。
- browserleaks.com、browserleaks.org、browserleaks.net、dnsleaktest.com、ipleak.net 的后缀规则先于通用直连/IP/兜底规则。包含随机探测子域，避免只代理网页主域。
- 常规DNS使用Cloudflare/Google的HTTPS端点，明确经“🚀 手动选择”连接，不使用DHCP、system、上级路由或明文备用DNS。代理不可用时不以运营商DNS兜底。
- 节点域名通过独立的阿里DoH引导，避免必须先建代理才能解析代理节点的循环。
- 直连目标保留阿里加密DNS以支持国内CDN；这不是“所有域名都境外解析”的方案。测漏后缀另有nameserver-policy并启用direct-nameserver-follow-policy。
- 不改变国内直连规则、现有地区筛选器、节点、订阅、Claude/Muse出口逻辑。

## 必须核对的生效边界

分流INI决定目标策略，基础YAML决定核心DNS上游，OpenClash自身的DNS覆写则可能再次覆盖它们。不能只看远端模板更新就断言设备DNS已经改变。

查看转换后的YAML：`dns.nameserver`应含`https://1.1.1.1/dns-query#🚀 手动选择`和`https://8.8.8.8/dns-query#🚀 手动选择`；`proxy-server-nameserver`应独立存在；常规上游不应被覆写成dhcp、system或192.168.1.1。用户若启用其他覆写，应自行核对最终结果，本变更不安装覆写脚本或自动部署。

客户端历史选择、应用自带DoH、LAN DNS劫持、Mac/手机物理接口IPv6和旁路网关拓扑，仍属于运行环境。`dns.ipv6=false`只控制核心AAAA回答，不能关闭光猫/网卡IPv6或证明其被接管。无需为此直接关闭全网IPv6。

## 检查与回退

本轮使用官方subconverter v0.9.0本地转换，验证60组/256条规则、DNS保留及优先级；转换后的DNS/全部分组最小配置通过本机Mihomo v1.19.29核心校验。未重新验证所有远程GeoSite/IP数据库。上述检查，不将此前已回滚的路由器候选测试当作当前设备验收。没有路由器写入；没有承诺已完成用户设备的零泄漏验证。

需要回退时恢复此前INI及基础文件的Git版本；路由器是否加载由用户决定。DNS与规则的核心语义参考：[Mihomo DNS 文档](https://wiki.metacubex.one/config/dns/)。
