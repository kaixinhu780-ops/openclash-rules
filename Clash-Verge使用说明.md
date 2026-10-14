# Clash Verge / Clash Verge Rev 分流模板使用说明

本模板适配 **Clash Verge** 及 **Clash Verge Rev**（支持 Mihomo / Meta 内核），已与 OpenClash 规则完全同步：

- ✅ **策略组已置顶**：`👆 手动选择` 与 `⚡ 自动选择` 位于最顶端
- ✅ **国外社交整合**：合并了 Telegram、Instagram、WhatsApp、Facebook、Discord、Reddit 等
- ✅ **国外流媒体整合**：合并了 Disney+、HBO-Max、PrimeVideo、Twitch 等
- ✅ **香港节点手动选**：`🇭🇰 香港节点` 为手动选择（select），其余地区为自动测速（url-test）
- ✅ **广告拦截后置**：`🛡️ 广告拦截` 放在 `🐟 漏网之鱼` 后面
- ✅ **自动过滤无效节点**：自动过滤「剩余流量/到期时间/官网」等通知类节点

---

## 推荐用法：使用「配置扩展 (Merge)」无缝套用机场订阅

使用 Merge 扩展的好处是：**不管你的机场怎么更新节点，分流规则和策略组永远生效，不需要每次都重新转换订阅！**

### 操作步骤：

1. **打开 Clash Verge / Clash Verge Rev**
2. 点击左侧 **「订阅」**（或「配置」Profiles）
3. 找到你的机场订阅卡片，**右键** 点击它，选择 **「扩展配置」**（部分版本为「编辑规则扩展」或「Merge」）
4. 在弹出的文本编辑器中，将 [clash-verge-template.yaml](clash-verge-template.yaml) 的 **完整内容复制并粘贴进去**
5. 点击右上角 **「保存」**
6. 回到 Clash Verge 主界面，重新选中该订阅或者点击右侧刷新，即可在「代理」面板中看到精美的分组和分流！

---

## 备用用法：作为独立本地配置使用

如果你想新建一个独立的本地配置：

1. 在 Clash Verge 的「订阅」界面，点击右上角 **「新建」** -> 类型选择 **「Local (本地)」**
2. 将 `clash-verge-template.yaml` 的内容复制进去
3. 在 `proxy-providers` 节点部分填入你的机场订阅链接
4. 保存并右键启用即可。

---

## 文件直达链接

- GitHub 源码：[clash-verge-template.yaml](https://raw.githubusercontent.com/kaixinhu780-ops/openclash-rules/main/clash-verge-template.yaml)
- jsDelivr 镜像加速：`https://fastly.jsdelivr.net/gh/kaixinhu780-ops/openclash-rules@main/clash-verge-template.yaml`
