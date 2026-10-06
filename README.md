# hackathon-open-source-hub

**开源黑客松项目索引**｜整合 fork 自 GitHub 的热门开源黑客松脚手架、赛事托管平台与评测底座。

> **用途**：打黑客松/算法赛时，从这里直接拿现成的起步模板、赛制复现底座和评测工具，不必每次从零搭。
> **主仓库定位**：本仓库只做索引与说明；实际代码在各 fork 仓库中，保持与上游同步。

---

## 一、数据来源 · 计算方法 · 口径限制

**数据来源**
- 星数与推送时间：GitHub REST API `api.github.com`（`stargazers_count` / `pushed_at`），交叉校验 `repos.ecosyste.ms`。
- 本仓库 fork 列表：`gh repo list sjkncs --fork` 与 `gh api repos/sjkncs/<name>` 实测返回。

**计算方法**
- 按 `topic:hackathon`、`hackathon in:name,description`、`topic:hackathon+topic:ai|llm|agents` 等检索式取候选，`sort=stars`。
- 活跃度一律按 **`pushed_at`（最后代码推送）** 判断，**不按 `updated_at`**——后者只要有人点 star 就会变，会严重高估活跃度。
- 星数与推送日为 **2026-10-06 快照**，非估算值。**同日复检已发现漂移**：复检时 22 行表格中有 14 行的星数或推送日与快照不同（星数变动 1–7 颗属正常；`hackathon-starter`、`EvalAI`、`OpenML`、`codabench`、`lighteval`、`ms-swift` 当日有新推送）。**引用本表数字时请注明快照时间，不要当作当前值。**
- **fork 新鲜度不能用 `GET /compare/{base}...{head}` 判断**。对 fork 仓库调用 `compare/main...main` 时，GitHub 会把 base 解析为**该 fork 自己的 parent 分支**，等于拿同仓库镜像自比，因此**恒返回 `status=identical`**——即使 fork 已落后上游。正确做法是直接比对 `repos/{fork}/git/ref/heads/{branch}` 与 `repos/{upstream}/git/ref/heads/{branch}` 的 SHA。

**口径限制（本索引不能用来做什么）**
- **不能**用来判断项目质量或"哪个更容易获奖"。星数只反映关注度。
- **不能**把本索引当作黑客松**获奖作品**清单。真正收录获奖作品的是 `awesome-hackathon-projects`，本仓库其余部分多为**基础设施**（脚手架 / 平台 / 评测）。
- 星数快照有时效性；许可协议以各上游仓库 `LICENSE` 文件为准，本表仅供参考。
- **不能**假定 fork 是最新版。**活跃上游的 fork 会在数小时内过期**：实测 `unsloth` 的 fork 在创建后约 90 分钟即落后上游一个提交。

---

## 二、筛选方法论：`topic:hackathon` 的流量污染与剔除记录

直接按 `topic:hackathon&sort=stars` 取 Top 15（该 topic 共 15,831 个仓库），**只有 2 个是真正意义上的黑客松项目/产出**。以下类型已人工剔除：

| 剔除项 | 星数 | 剔除理由 |
|---|---|---|
| `ankit0183/Wifi-Hacking` | 2,731 | **hacking = 渗透/破解，不是 hackathon** |
| `noob-hackers/hacklock` | 2,479 | 同上（Android 图案锁钓鱼演示） |
| `hhhrrrttt222111/Ethical-Hacking-Tools` | 2,181 | 同上，且 2023 年已停更 |
| `kriasoft/graphql-starter-kit` | 3,968 | 与黑客松无关，且停更约 2 年 |
| `manishbisht/Competitive-Programming` | 1,768 | 算法竞赛题解，且 2023 停更 |
| `Olivr/free-domain` | 808 | 免费域名领取，非黑客松 |

**可直接复用的筛法**：`topic:hackathon-winner`、`topic:hackathon-project`，或 `created:>2025-01-01 topic:hackathon`。单纯用 `topic:hackathon&sort=stars` 会被脚手架与安全工具吃掉头部。

---

