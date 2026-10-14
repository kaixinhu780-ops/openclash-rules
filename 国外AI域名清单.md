# 国外 AI 域名清单

核对日期：2026-10-14。以下条目包括 55 条「🤖 国外AI」域名条件与 4 条「🧩 Muse」域名条件，本次整理新增的 43 条域名条件已在其中。`DOMAIN-SUFFIX` 覆盖根域名及任意层级子域名；`DOMAIN` 仅匹配列出的精确主机名。不是所有域名都代表独立 AI 产品。

ChatGPT、Claude、Gemini（包括 NotebookLM、AI Studio）继续使用各自独立分组，不在本表中。Muse 已改为独立分组。

| 匹配类型 | 域名 |
|---|---|
| `DOMAIN-SUFFIX` | `perplexity.ai` |
| `DOMAIN-SUFFIX` | `pplx.ai` |
| `DOMAIN-SUFFIX` | `pplx-res.cloudinary.com` |
| `DOMAIN-SUFFIX` | `grok.com` |
| `DOMAIN-SUFFIX` | `x.ai` |
| `DOMAIN-SUFFIX` | `poe.com` |
| `DOMAIN-SUFFIX` | `cursor.com` |
| `DOMAIN-SUFFIX` | `cursor.sh` |
| `DOMAIN-SUFFIX` | `cursorapi.com` |
| `DOMAIN-SUFFIX` | `windsurf.com` |
| `DOMAIN-SUFFIX` | `codeium.com` |
| `DOMAIN` | `copilot.microsoft.com` |
| `DOMAIN` | `sydney.bing.com` |
| `DOMAIN` | `edgeservices.bing.com` |
| `DOMAIN-SUFFIX` | `githubcopilot.com` |
| `DOMAIN` | `copilot-proxy.githubusercontent.com` |
| `DOMAIN-SUFFIX` | `llama.com` |
| `DOMAIN-SUFFIX` | `pi.ai` |
| `DOMAIN-SUFFIX` | `inflection.ai` |
| `DOMAIN-SUFFIX` | `grok.x.com` |
| `DOMAIN-SUFFIX` | `grokbot.com` |
| `DOMAIN-SUFFIX` | `dot.com` |
| `DOMAIN-SUFFIX` | `cursor-cdn.com` |
| `DOMAIN-SUFFIX` | `cursorvm.com` |
| `DOMAIN-SUFFIX` | `perplexity.com` |
| `DOMAIN` | `ppl-ai-file-upload.s3.amazonaws.com` |
| `DOMAIN-SUFFIX` | `groq.com` |
| `DOMAIN-SUFFIX` | `manus.im` |
| `DOMAIN-SUFFIX` | `manuscdn.com` |
| `DOMAIN-SUFFIX` | `huggingface.co` |
| `DOMAIN-SUFFIX` | `hf.co` |
| `DOMAIN-SUFFIX` | `hf.space` |
| `DOMAIN-SUFFIX` | `elevenlabs.io` |
| `DOMAIN-SUFFIX` | `elevenlabs.com` |
| `DOMAIN-SUFFIX` | `mistral.ai` |
| `DOMAIN-SUFFIX` | `cohere.ai` |
| `DOMAIN-SUFFIX` | `cohere.com` |
| `DOMAIN-SUFFIX` | `openrouter.ai` |
| `DOMAIN-SUFFIX` | `arena.ai` |
| `DOMAIN-SUFFIX` | `devin.ai` |
| `DOMAIN-SUFFIX` | `deepwiki.com` |
| `DOMAIN-SUFFIX` | `deepwiki.org` |
| `DOMAIN-SUFFIX` | `coderabbit.ai` |
| `DOMAIN-SUFFIX` | `midjourney.com` |
| `DOMAIN-SUFFIX` | `novelai.net` |
| `DOMAIN-SUFFIX` | `jasper.ai` |
| `DOMAIN-SUFFIX` | `clipdrop.co` |
| `DOMAIN-SUFFIX` | `openart.ai` |
| `DOMAIN-SUFFIX` | `lovart.ai` |
| `DOMAIN-SUFFIX` | `chutes.ai` |
| `DOMAIN-SUFFIX` | `copilot.com` |
| `DOMAIN-SUFFIX` | `copilot.cloud.microsoft` |
| `DOMAIN-SUFFIX` | `copilot-stg.com` |
| `DOMAIN-SUFFIX` | `kiro.dev` |
| `DOMAIN` | `coderabbit.gallery.vsassets.io` |

