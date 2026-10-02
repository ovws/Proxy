# Egern 自定义规则集

此目录存放 Egern 原生规则条件。策略名、节点、订阅、DNS 和证书不属于规则集，必须在私人主配置中维护。

| 文件 | 用途 |
| --- | --- |
| LAN.yaml | 局域网及系统连接检测 |
| DomesticAI.yaml | 国内 AI 服务 |
| AI.yaml | AI 服务补充 |
| Developer.yaml | 开发服务补充 |
| Work.yaml | 工作协作服务补充 |
| Broker.yaml | 券商与投资服务 |
| Telegram.yaml | Telegram 服务补充 |
| X.yaml | X / Twitter 服务补充 |
| Domestic.yaml | 国内常用服务补充 |

## 维护

直接修改相应 YAML 中的 `domain_set`、`domain_suffix_set`、`ip_cidr_set` 等原生集合。域名只填写公开服务域名，CIDR 只填写公开服务网段或标准局域网网段。不要放入私人服务器地址、节点密钥、订阅链接、账户标识或 CA 证书。

规则集内部条件按 OR 匹配，集合不带策略。主配置的规则引用顺序决定优先级：国内 AI 需在通用 AI 前，AI 需在 Google 前，流媒体需在 Google 前，国内规则位于其他服务之后。`no_resolve: true` 保留 IP 条件的无解析匹配。

主配置引用 `https://raw.githubusercontent.com/ovws/Proxy/master/Rule/Egern/Custom/<文件名>`，设置 `update_interval: 86400` 可每日检查更新。DNS 引导、管理工具直连和最终兜底应保留在主配置，不依赖这些远程规则。

仅做同策略、同优先级块内的去重。不要跨策略合并看似重复的条件，否则会改变首次匹配行为。
