---
title: "[podcast]和苏煜聊Agent技术史、OpenClaw Moment、边界的消弭和社会的辐射"
date: 2026-05-02
draft: false
tags:
  - agent
  - llm
summary: Agent 不是 2026 年才出现的新概念，而是 AI 从一开始就想解决的终极问题；真正的新变化是 LLM 让“语言”成为 Agent 的感知、推理、记忆和行动脚手架，于是 Agent 从研究范式走向产品范式。OpenClaw Moment 则像 ChatGPT Moment 一样，把这种能力用新的交互形态推到大众面前。
source: https://www.xiaoyuzhoufm.com/episode/69f3857a5c60a99573fea0c2
---

<audio controls src="https://media.xyzcdn.net/626b46ea9cbbf0451cf5a962/luffrgudEiiGHQxam49tfQci63NO.m4a"></audio>
## Transcript
![](139.%20【Agent的综述】和苏煜聊Agent技术史、OpenClaw%20Moment、边界的消弭和社会的辐射-69f3857a5c60a99573fea0c2%202.txt)


## Summary

### 1. 苏煜是谁

苏煜是清华本科、美国 PhD，后来在 Ohio State 任教，创立 OSU NLP Group，长期研究 Language Agent、Computer Use Agent、Web Agent、多模态 Benchmark 等方向。后来搬到硅谷，创办 NeoCognition，定位是做 Agent Research Lab。节目里提到 NeoCognition 完成了约 **4000 万美元 seed round**，核心方向是 Agent 的 specialization / continual learning。

---

### 2. Agent 的历史主线

他把 Agent 的演进分成几代：

**第一代：Logical Agent，约 1950s-1990s。**  
代表是专家系统。核心方法是：把专家知识写成逻辑规则，再用 inference engine 推理。问题是表达能力太窄，知识获取成本极高，导致专家系统无法兑现承诺，也促成了一轮 AI winter。

**第二代：Neural Agent，2000 年后，尤其 2010 年后。**  
代表是 Deep RL、AlphaGo、Atari、Dota、星际等游戏 Agent。它比逻辑系统更能学习，但依然高度受限：任务边界窄、输入输出单一、推理隐式、sample efficiency 很差。

**第三条支线：Semantic Parsing。**  
这不是 Agent 主流线，而是 NLP 里的另一条线：把自然语言转成机器可执行的 formal meaning representation，比如 SQL、知识图谱查询、网页操作等。它本质是在扩大 Agent 的 action space：让人说的话能变成机器可执行的动作。

**第四代：Language Agent。**  
ChatGPT 之后，LLM 提供了强大的语言世界模型。语言不再只是输入输出界面，而变成 Agent 的 scaffold：用于感知、推理、记忆压缩、行动表达。这里的关键变化是：Agent 能用自然语言、编程语言、formal language 去理解和操纵数字世界。

---

### 3. 这期最核心的理论框架：Memory + Autonomy

苏煜定义 Agent 不靠花哨概念，而靠三个条件：
1. 它是一个有边界的 entity；
2. 它处在某个环境中；
3. 它会为了目标进行 goal-directed activities。

然后他认为，一个好的 Agent 至少需要两大能力：

**Memory：记忆 / 知识表示 / 学习 / 遗忘。**  
包括 semantic memory、episodic memory、procedural memory。

**Autonomy：自主性。**  
包括 perception、reasoning、decision making、action。

他的判断是：过去很多 Agent 失败，不是因为“没有智能”这么简单，而是 memory 和 autonomy 都太弱。LLM 的重要性在于，它同时增强了两者：预训练形成压缩后的世界表示，语言又让推理和行动变得可组合。

---

### 4. 为什么 Language Agent 是关键转折

节目里有一个很重要的类比：**语言在人类文明史中出现得很晚，但语言出现后，人类文明进入指数级加速。**

苏煜认为 AI Agent 现在发生了类似事情：语言成为智能体的“文明基础设施”。语言不仅是交流工具，还是符号化、压缩、推理、规划、协作的工具。所以他不把 LLM 看成“随机鹦鹉”，而是看成一种把语言表层压缩成世界表示的系统。

这也是为什么他坚持叫 **Language Agent**：不是说 Agent 只会说话，而是说它以 language/symbol 为核心机制来理解世界和行动。Coding 也是 language，所以 Coding Agent 并不是脱离 Language Agent，而是 Language Agent 在数字世界里的强势分支。

---

### 5. 过去三年 Language Agent 的关键节点

他大致复盘了这样一条线：

**2022：Chain-of-Thought 与 ReAct。**  
CoT 让模型可以用语言做 adaptive reasoning；ReAct 把“思考—行动—观察”循环引入外部环境，形成更像 Agent 的结构。

**2022-2023：LLM Planner、MindWeb、Toolformer。**  
LLM 开始用于 robot planning、web agent、tool use。Toolformer 的意义在于：模型开始能调用现成工具，这对企业软件和 productivity 场景非常关键。

**2023：AutoGPT。**  
AutoGPT 代表早期大众对 Agent 的想象：给 LLM 套一个 agent 外壳，好像它什么都能做。实际能力有限，但它提前预演了后来的 OpenClaw 式爆火。