## Muse 独立分组

| 匹配类型 | 域名 |
|---|---|
| `DOMAIN-SUFFIX` | `muse.ai` |
| `DOMAIN-SUFFIX` | `meta.ai` |
| `DOMAIN-SUFFIX` | `metaaivm.com` |
| `DOMAIN` | `auth.meta.com` |

上述四项归「🧩 Muse」，默认手动选择，可独立选节点；`llama.com` 仍归国外 AI。共享 Meta AI/登录端点也可能服务于其他 Meta 功能。

## 服务与范围

新增 Muse / Meta AI、Pi / Inflection、Grok Bot 所用的 Cursor 资源与云电脑、Groq、Manus、Hugging Face、ElevenLabs、Mistral、Cohere、OpenRouter、Arena、Devin、DeepWiki、CodeRabbit、Midjourney、NovelAI、Jasper、Clipdrop、OpenArt、Lovart、Chutes、Kiro，并补充 Perplexity、Copilot。

- Muse 的 `muse.ai` 已覆盖 `auth.muse.ai`、`platform.muse.ai` 等子域；Meta 登录使用精确的 `auth.meta.com`。整个 `meta.com`、`facebook.com`、`fbcdn.net` 没有从社交组移到 AI 组。
- Pi 的 `pi.ai` 和 `inflection.ai` 已覆盖它们的 API、帮助中心、开发者页面等子域名。没有引入名称相近的第三方代用 API 服务。
- Grok 的 `grok.com`、`x.ai` 已覆盖它们的 API 和静态资源子域；新增 `grok.x.com` 优先于 X 通用规则。Grok Bot 的已确认入口与 Cursor 资源、云电脑也归 AI；整个 `x.com` 仍走 X/Twitter 分组。
- `cursorvm.com` 后缀规则覆盖嵌套主机，例如 `computer.cluster.cursorvm.com`；不需要枚举每台机器动态生成的主机名。
- Perplexity 的 S3 上传域名、CodeRabbit 的 VS Assets 域名采用精确匹配，没有把整个 AWS、Azure、Cloudflare、Auth0、Clerk 或 WorkOS 改为 AI 流量。
- Muse 经 Facebook/Instagram/WhatsApp 登录或调用，Grok 经 X 使用时，部分共享链路仍属于社交组。需要保持登录出口一致时，让对应社交组与 Muse/国外 AI 选择同一节点；本模板默认都跟随手动选择。

网页/App、API、CDN 的域名可能变动；云端 Agent 访问第三方网站的流量也不等同于你软路由上的本地 AI 请求。本清单不保证枚举所有未来域名或运行时目的地址。

## 依据

- [Muse 主站](https://muse.ai/)与 [Meta 的 Muse 介绍](https://ai.meta.com/muse)：产品与主站；[Meta 登录入口](https://auth.meta.com/)：已观察的登录跳转。
- [Pi 官方帮助中心](https://help.pi.ai/en/articles/13147185-how-is-my-data-used-and-how-can-i-control-my-privacy-and-tracking)、[Pi 隐私页面](https://meetings.pi.ai/privacy)：Pi 与 Inflection 服务域名。
- [Grok Bot 官方网络文档](https://docs.x.ai/grok-bot/proxies)：Cursor API、资源和嵌套云电脑域名；[Grok Bot 官方入口](https://x.ai/bot)、[grokbot.com](https://grokbot.com/)与 [dot.com](https://dot.com/)：已观察的官网重定向。
- [v2fly 海外 AI 分类维护源](https://github.com/v2fly/domain-list-community/blob/master/data/category-ai-%21cn)：其他服务域名依据。另核对 [Meta](https://github.com/v2fly/domain-list-community/blob/master/data/meta)、[xAI](https://github.com/v2fly/domain-list-community/blob/master/data/xai)、[Cursor](https://github.com/v2fly/domain-list-community/blob/master/data/cursor)、[Perplexity](https://github.com/v2fly/domain-list-community/blob/master/data/perplexity)、[Manus](https://github.com/v2fly/domain-list-community/blob/master/data/manus)、[Hugging Face](https://github.com/v2fly/domain-list-community/blob/master/data/huggingface)、[ElevenLabs](https://github.com/v2fly/domain-list-community/blob/master/data/elevenlabs)的维护源，快照保存在 validation/ai-source-snapshots。

本次实际转换、100 个代表性域名命中、分组引用和 Mihomo 配置检查通过；尚未在真实账户、节点、Muse/Pi/Grok Bot App 或软路由中验证功能。
