# 🧠 Awesome DeepSeek V4 — 关于下一代编程AI的一切

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DeepSeek V4](https://img.shields.io/badge/DeepSeek-V4-blue.svg)](https://github.com/deepseek-ai)
[![在Atlas Cloud上试用V3.2](https://img.shields.io/badge/试用V3.2-Atlas%20Cloud-green.svg)](https://www.atlascloud.ai?ref=JPM683)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**语言:** [English](README.md) | 中文 | [日本語](README_ja.md) | [한국어](README_ko.md)

---

> **⚠️ DeepSeek V4 尚未正式发布。本指南汇总了我们目前了解的所有信息，包括泄露信息、内部报告和官方暗示。信息可能随时变化。**

---

## 目录

- [什么是 DeepSeek V4？](#什么是-deepseek-v4)
- [当前状态与时间线](#当前状态与时间线)
- [预期功能深度解析](#预期功能深度解析)
  - [万亿参数规模](#万亿参数规模)
  - [Engram 记忆架构](#engram-记忆架构)
  - [100万+ Token 上下文窗口](#100万-token-上下文窗口)
  - [多模态能力](#多模态能力)
- [架构详解](#架构详解)
  - [混合专家模型 (MoE)](#混合专家模型-moe)
  - [高效推理](#高效推理)
- [编程能力](#编程能力)
  - [仓库级代码理解](#仓库级代码理解)
  - [多文件推理](#多文件推理)
  - [高级代码生成](#高级代码生成)
- [预期基准测试](#预期基准测试)
- [公告与延期时间线](#公告与延期时间线)
- [使用 Atlas Cloud 提前准备](#使用-atlas-cloud-提前准备)
- [Atlas Cloud API 快速上手](#atlas-cloud-api-快速上手)
  - [Python](#python)
  - [cURL](#curl)
  - [Node.js](#nodejs)
- [价格](#价格)
- [V3.2 与 V4 功能对比](#v32-与-v4-功能对比)
- [常见问题](#常见问题)
- [贡献](#贡献)

---

## 什么是 DeepSeek V4？

**DeepSeek V4** 是 [DeepSeek](https://www.deepseek.com/) 即将推出的下一代大型语言模型。DeepSeek 是一家中国AI实验室，凭借其开源权重模型在AI领域掀起了巨大波澜。在 DeepSeek V3 和 V3.2 取得成功的基础上，V4 模型预计将在AI能力上实现代际飞跃——尤其是在软件工程、代码理解和长上下文推理方面。

### 为什么如此受关注？

- **万亿参数规模** 通过混合专家模型实现极致效率
- **Engram 记忆** — 一种超越标准注意力机制的新型长上下文检索架构
- **100万+ Token 上下文** — 在单次提示中处理整个代码库
- **原生多模态** — 文本、代码和视觉在一个统一模型中
- **开源权重承诺** — DeepSeek 已暗示 V4 将延续其开源传统
- **泄露基准测试** 显示在编程任务上的性能可与 GPT-5 和 Claude 4 媲美甚至超越

### 关键特性一览

| 特性 | DeepSeek V4（预期） |
|------|-------------------|
| 总参数量 | ~1万亿 |
| 活跃参数量 | ~370亿/token |
| 架构 | 混合专家模型 (MoE) |
| 上下文窗口 | 100万+ tokens |
| 记忆系统 | Engram 记忆架构 |
| 模态 | 文本 + 代码 + 视觉 |
| 代码基准 (HumanEval) | ~90%（泄露） |
| SWE-bench Verified | 80%+（泄露） |
| 开源权重 | 预期（是） |

---

## 当前状态与时间线

> **最后更新：2026年3月12日**

🔴 **状态：尚未发布**

DeepSeek V4 已错过多个预期发布窗口。截至2026年3月，尚未确认正式发布日期。

**我们所了解的：**
- 据报道内部测试仍在进行中
- 多个发布窗口已过但无公告
- DeepSeek 团队在社交媒体上异常沉默
- 一些早期接触的研究人员暗示结果"令人印象深刻"
- 泄露的基准测试分数已在中文论坛上出现

**不要等待 — [立即在 Atlas Cloud 上使用 DeepSeek V3.2 开始构建](https://www.atlascloud.ai?ref=JPM683)，V4 发布后无缝升级。**

---

## 预期功能深度解析

### 万亿参数规模

DeepSeek V4 预计拥有约 **1万亿总参数**，使其成为有史以来最大的语言模型之一。然而，与为每个 token 激活所有参数的密集模型不同，V4 使用混合专家架构来保持可控的推理成本。

**为什么重要：**
- 更多参数 = 更大的知识容量
- 模型可以存储更多代码模式、算法和编程概念的"知识库"
- 万亿级模型展示了小模型中不存在的涌现能力
- 尽管规模巨大，MoE 使每 token 计算量与 370 亿密集模型相当

**技术细节：**
- 预计所有专家共 1T 总参数
- 每 token ~370 亿活跃参数（仅相关专家被激活）
- 这使 V4 拥有万亿参数模型的知识容量和 ~370 亿模型的推理速度
- 训练可能使用了数千块 GPU，历时数月

### Engram 记忆架构

DeepSeek V4 最令人期待的创新可能是 **Engram 记忆架构** — 一种超越标准 transformer 注意力机制的新型长上下文信息检索方法。

**什么是 Engram 记忆？**

传统 transformer 在处理很长的上下文时存在困难，因为注意力随序列长度呈二次方增长。Engram 记忆引入了一个辅助记忆系统：

1. **压缩** 长距离上下文为密集的"engram"表示
2. **索引** 这些表示以实现高效检索
3. **整合** 检索到的信息与模型的注意力机制无缝结合
4. **持久化** 贯穿整个生成过程，类似于一种"工作记忆"

**对开发者的意义：**
- 处理整个代码库而不会丢失远距离依赖
- 在100万+ token 中保持连贯理解
- 更好地回忆上下文早期的函数签名、类型定义和 API 模式
- 大型项目中更准确的跨文件推理

### 100万+ Token 上下文窗口

DeepSeek V4 预计支持超过 **100万 token** 的上下文窗口 — 足以容纳：

- ~75万字文本
- ~2.5万页文档
- 整个中等规模代码库（100+ 文件）
- 多本完整书籍
- 数千页 API 文档

**上下文窗口对比：**

| 模型 | 上下文窗口 |
|------|-----------|
| GPT-4（原版） | 8K / 32K |
| Claude 3 | 200K |
| Gemini 1.5 Pro | 1M |
| DeepSeek V3.2 | 128K |
| **DeepSeek V4（预期）** | **1M+** |
| Claude 4 | 500K |
| GPT-5 | 256K |

### 多模态能力

DeepSeek V4 预计原生支持多模态，处理 **文本、代码和视觉** 的统一架构。

**视觉能力（预期）：**
- 截图转代码生成
- UI/UX 分析和建议
- 图表和架构图理解
- 从截图中识别 Bug
- 设计系统理解

---

## 架构详解

### 混合专家模型 (MoE)

DeepSeek V4 延续了 V3 中建立的 MoE 传统，但规模更大。

**V4 中 MoE 的工作原理：**

```
输入 Token
    │
    ▼
┌─────────┐
│  路由器  │ ── 选择激活哪些专家
└─────────┘
    │
    ▼
┌─────────────────────────────┐
│  专家 1  │  专家 2  │  ...  │ ── 1T 总参数中仅 ~370 亿活跃
│  (活跃)  │  (活跃)  │       │
└─────────────────────────────┘
    │
    ▼
┌─────────┐
│  输出    │
└─────────┘
```

**关键架构决策：**
- **细粒度专家**：更多更小的专家实现更好的专业化
- **共享专家**：部分专家始终活跃，提供"通用知识"骨干
- **负载均衡**：高级路由确保专家间均匀利用
- **专家并行**：专家分布在多块 GPU 上实现高效推理

### 高效推理

尽管万亿参数规模，V4 被设计为可实际部署：

- 每 token **370 亿活跃参数** — 与运行 370 亿密集模型相当
- **推测解码** 支持更快生成
- **KV-cache 优化** 实现长上下文效率
- **量化友好** 架构（预期支持 FP8/INT4）
- **多头潜在注意力 (MLA)** — 延续 V3 以减少内存占用

---

## 编程能力

### 仓库级代码理解

DeepSeek V4 最受期待的功能之一是 **真正的仓库级代码理解**。当前模型可以理解单个文件或少量文件，V4 预计能将整个代码库作为连贯系统来理解。

**这意味着：**
- 理解项目的完整依赖图
- 跨多个文件和包追踪类型定义
- 理解架构模式（MVC、微服务、事件驱动等）
- 在完整系统上下文中识别代码异味和反模式
- 建议考虑所有下游影响的重构

### 多文件推理

基于仓库级理解，V4 预计在 **多文件推理** 方面表现出色 — 理解一个文件中的更改如何影响其他文件。

**能力：**
- 跨文件类型检查和推断
- 导入/导出链分析
- 跨模块副作用追踪
- 数据库 schema ↔ ORM 模型 ↔ API 路由一致性检查
- 全栈推理（前端 ↔ 后端 ↔ 数据库）

### 高级代码生成

泄露的基准测试显示 V4 将达到：

- **HumanEval ~90%** — 在标准编程基准测试中接近完美
- **SWE-bench Verified 80%+** — 解决流行仓库的真实 GitHub Issues
- 显著改进：复杂算法实现、系统设计、测试生成、Bug 诊断和性能优化

---

## 预期基准测试

### 编程基准测试

| 基准测试 | DeepSeek V4（预期） | Claude 4 | GPT-5 | Qwen 3.5 | DeepSeek V3.2 |
|---------|-------------------|----------|-------|-----------|---------------|
| HumanEval | ~90% | 90.2% | 91.0% | 85.4% | 82.6% |
| HumanEval+ | ~85% | 84.5% | 86.2% | 80.1% | 77.3% |
| MBPP | ~88% | 87.8% | 89.5% | 83.2% | 80.1% |
| SWE-bench Verified | 80%+ | 72.5% | 68.3% | 55.8% | 48.2% |
| SWE-bench Lite | ~85% | 78.4% | 74.1% | 62.3% | 55.7% |
| LiveCodeBench | ~75% | 70.2% | 72.8% | 63.5% | 58.4% |
| CodeContests | ~35% | 31.5% | 33.2% | 25.8% | 22.1% |

### 通用基准测试

| 基准测试 | DeepSeek V4（预期） | Claude 4 | GPT-5 | Qwen 3.5 | DeepSeek V3.2 |
|---------|-------------------|----------|-------|-----------|---------------|
| MMLU | ~92% | 91.8% | 93.2% | 88.5% | 85.7% |
| MMLU-Pro | ~78% | 76.5% | 79.1% | 72.3% | 68.9% |
| GPQA Diamond | ~68% | 65.2% | 67.8% | 58.4% | 52.1% |
| MATH-500 | ~95% | 93.5% | 94.8% | 89.2% | 85.3% |

### 长上下文基准测试

| 基准测试 | DeepSeek V4（预期） | Claude 4 | GPT-5 | Qwen 3.5 | DeepSeek V3.2 |
|---------|-------------------|----------|-------|-----------|---------------|
| RULER (128K) | ~95% | 92.3% | 88.5% | 85.2% | 80.4% |
| Needle in Haystack (1M) | ~98% | 95.1% | N/A | N/A | N/A |
| LongBench | ~60% | 55.8% | 52.3% | 48.5% | 43.2% |
| InfiniteBench | ~75% | 68.4% | 62.1% | 55.8% | 48.7% |

> **注意：** 所有 V4 数据来自泄露/未验证来源。官方基准测试将在发布后公布。

---

## 公告与延期时间线

| 日期 | 事件 | 详情 |
|------|------|------|
| 2025-07 | DeepSeek V3 发布 | V3 模型发布，确立 DeepSeek 顶级 AI 实验室地位 |
| 2025-09 | V3.1 更新 | 增量改进，更好的指令遵循 |
| 2025-11 | V3.2 发布 | 重大更新，改进编程能力，128K 上下文 |
| 2025-12 | V4 传闻开始 | 中文技术论坛报告 V4 训练已启动 |
| 2026-01 | 首次泄露基准测试 | HumanEval ~90% 分数在社交媒体上出现 |
| 2026-01 | 预期发布窗口 #1 | 社区预期1月发布 — **未兑现** |
| 2026-02 | SWE-bench 泄露 | 内部人士报告 80%+ SWE-bench Verified 分数 |
| 2026-02 | 预期发布窗口 #2 | 传闻2月目标 — **未兑现** |
| 2026-03 | 架构细节泄露 | Engram 记忆和 100万+ 上下文细节浮出水面 |
| 2026-03 | 预期发布窗口 #3 | 3月推测进行中 — **尚未发布** |
| 待定 | V4 正式发布 | 等待 DeepSeek 公告 |

---

## 使用 Atlas Cloud 提前准备

**为什么要等 V4？立即开始构建吧！**

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) 通过完全托管的 OpenAI 兼容 API 提供 **DeepSeek V3.2**。当 V4 发布时，你只需更改一行代码即可升级 — 只需更新模型名称。

### 为什么选择 Atlas Cloud？

🔒 **SOC I & II 认证** | 🏥 **HIPAA 合规** | 🇺🇸 **美国公司**

- **OpenAI 兼容 API** — 即插即用，适用于任何 OpenAI SDK
- **DeepSeek V3.2 现已可用** — $0.26/$0.38 每百万 token（输入/输出）
- **无缝 V4 升级** — 相同 API，相同端点，只需更改模型名称
- **无需管理基础设施** — 完全无服务器，自动扩展
- **企业级安全** — SOC I & II，HIPAA 合规
- **99.9% 在线率 SLA** — 生产就绪的可靠性
- **💰 支持微信支付宝直接付款** — 中国用户无需信用卡
- **慷慨免费额度** — 无需信用卡即可开始构建

### 立即开始

> 💡 **通过[此推荐链接](https://www.atlascloud.ai?ref=JPM683)注册，首次充值获得 25% 奖励（最高 $100）！**

1. 在 [atlascloud.ai](https://www.atlascloud.ai?ref=JPM683) 注册
2. 从控制台获取 API 密钥
3. 使用任何 OpenAI 兼容 SDK 调用 DeepSeek V3.2
4. V4 发布后，只需更改模型名称 — 完成！

---

## Atlas Cloud API 快速上手

Atlas Cloud API 完全兼容 OpenAI。如果你用过 OpenAI SDK，你已经知道如何使用它。

### Python

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-atlas-cloud-api-key",
    base_url="https://api.atlascloud.ai/v1"
)

# 今天使用 DeepSeek V3.2 — V4 发布后切换
response = client.chat.completions.create(
    model="deepseek/deepseek-v3.2",  # V4 可用后改为 deepseek/deepseek-v4
    messages=[
        {"role": "system", "content": "你是一位专业的软件工程师。"},
        {"role": "user", "content": "用 Python 实现一个线程安全的 LRU 缓存，要求 get 和 put 操作都是 O(1) 复杂度。"}
    ],
    temperature=0.7,
    max_tokens=4096
)

print(response.choices[0].message.content)
```

**流式输出示例：**

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-atlas-cloud-api-key",
    base_url="https://api.atlascloud.ai/v1"
)

stream = client.chat.completions.create(
    model="deepseek/deepseek-v3.2",
    messages=[
        {"role": "user", "content": "用 FastAPI 编写一个包含认证、CRUD 和测试的完整 REST API。"}
    ],
    stream=True
)

for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="")
```

### cURL

```bash
curl https://api.atlascloud.ai/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your-atlas-cloud-api-key" \
  -d '{
    "model": "deepseek/deepseek-v3.2",
    "messages": [
      {"role": "system", "content": "你是一位专业的软件工程师。"},
      {"role": "user", "content": "设计一个电商平台的微服务架构。"}
    ],
    "temperature": 0.7,
    "max_tokens": 4096
  }'
```

### Node.js

```javascript
import OpenAI from 'openai';

const client = new OpenAI({
  apiKey: 'your-atlas-cloud-api-key',
  baseURL: 'https://api.atlascloud.ai/v1'
});

// 今天使用 DeepSeek V3.2 — V4 发布后切换
const response = await client.chat.completions.create({
  model: 'deepseek/deepseek-v3.2', // V4 可用后改为 deepseek/deepseek-v4
  messages: [
    { role: 'system', content: '你是一位专业的软件工程师。' },
    { role: 'user', content: '用 Node.js 创建一个带认证和限流的实时 WebSocket 服务器。' }
  ],
  temperature: 0.7,
  max_tokens: 4096
});

console.log(response.choices[0].message.content);
```

---

## 价格

### 当前：Atlas Cloud 上的 DeepSeek V3.2

| | 每百万 Token 价格 |
|---|---|
| **输入** | $0.26 |
| **输出** | $0.38 |

### 预期：Atlas Cloud 上的 DeepSeek V4

| | 预估每百万 Token 价格 |
|---|---|
| **输入** | $0.40 - $0.60（预估） |
| **输出** | $0.60 - $1.00（预估） |

> **注意：** V4 价格为推测性的。尽管参数量巨大，MoE 架构使推理成本可控。实际价格将在发布时公布。

### 成本对比

| 提供商 | 模型 | 输入（每百万） | 输出（每百万） |
|--------|------|---------------|---------------|
| **Atlas Cloud** | **DeepSeek V3.2** | **$0.26** | **$0.38** |
| OpenAI | GPT-4o | $2.50 | $10.00 |
| Anthropic | Claude 3.5 Sonnet | $3.00 | $15.00 |
| Google | Gemini 1.5 Pro | $1.25 | $5.00 |

Atlas Cloud 上的 DeepSeek V3.2 比其他提供商的同类模型**便宜高达40倍**。

> 💰 **[通过推荐链接注册](https://www.atlascloud.ai?ref=JPM683)，获得 25% 奖励额度（最高 $100）！**

---

## V3.2 与 V4 功能对比

| 特性 | DeepSeek V3.2（现已可用） | DeepSeek V4（预期） |
|------|--------------------------|-------------------|
| **总参数量** | ~2360亿 | ~1万亿 |
| **活跃参数量** | ~210亿 | ~370亿 |
| **架构** | MoE | MoE + Engram 记忆 |
| **上下文窗口** | 128K tokens | 100万+ tokens |
| **模态** | 文本 + 代码 | 文本 + 代码 + 视觉 |
| **HumanEval** | 82.6% | ~90% |
| **SWE-bench Verified** | 48.2% | 80%+ |
| **记忆系统** | 标准注意力 | Engram 记忆架构 |
| **代码理解** | 文件级 | 仓库级 |
| **多文件推理** | 基础 | 高级 |
| **开源权重** | 是 | 预期（是） |
| **Atlas Cloud** | ✅ 可用 | 🔜 计划首日支持 |
| **API 兼容性** | OpenAI 兼容 | OpenAI 兼容 |
| **价格（输入/百万）** | $0.26 | 待定（~$0.40-0.60 预估） |
| **价格（输出/百万）** | $0.38 | 待定（~$0.60-1.00 预估） |
| **微信/支付宝付款** | ✅ 支持 | ✅ 支持 |

---

## 常见问题

### 1. DeepSeek V4 什么时候发布？

截至2026年3月，没有确认的发布日期。DeepSeek V4 已错过多个预期发布窗口（2026年1月、2月、3月）。模型似乎仍在内部测试中。我们会在官方日期公布后第一时间更新本指南。

### 2. DeepSeek V4 会免费/开源吗？

DeepSeek 有良好的开源权重发布记录。V3 和 V3.2 都以宽松许可证发布了开源权重。普遍预期 V4 将遵循相同的做法，但尚未得到官方确认。

### 3. 现在怎么试用 DeepSeek 模型？

你可以通过 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) 立即使用 **DeepSeek V3.2**。它通过 OpenAI 兼容 API 提供，价格仅为 $0.26/$0.38 每百万 token（输入/输出）。**支持微信支付宝直接付款**，中国用户无需信用卡即可使用。V4 发布后，只需更改模型名称即可升级。

### 4. DeepSeek V4 会比 GPT-5 好吗？

根据泄露的基准测试，V4 在很多任务上似乎与 GPT-5 不相上下，在 SWE-bench 等编程基准测试上可能显著优于 GPT-5。然而，官方基准测试尚未公布，实际性能可能与基准测试分数有所不同。

### 5. 什么是 Engram 记忆架构？

Engram 记忆是一种新型架构，用辅助记忆系统增强标准 transformer 注意力。它允许模型高效地压缩、索引和检索来自超长上下文（100万+ token）的信息，类似于人类大脑中"印迹"（engram，大脑中的记忆痕迹）的工作方式。

### 6. MoE 如何使 V4 在 1T 参数下保持高效？

混合专家模型（MoE）只为每个 token 激活参数的一个子集。在 V4 中，1T 参数中只有 ~370 亿被激活。这意味着你获得万亿参数模型的知识容量，但推理速度和成本与 ~370 亿模型相当。

### 7. DeepSeek V4 能理解图像吗？

是的 — V4 预计原生支持多模态，支持文本、代码和视觉输入。这支持截图转代码、UI 分析、图表理解和可视化调试等用例。

### 8. V4 支持多大的上下文窗口？

V4 预计支持 100 万+ token 的上下文，由 Engram 记忆架构驱动。这足以在单次提示中处理整个代码库、文档集或书籍长度的文件。

### 9. Atlas Cloud 会在发布当天支持 V4 吗？

Atlas Cloud 计划在 V4 可用后第一时间提供。由于 API 兼容 OpenAI，现有集成只需更改模型名称即可使用 V4 — 无需代码更改。

### 10. V4 与 Claude 4 在编程方面如何比较？

根据泄露的基准测试，V4 预计在大多数编程基准测试上匹配或超过 Claude 4，特别是 SWE-bench Verified（80%+ vs 72.5%）。然而，不同模型有不同优势，实际性能取决于具体用例。

### 11. V4 支持哪些编程语言？

与 V3.2 类似，V4 预计支持所有主流编程语言，包括 Python、JavaScript/TypeScript、Java、C/C++、Go、Rust、PHP、Ruby、Swift、Kotlin 等。仓库级理解功能预计在所有支持的语言中都能工作。

### 12. DeepSeek V4 适合企业使用吗？

通过 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) 访问时，企业级安全得到保障：
- 🔒 **SOC I & II 认证**
- 🏥 **HIPAA 合规**
- 🇺🇸 **美国公司**
- 静态和传输加密
- 不使用客户数据训练
- 提供企业 SSO 和访问控制
- **支持微信支付宝直接付款**

### 13. 准备迎接 V4 的最佳方式是什么？

1. **立即在 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) 上使用 V3.2 开始构建**
2. 使用模型无关的抽象设计应用
3. 使用 OpenAI 兼容 API 格式
4. V4 发布后，更改一行代码（模型名称）即可
5. Star 本仓库以获取 V4 更新通知！

### 14. V4 会支持函数调用/工具使用吗？

基于 V3.2 的能力和行业趋势，V4 极有可能支持函数调用、工具使用和结构化输出（JSON 模式）。这些功能对于构建 AI 代理和自主编程助手至关重要。

---

## 贡献

欢迎贡献！如果你有：

- 关于 DeepSeek V4 的新信息
- 基准测试结果或对比
- 教程或指南
- 工具集成
- Bug 报告或更正

请提交 Issue 或 Pull Request。

---

## 立即开始

不要等 V4 — **立即在 Atlas Cloud 上使用 DeepSeek V3.2 开始构建**。

🔒 SOC I & II 认证 | 🏥 HIPAA 合规 | 🇺🇸 美国公司 | 💰 支持微信支付宝直接付款

| 特性 | 详情 |
|------|------|
| **模型** | DeepSeek V3.2（V4 即将推出） |
| **价格** | $0.26 / $0.38 每百万 token |
| **API** | OpenAI 兼容 |
| **升级** | V4 发布后无缝切换 |
| **奖励** | 首次充值 25%（最高 $100） |
| **支付** | 支持微信/支付宝直接付款 |

<div align="center">

### [👉 开始使用 Atlas Cloud — 25% 奖励额度 👈](https://www.atlascloud.ai?ref=JPM683)

*使用推荐链接注册，首次充值获得 25% 奖励，最高 $100*

</div>

---

<div align="center">

**由开源社区用 ❤️ 打造**

[⬆ 返回顶部](#-awesome-deepseek-v4--关于下一代编程ai的一切)

</div>
