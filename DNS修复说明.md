# OpenClash DNS 修复（2026-10-15）

用户反馈 BrowserLeaks DNS 列表出现中国地区解析器。仅有旗帜无法识别具体解析器或确认实际泄漏路径；本次先修复发布配置中可确认的问题，再要求路由器实测。

## 已修正的配置

- 原底稿的 default-nameserver、proxy-server-nameserver 使用明文 223.5.5.5 / 119.29.29.29；现在改为 IP 形式的 HTTPS DNS，并明确 DIRECT 引导。只有节点服务器域名与必要的 DNS 引导使用此通道。
- nameserver 和 direct-nameserver 都改用 `https://1.1.1.1/dns-query#👆 手动选择`、`https://8.8.8.8/dns-query#👆 手动选择`，明确指定代理。只设置 respect-rules 或海外解析器地址不等于强制代理。
- 移除普通域名查询使用国内解析器的 nameserver-policy，以及没有配置 fallback 的 fallback-filter。使用 IP 形式的海外 DoH，减少解析 DNS 服务器域名的引导依赖。
- respect-rules 设为 false：每个 DNS 上游已用后缀明确选择代理或 DIRECT，不再依赖业务路由推断 DNS 连接出口。不启用 HTTP/3 优先。
- 模板改引用 `v1.4-dns` 标签的 DNS 底稿，避免 CDN 继续返回 v1.3 内容。保持已有业务分流和策略组设置。

Mihomo 文档允许 default-nameserver 使用 IP 形式的加密 DNS；此前“必须使用明文 IP”的说法不正确。此版本不添加拒绝全部 53 端口的规则，因为若 DNS 劫持未生效，会直接破坏客户端解析。DNS 劫持必须在路由器侧落实。

## 使用与代价

1. 在 OpenClash 更新原模板订阅，重新生成配置并重新加载内核。主模板地址不变；不要继续固定使用旧模板或旧 DNS 底稿。
2. 检查最终运行 YAML：nameserver 和 direct-nameserver 必须含 `#👆 手动选择`；default-nameserver 和 proxy-server-nameserver 必须为 HTTPS；没有额外的 system、WAN/运营商或明文 DNS。若 OpenClash DNS 覆写启用，必须同步此设置，否则会覆盖转换模板。
3. 手动选择组必须选可用的代理节点。确认 LAN 设备的 DNS 指向软路由，OpenClash DNS 接管已启用，Dnsmasq 没有在并行向 ISP/WAN DNS 查询。
4. 对没有配置 IPv6 接管的路由器，不要向 LAN 下发可绕过路由器的 IPv6 DNS。YAML 中 ipv6=false 不能关闭路由器的 RA/DHCPv6。浏览器/系统自带 DoH、其他 VPN 的解析路径也需要单独检查。
5. 重新运行 BrowserLeaks 扩展测试，记录实际解析器运营商和地址类型；不同城市或国家标签不能单独证明泄漏。若仍出现非预期国内运营商解析器，需要结合最终运行配置和出口 TCP/UDP 53、IPv6 抓包判断。

国内网站的业务连接仍可直连，但普通域名的查询统一经代理访问海外 DNS，国内 CDN 调度可能变慢。代理断开时依赖该解析通道的请求可能失败，这是严格查询模式的可用性取舍。节点引导使用的国内加密解析器仍可看到节点域名；解析器及代理服务各自的日志行为不受客户端配置控制。

## 本次验证范围

- 实际 subconverter 转换，确认 DNS 字段与底稿一致、30 个策略组及业务路由规则未改变。
- 官方 Mihomo v1.19.32 的配置检查通过。
- 本地回环测试使用拒绝 CONNECT 的 HTTP 代理：普通 TXT 查询和 DIRECT 出口主机解析均向选定代理请求连接海外 DoH；代理拒绝连接时 DNS 查询返回 SERVFAIL。该测试证明本地配置的代理分派和错误处理，不证明用户路由器已接管所有 DNS。
- 尚未访问用户路由器，尚无真实节点、BrowserLeaks 或路由器出口抓包验收，不能声称实机泄漏已经排除。

依据：[Mihomo DNS 文档](https://wiki.metacubex.one/config/dns/)及 [BrowserLeaks DNS 测试说明](https://browserleaks.com/dns)。