**2023 下半年后：多模态 Agent。**  
GPT-4V / 多模态模型出现后，Agent 从 text-only 转向 vision-based / hybrid。Web Arena、MMMU、OSWorld 等 benchmark 和环境推动了 Web、Desktop、Mobile Agent 的发展。

**2024-2025：Computer Use + Coding Agent 爆发。**  
Agent 开始像人一样看屏幕、点按钮、操作像素级界面。Coding Agent 则因为代码是数字世界的底层 fabric，成为边界消弭的核心推动力。

---

### 6. OpenClaw Moment 的意义

苏煜认为 OpenClaw Moment 和 ChatGPT Moment 很像。

ChatGPT 当年并不是底层技术突然从 0 到 1，而是把已经成熟一些的 LLM 用 chatbot 交互形态释放给大众，于是大家突然感知到“原来模型已经这么强”。

OpenClaw 也是类似：Agent 的底层能力已经积累了一段时间，它真正改变的是交互形态和权限边界。比如 always-on、即时通讯入口、独立环境、更高自动化、更开放的 permission。很多 Agent 研究者可能觉得技术上 “nothing is new”，但大众第一次感知到“原来 Agent 已经能做这么多事”。

所以 OpenClaw Moment 标志的不是一个单点技术创新，而是：**高度自动化 / personal agent 范式开始被社会感知。**

---

### 7. 为什么 Coding 会消弭边界

节目里很重要的一个判断是：Browser Agent、Desktop Agent、Mobile Agent、GUI Agent、CLI Agent、API Agent、Coding Agent，这些划分都只是阶段性的。

最后大家要的是：**Universal Digital Agent**，也就是一个可以在数字世界里完成各种任务的通用智能体。

Coding 之所以关键，是因为数字世界本身就是 code render 出来的。GUI、CLI、API、网页、软件，本质上都能被代码表达和转换。因此 Coding Agent 会推动这些边界消失。

但他也反对“CLI 会完全取代 GUI”。GUI 短期甚至长期都不会消失，因为 GUI 是人类数字世界事实上的 interface，里面已经编码了大量业务逻辑、约束和历史知识。Agent 如果能用 GUI，就能 piggyback 在这些已存在的知识和系统上，而不需要全社会把旧系统都重写成 CLI/API。

---

### 8. NeoCognition 的创业 thesis

NeoCognition 的核心不是做一个“又一个通用 Agent”，而是研究 **specialized intelligence / expert agent**。

苏煜的判断是：通用智能已经越来越便宜，真正稀缺的是让 Agent 进入某个小世界后，快速变成专家。

所谓小世界包括：
- 一个公司；
- 一个部门；
- 一个职业；
- 一个软件；
- 一个工作流；
- 一个行业场景；
- 一套隐性规则和人际协作模型
- 
==Agent 要真正有价值，不能只会泛泛完成 60%-70%，而是要通过 continual learning 建立某个 micro-world 的 world model，变得可靠、快速、低成本。==

他认为下一阶段最大的 learning signal 来自真实 deployment，因为 Agent 的 research 和 production 会越来越不可分离：不部署到真实环境，就拿不到足够有效的持续学习信号。

---

### 9. 当前 Agent 最大瓶颈

他把很多问题归到同一个核心：**memory / self-learning / continual learning / world model / specialization，其实是在讲同一件事。**

现在 Agent 看起来很强，但常见问题是：
- reliability 不够；
- speed 不够；
- cost 太高；
- token 消耗大；
- 成功率不稳定；
- 进入真实场景门槛高；
- 对长尾业务、隐性规则、专业流程理解不深。

所以 2026 年他预期的主旋律是：**continual learning / self learning**。不只是把上下文塞长，而是让 Agent 能从真实工作中学习，把经验压缩成可复用的世界模型。

---

### 10. 中美差异：美国偏技术圈，中国偏全民扩散

他认为 OpenClaw 在中国的出圈程度比美国更强。美国更多还是开发者圈、技术圈在研究如何做深；中国则更容易变成全民话题、产业机会、个人翻身工具，甚至形成“不学就被淘汰”的焦虑。

但他不完全悲观。他认为中国在应用层动作快，这是 AI 时代的优势：当基础模型能力超过临界点后，大量以前“不值得做”的事情，因为 AI 降低摩擦，突然变得值得做。问题在于是否有人能发现这些长尾价值，并快速落地。

---

### 11. 大厂都在 bet 什么

他的判断是：之前大家 bet 的方向还比较分散，但现在正在高度趋同。

Anthropic 在 coding / productivity agent 上打了样，很多公司都在跟。OpenAI 也在往 Agent、productivity、coding 方向收束。Google 有强模型和强生态，但他觉得 Google 的 adoption 声势似乎还差一点，可能有更深层组织问题没看清。整体趋势是：==**大厂都会做通用入口、生产力工具和平台级 Agent，但真正垂直、专业、深场景的 expert agent 仍然留给创业公司和行业玩家。**==

---

## 技术支持
[Chrome Extension: CastSaver for Xiaoyuzhou](https://chromewebstore.google.com/detail/castsaver-for-xiaoyuzhou/nkdidhjgknghmmakckchbohafnbacpin)

[妙计飞书](https://www.feishu.cn/product/minutes)

[openai chatgpt](https://chatgpt.com/)