## 三、A 类 · 黑客松脚手架与起步模板

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [hackathon-starter](https://github.com/sjkncs/hackathon-starter) | sahat/hackathon-starter | **35,253** | 2026-09-29 | MIT | Node.js 脚手架，通用起步模板事实标准，**头部唯一仍活跃者** |
| [nano-banana-hackathon-kit](https://github.com/sjkncs/nano-banana-hackathon-kit) | google-gemini/nano-banana-hackathon-kit | 1,028 | 2025-09-08 | Apache-2.0 | Nano Banana Hackathon 官方 starter kit |
| [laravel-hackathon-starter](https://github.com/sjkncs/laravel-hackathon-starter) | unicodeveloper/laravel-hackathon-starter | 1,685 | 2023-12-14 | MIT | Laravel 版 MVP 脚手架（**已停更**） |
| [mlh-hackathon-nodejs-starter](https://github.com/sjkncs/mlh-hackathon-nodejs-starter) | MLH/mlh-hackathon-nodejs-starter | 702 | 2022-02-11 | MIT | MLH 官方 Node 脚手架（已停更） |
| [django-hackathon-starter](https://github.com/sjkncs/django-hackathon-starter) | DrkSephy/django-hackathon-starter | 1,623 | 2020-03-05 | **未声明许可** | Django 版脚手架（已停更 6 年）——**无 LICENSE，慎用**，见第十节 |
| [RAG_Hack](https://github.com/sjkncs/RAG_Hack) | microsoft/RAG_Hack | 523 | 2024-10-11 | MIT | 微软 Hack Together: RAG Hack 官方仓库 |

---

## 四、B 类 · 黑客松项目与获奖作品聚合

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [awesome-hackathon-projects](https://github.com/sjkncs/awesome-hackathon-projects) | Olanetsoft/awesome-hackathon-projects | 1,864 | 2025-05-20 | MIT | **唯一纯正的黑客松项目精选清单**，找选题灵感首选 |

---

## 五、C 类 · 赛事托管平台与评测底座（可自建、可复现赛制）

**真正"可自部署、带注册与排行榜"的竞赛平台只有这一小圈：**

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [EvalAI](https://github.com/sjkncs/EvalAI) | Cloud-CV/EvalAI | **2,044** | 2026-09-20 | BSD 3-Clause | 开源 AI 竞赛/榜单托管（Django + Angular），支持注册、组队、代码评测 |
| [OpenML](https://github.com/sjkncs/OpenML) | openml/OpenML | 751 | 2026-08-06 | BSD-3-Clause | 开放 ML 平台：数据集/任务/运行/排行榜，带账号体系 |
| [codalab-competitions](https://github.com/sjkncs/codalab-competitions) | codalab/codalab-competitions | 539 | 2026-09-07 | Apache-2.0 | 经典 CodaLab Competitions，Docker 提交 + 排行榜 |
| [codabench](https://github.com/sjkncs/codabench) | codalab/codabench | 178 | 2026-09-29 | Apache-2.0 | CodaLab 继任者，**同类中最活跃**，推荐作为自建首选 |

**竞赛本身作为基准的"元用法"：**

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [mle-bench](https://github.com/sjkncs/mle-bench) | openai/mle-bench | 1,764 | 2026-04-24 | MIT | 直接把 Kaggle 竞赛当基准，评测 AI agent 的 MLE 能力——**最贴近"AI 自动打比赛"** |

**明确"不开源 / 易混淆"，避免踩坑：**

| 对象 | 状态 |
|---|---|
| **Kaggle** | 平台本体**闭源**，官方只开源 CLI 与仿真环境 |
| **阿里天池 / DataFountain / Zindi / HackerEarth** | **闭源商业平台**，未发现平台本体开源仓库 |
| **AIcrowd** | 本体**不开源**，GitHub 组织下全是 starter-kit 与客户端模板 |
| `thu-ml/tianshou` | 约 11,010★、MIT，但它是**深度强化学习算法库**，不是竞赛平台——"tianshou（天授）"与"天池 Tianchi"是两个东西 |

---

## 六、C-2 类 · 评测框架与公开榜单（想自建 leaderboard 用这些）

竞赛平台解决"收作品、排行、评测"，榜单框架解决"怎么评"。两类配合使用：

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [evals](https://github.com/sjkncs/evals) | openai/evals | **19,561** | 2026-04-14 | MIT | LLM 评测框架 + 开源基准注册表 |
| [lm-evaluation-harness](https://github.com/sjkncs/lm-evaluation-harness) | EleutherAI/lm-evaluation-harness | **14,139** | 2026-09-14 | MIT | few-shot LLM 评测框架，**多个公开榜单的后端** |
| [opencompass](https://github.com/sjkncs/opencompass) | open-compass/opencompass | 7,493 | 2026-09-28 | Apache-2.0 | 中文/多模型 LLM 评测平台，CompassHub 公开榜单 |
| [evalscope](https://github.com/sjkncs/evalscope) | modelscope/evalscope | 3,504 | 2026-09-30 | Apache-2.0 | **魔搭自家评测框架**（LLM/VLM/AIGC 评测 + 性能压测） |
| [lighteval](https://github.com/sjkncs/lighteval) | huggingface/lighteval | 2,552 | 2026-09-30 | MIT | HF 评测工具包，Open LLM Leaderboard 后端 |

> **打魔搭系赛事的推荐组合**：`ms-swift`（微调）+ `evalscope`（评测）+ `ms-agent`（编排）——赛方自家工具链，兼容性风险最低。

---

## 七、C-3 类 · AI / LLM / Agent 类项目与赛事作品

| 仓库（fork） | 上游 | 星数 | 最后推送 | 许可 | 定位 |
|---|---|---|---|---|---|
| [ChatDev](https://github.com/sjkncs/ChatDev) | OpenBMB/ChatDev | **34,454** | 2026-07-24 | Apache-2.0 | LLM 多智能体协作完成软件开发，黑客松常客 |
| [lerobot](https://github.com/sjkncs/lerobot) | huggingface/lerobot | **27,964** | 2026-10-06 | Apache-2.0 | 端到端机器人学习，**LeRobot Worldwide / AMD DevMaster 黑客松的底座**（具身智能赛事首选） |
| [SWE-agent](https://github.com/sjkncs/SWE-agent) | SWE-agent/SWE-agent | **20,496** | 2026-10-06 | MIT | 拿 GitHub issue 自动修复代码（NeurIPS 2024），官方描述含"competitive coding challenges" |
| [ms-swift](https://github.com/sjkncs/ms-swift) | modelscope/ms-swift | **15,784** | 2026-10-05 | Apache-2.0 | 600+ LLM / 300+ MLLM 的 CPT/SFT/DPO/GRPO 微调框架 |
| [unsloth](https://github.com/sjkncs/unsloth) | unslothai/unsloth | **77,271** | 2026-10-06 | Apache-2.0 | 单卡微调加速，黑客松"48 小时把模型练出来"的刚需工具 |

> 说明：`unsloth` 属**跨赛事的通用微调工具**，不以黑客松为主题，但它决定了你能不能在一个周末内把模型调出来，因此收录。

**故意未收录的大体量通用仓库（可自行按需 fork，理由是体积而非质量问题）：**

| 上游 | 星数 | 体积 | 未收录理由 |
|---|---|---|---|
| openai/openai-cookbook | 76,367 | **954 MB** | 教程集合，与黑客松无直接关系，且体量过大 |
| huggingface/transformers | 167,000 | **515 MB** | 通用模型定义框架，不属于黑客松/赛事基建 |
| vllm-project/vllm | 93,274 | **304 MB** | 推理引擎，属部署层，非赛事基建 |
| microsoft/autogen | 61,273 | 145 MB | 通用多 agent 框架；许可为 **CC-BY-4.0**（非软件许可，商用需谨慎） |

---

## 八、fork 进度

**本索引覆盖的 fork 已全部落地**（A 类 7 + B 类 1 + C 类 4 + C-2 类 5 + C-3 类 5 + 平台 4 = 26 个）。fork 创建过程中曾两次撞上 GitHub 的**内容创建二级限速**（与 5,000 次/小时的 API 配额无关，且**不返回 `Retry-After`**，只能等待冷却窗口），均已通过退避重试补齐。

### fork 新鲜度实测（2026-10-06 复检，直接 SHA 比对）

| fork | 状态 |
|---|---|
| unsloth | **落后上游**（fork 创建后约 90 分钟即被上游超越） |
| lerobot | **落后上游** |
| ms-swift | **落后上游** |
| 其余 13 个受检仓库 | 与上游同步 |

> 本节最初曾用 `GET /compare/main...main` 审计并得出"26/26 全部 identical、无偏离"的结论，**该结论是错的**——原因是 `compare` 对 fork 的 base 解析语义（详见第一节）。已改为直接 SHA 比对并更正。**这不是抓取失败，而是一个会随上游提交持续发生的正常现象**：fork 是创建时刻的快照。

**维护提示**
- fork 仓库的星数**不继承上游，恒显示 0**。本 README 各表记录的是**上游星数**，判断活跃度请直接看 fork 页面的提交时间或上游 `pushed_at`。
- 要同步上游最新提交，在 **GitHub 网页**的 fork 页面点 `Sync fork` 即可。**注意**：本机 `git` 到 `github.com:443` 不通（实测超时约 21 秒），命令行 `git pull upstream` 会失败；本 README 亦因此改走 Contents API 写入而非 `git push`。

---

## 九、配套赛事入口（截至 2026-10-06 实测）

| 赛事 | 报名入口 | 状态 | 硬截止 |
|---|---|---|---|
| 天猫 AI 黑客松·高校挑战赛 | 淘宝 App 搜"天猫AI黑客松" | **即将截止** | **2026-10-07** |
| 怀柔科学城 AI for Science · OPC 创新挑战赛 | "怀柔科创"小程序 / 赛事官网 | 可报名（截止日存在 10-10 与 11-10 两种口径） | **按 10-10 假设** |
| 2026 上海开源软件应用创新大赛 | oschina.net/os2026 | 可报名（**先交基础信息即锁席位**） | **2026-10-11** |
| 蚂蚁灵波具身大模型挑战赛 | ModelScope / 阿里云天池 | 可报名（报名后需进官方钉钉群） | 2026-10-26 |
| 支付宝｜智能体涌现奖比赛 | ModelScope /events/375 | 可报名 | 2026-11-10 |

---

## 十、许可与致谢

本仓库为**索引仓库**，不复制上游代码。所有 fork 仓库均保留各自上游的 `LICENSE` 与版权声明：

### 许可分组（已逐个读取许可证正文核实，非依赖 GitHub 标签）

- **MIT（11）**：hackathon-starter、awesome-hackathon-projects、RAG_Hack、laravel-hackathon-starter、mlh-hackathon-nodejs-starter、SWE-bench、SWE-agent、lm-evaluation-harness、lighteval、mle-bench、evals
- **Apache-2.0（12）**：nano-banana-hackathon-kit、codabench、ms-agent、rse-grand-challenge、FastChat、ChatDev、lerobot、ms-swift、evalscope、opencompass、unsloth、codalab-competitions
- **BSD 3-Clause（2）**：OpenML、EvalAI
- **⚠️ 未声明任何许可（1）**：django-hackathon-starter。已实测**根目录无 `LICENSE`／`COPYING` 文件**，README 亦无许可声明。按著作权默认规则视为**保留全部权利**——与 MIT / Apache 完全不是一回事，**不要**当作可自由使用的代码。

### 关于 GitHub 的 `NOASSERTION` 标签（重要纠正）

GitHub API 对 **EvalAI、codalab-competitions、mle-bench、evals** 四个仓库返回 `NOASSERTION`，**这不等于"自定义许可"或"无许可"**。实测读取其许可证正文后确认，四者都是标准许可，只是 GitHub 的识别器未能匹配：

| 仓库 | GitHub 标签 | **实际许可（已读正文）** |
|---|---|---|
| EvalAI | NOASSERTION | **BSD 3-Clause**（第 3 条仅限制以其名义背书/推广，**无任何非商业限制**） |
| codalab-competitions | NOASSERTION | **Apache-2.0**（正文明确写 "released under the Apache License 2.0"） |
| mle-bench | NOASSERTION | **MIT**（Copyright (c) 2024 OpenAI） |
| evals | NOASSERTION | **MIT**（Copyright (c) 2023 OpenAI） |

**教训**：不要把 GitHub 的 `NOASSERTION` 直接当作法律结论转述——它只说明自动识别失败，必须读正文字段才能定性。本项目最初的 README 就犯了这个错，现已更正。

**EvalAI 与 codalab-competitions 的文件名分别为 `LICENSE` 与 `LICENSE.TXT`，且正文为短式引用**（后者仅 353 字节，正文指向 apache.org），这也是识别器失败的常见原因。

**使用 fork 前请自行确认上游许可证是否允许你的用途**（尤其是竞赛交付物与商业场景）。上游作者保留全部权利。

---

*索引生成时间：2026-10-06｜星数为 API 快照，会实时变动。*
