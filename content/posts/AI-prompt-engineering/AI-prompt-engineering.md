---
title: AI-prompt-engineering
slug: AI-prompt-engineering
date: 2026-03-16
draft: true
tags: []
summary: |-
  Prompting 的核心，是把你脑中的东西，分析清楚，然后外化给一个聪明但没有你背景知识的对象。
  不要居高临下，不要过度简化，也不要偷懒省略关键前提。
  你要做的，是让你脑中的复杂想法，对对方来说变得可理解、可执行。
---
> Prompting 的核心，是把你脑中的东西，分析清楚，然后外化给一个聪明但没有你背景知识的对象。  不要居高临下，不要过度简化，也不要偷懒省略关键前提。  你要做的，是让你脑中的复杂想法，对对方来说变得可理解、可执行。

[AI prompt engineering: A deep dive](https://www.youtube.com/watch?v=T9aRN5JkmL8)
[prompt engineering doc](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/overview)

这里的核心不是“提示词有没有魔法”，而是：

**Prompt engineering 本质上是在把你脑子里的任务，尽可能无歧义地外化给模型。**  
它像工程，不只是因为“写了一段字”，而是因为你需要反复试验、看输出、找误解、修提示、测边界、处理异常输入，并把它嵌入整个系统里。

---

## 一句话总结

这场讨论的共识是：

**好 prompt 不是花哨技巧，而是清晰沟通 + 大量迭代 + 对模型行为的细读 + 对边界情况的系统化思考。**

---

## 主要观点总结

### 1. 什么是 prompt engineering

他们把 prompt engineering 定义成：

- 想办法让模型更好地完成任务
    
- 不只是“写一句提示词”
    
- 而是一个反复实验、观察输出、修正表达、整合进系统的过程
    

之所以叫 **engineering**，是因为它像工程一样：

- 有 trial and error
    
- 有版本管理和实验记录
    
- 有性能、延迟、上下文长度、数据来源等权衡
    
- 有系统设计问题，不只是文案问题
    

David 的说法很重要：  
**Prompt 有点像“编程模型”的方式，但别把它想得太抽象。多数时候，最有效的还是把任务清楚说出来。**

---

### 2. 什么样的人是好的 prompt engineer

他们提了几个关键能力：

#### 清晰表达

不是华丽写作，而是能把任务讲明白。  
Amanda 特别强调：**好 writer 不一定是好 prompt engineer。**

#### 愿意高频迭代

不是写一次就完，而是短时间内发很多 prompt，连续试、连续修。

#### 会找 edge cases

不能只测正常输入，要专门测异常情况，比如：

- 空输入
    
- 不符合格式的输入
    
- 数据里根本没有目标项
    
- 用户乱输、错别字、没标点、像搜索框一样乱打词
    

#### 能跳出自己的知识诅咒

这是他们反复强调的一点：

> 你自己知道这个任务，不代表 prompt 已经把任务说清楚了。

很多人写的 prompt，离开自己的上下文以后，别人都看不懂，更别说模型。

---

### 3. 提高 prompt 最重要的方法：看输出

他们反复提到一件事：

**一定要认真读模型输出。**

不是只看“对没对”，还要看：

- 它是怎么理解任务的
    
- 它哪里误解了
    
- 它有没有按你要求的格式思考
    
- 它的 reasoning 有没有偏掉
    

一个典型例子是：  
你写了 “think step by step”，但模型未必真的逐步写出了步骤。  
所以不能只写指令，要看它实际有没有执行。

---

### 4. 很多 prompt 问题，直接问模型就行

Amanda 提了一个很实用的技巧：

先把 prompt 给模型，但**不要让它执行任务**，而是让它：

- 只指出哪里不清楚
    
- 哪里有歧义
    
- 它不理解什么
    
- 哪些地方可能出错
    

还有一个技巧是：

- 告诉模型它答错了
    
- 再问它为什么答错
    
- 再让它帮你改 prompt
    

他们的结论不是“这总是对”，而是：  
**很多时候这样做真的能学到东西，而且成本很低，值得试。**

---

### 5. 别迷信“角色扮演 prompt”

他们对“you are an expert…”、“你是一个老师…”这类角色提示，态度偏谨慎。

Amanda 的观点很鲜明：

- 如果模型已经懂你的真实任务，就直接说真实任务
    
- 没必要骗它说自己是老师、学生、别的角色
    
- 她更喜欢告诉模型真实背景，比如“我是 AI researcher，我在做这个实验”
    

他们认为很多人用“角色扮演”是在偷懒：  
不是把真实任务讲清楚，而是找一个“有点像”的场景替代。

这容易出问题，因为：

- 你让模型做的是 A
    
- 但 prompt 里写成了 B
    
- 模型按 B 做得很好，但不是你真正要的 A
    

不过 Zack 也补充了一点：  
**适当的比喻/类比有时有帮助。**  
比如评价图表质量时，让模型按“像高中作业评分那样”去判断，可能能帮助它抓住你想要的标准。

所以更准确地说：

- **假的 persona 不一定有用**
    
- **恰当的类比有时有用**
    
- 但最稳的还是把真实场景讲清楚
    

---

### 6. 最常见的错误：用户把 prompt 当 Google 搜索框

他们提到两个典型误区：

#### 误区一：像搜关键词一样写 prompt

尤其在聊天产品里，很多人输入的是关键词，不是任务描述。

#### 误区二：追求一句“神之一笔”

很多人 obsess 在某句“完美指令”上，想找到一个 magical line。  
但他们认为更有效的是：

- 把任务背景讲清楚
    
- 讲出判断标准
    
- 讲出异常情况怎么办
    
- 像对一个聪明但没上下文的人交代工作那样去写
    

Amanda 给了一个很好用的心智模型：

> 想象你从 temp agency 请来一个很聪明、懂很多世界知识、但完全不了解你业务的人。  
> 你会怎么给他交代任务？那就是 prompt 该怎么写。

---

### 7. 要给模型“退路”

这是很实用的一点。

很多 prompt 只规定了正常情况，却没说异常情况怎么办。  
结果模型为了“完成任务”，会瞎猜。

比如本来是让它判断图表质量，结果输入是一张山羊图片。  
如果你没告诉它异常时怎么处理，它可能硬给出“这是个好图表”。

所以好的 prompt 应该明确：

- 看不懂时怎么办
    
- 输入不符合预期时怎么办
    
- 不确定时输出什么标记
    
- 是否允许拒答或标记 unsure
    

这样做不仅让结果更稳，还能帮你发现脏数据和边界输入。

---

### 8. Chain of thought 有用，但别哲学化过头

他们讨论了 reasoning / chain of thought：

- 模型先写推理，再给答案，通常确实更好
    
- 结构化 reasoning 也确实能进一步提高效果
    

但他们不太想陷入“这算不算真正思考”的哲学争论。  
更实际的结论是：

- **它确实有用**
    
- **不只是白白多了 token**
    
- 因为如果只是给它多一点 token 空间，让它重复“um ah”之类，不会得到同样效果
    

所以他们的态度大概是：

> 不管它是不是“真正思考”，至少 reasoning 这件事对结果质量有帮助。

---

### 9. 企业 prompt 和研究 prompt 不一样

这一段很重要。

#### 企业/产品 prompt 的目标

- 稳定
    
- 可重复
    
- 格式一致
    
- 对大量真实用户输入都能扛住
    
- 通常更依赖示例
    
- 更关注可靠性和规模化运行
    

#### 研究 prompt 的目标

- 探索模型能力边界
    
- 看多样性、看潜力、看 top performance
    
- 不一定想把输出收得很死
    
- 往往不想用太接近真实数据的示例，免得模型被“带偏”成固定模式
    

Amanda 说她有时故意给**风格完全不同**的示例，只想让模型理解“任务结构”，而不是模仿具体表述。

David 还提到一个关键区别：

- 在 Claude 聊天里，你只需要它**这一次**答对
    
- 在企业系统里，你要它**一百万次都尽量稳**
    

这会直接决定你写 prompt 的方式。

---

### 10. Prompting 最好的训练方法是什么

他们给出的建议都很实战：

#### Zack

多读好 prompt，多读模型输出。

#### Amanda

反复做，甚至把 prompt 给没上下文的人看。  
像训练写哲学论文一样，练习把复杂想法讲给“聪明但不懂背景的人”。

#### David

专门去做“你觉得模型本来做不到”的任务。  
因为真正能让你学到东西的，不是容易任务，而是边界任务。

这点很有意思：

> 只有在逼近模型能力边界时，你才会真正理解 prompt engineering。

---

### 11. Jailbreak 本质像“了解系统后的黑客行为”

他们聊 jailbreak 的看法比较克制：

- 这不是单纯“社工”
    
- 也不是单纯“语言技巧”
    
- 更像是：理解模型训练方式、注意力模式、数据分布之后，去利用其中薄弱点
    

比如：

- 多语言切换
    
- 让模型先输出某种前缀
    
- 用超长上下文
    
- 构造分布外输入
    

都可能和模型训练分布、后训练方式有关。

但 Amanda 也坦白说：  
**“jailbreak 到底在模型内部发生了什么”，现在并没有一个她很确信的统一解释。**

---

### 12. Prompt engineering 这几年最大的变化

他们认为最明显的变化是：

#### 以前有很多“技巧”

比如某些神奇写法、触发短语、特定格式。

#### 现在这些技巧越来越短命

因为一旦某种 prompting hack 被发现有效，模型团队往往会把它直接训练进模型里。  
于是：

- 以前你得写“think step by step”
    
- 后来模型看到数学题就会自然这样做了
    

所以未来趋势不是“背 prompt 咒语”，而是：

- 更高层次的清晰表达
    
- 更深的任务建模
    
- 更好的上下文提供
    
- 更强的人机协作
    

---

### 13. 一个很有意思的变化：越来越“尊重模型”

他们都提到一个趋势：

**现在更敢把完整背景、原始材料、论文直接塞给模型了。**

以前会担心：

- 信息太多它会乱
    
- 太复杂它理解不了
    
- 需要人为先简化、先转述
    

现在则更倾向于：

- 直接给 paper
    
- 直接给原文
    
- 直接让模型先读，再让它生成 prompt、模板、示例
    

Amanda 的方法甚至是：

> 想测试某个 prompting technique？直接把论文给模型看，让它自己总结成 meta-prompt。

这代表他们对模型能力边界的判断，已经和早期很不同了。

---

### 14. Prompt engineering 的未来：不会消失，但形态会变

他们的结论不是“以后不需要 prompt 了”，而是：

### 不会消失的部分

只要你还需要告诉模型：

- 目标是什么
    
- 约束是什么
    
- 成功标准是什么
    
- edge case 怎么处理
    

那 prompt engineering 就不会消失。

### 会变化的部分

未来更可能变成：

- 模型来反问你
    
- 模型来采访你
    
- 模型来帮你发现你没说清楚的地方
    
- 模型来帮助你生成 prompt
    

也就是说，从“你教模型”慢慢转向“模型帮你把想法说清楚”。

他们已经开始这么做了，比如：

- 让 Claude 采访自己
    
- 让 Claude 根据自己的回答整理 prompt
    
- 让 Claude 找出任务定义中的缺口
    

---

## 我觉得最精彩的一个结论

Amanda 最后给了一个非常强的总结，我把它翻成更自然的中文：

> Prompting 的核心，是把你脑中的东西，分析清楚，然后外化给一个聪明但没有你背景知识的对象。  
> 不要居高临下，不要过度简化，也不要偷懒省略关键前提。  
> 你要做的，是让你脑中的复杂想法，对对方来说变得可理解、可执行。

这基本就是整场最好的定义。

---

## 这场讨论最后沉淀出的几个实用原则

你平时写 prompt，可以直接记这几条：

1. **先把任务像交代给一个聪明新人那样讲清楚**
    
2. **不要迷信咒语和花招**
    
3. **认真读输出，比盯着 prompt 本身更重要**
    
4. **多测异常输入，不要只测理想 case**
    
5. **给模型不确定时的退出机制**
    
6. **模型答错了，直接问它为什么错**
    
7. **能给原始材料就给原始材料，别总想着手工 baby-sit**
    
8. **聊天 prompt 和系统 prompt 是两种东西**
    
9. **真正的提升来自做难任务、做边界任务**
    
10. **未来最重要的能力，可能不是“写神 prompt”，而是“把自己想要什么说清楚”**
    

---

英文全文对话稿：
Introduction
0:00
- Basically, this entire roundtable session here is just gonna be focused mainly on prompt engineering.
0:06
A variety of perspectives at this table around prompting from a research side, from a consumer side,
0:11
and from the enterprise side. And I want to just get the whole wide range of opinions
0:16
because there's a lot of them. And just open it up to discussion and explore what prompt engineering really is
0:24
and what it's all about. And yeah, we'll just take it from there. So maybe we can go around the horn with intros.
0:30
I can kick it off. I'm Alex. I lead Developer Relations here at Anthropic. Before that,
0:36
I was technically a prompt engineer at Anthropic. I worked on our prompt engineering team,
0:43
and did a variety of roles spanning from a solutions architect type of thing,
0:48
to working on the research side. So with that, maybe I can hand it over to David.
0:53
- Heck, yeah. My name's David Hershey. I work with customers mostly at Anthropic
0:59
on a bunch of stuff technical, I help people with finetuning, but also just a lot of the generic things
1:06
that make it hard to adopt language models of prompting. And just like how to build systems with language models,
1:11
but spend most of my time working with customers. - Cool. I'm Amanda Askell. I lead one of the Finetuning teams at Anthropic,
1:19
where I guess I try to make Claude be honest and kind.
1:24
Yeah. - My name is Zack Witten. I'm a Prompt Engineer at Anthropic.
1:30
Alex and I always argue about who the first one was. He says it's him, I say it's me. - Contested. - Yeah. I used to work a lot with individual customers,
1:38
kind of the same way David does now. And then as we brought more solutions architects
1:44
to the team, I started working on things that are meant to raise the overall levels
1:50
of ambient prompting in society, I guess, like the prompt generator and the various educational materials that people use.
1:59
- Nice, cool. Well, thanks guys for all coming here. I'm gonna start with a very broad question
Defining prompt engineering
2:05
just so we have a frame going into the rest of our conversations here. What is prompt engineering? Why is it engineering?
2:14
What's prompt, really? If anyone wants to kick that off, give your own perspective on it,
2:19
feel free to take the rein here. - I feel like we have a prompt engineer. It's his job.
2:24
- We're all prompt engineers in our own form. - But one of us has a job. - Yeah. Zack, maybe since it's in your title.
2:30
- One of us has a job, but the other three don't have jobs.
2:35
- I guess I feel like prompt engineering is trying to get the model to do things, trying to bring the most out of the model.
2:42
Trying to work with the model to get things done that you wouldn't have been able to do otherwise.
2:49
So a lot of it is just clear communicating. I think at heart,
2:55
talking to a model is a lot like talking to a person. And getting in there and understanding the psychology of the model,
3:02
which Amanda is the world's most expert person in the world.
3:08
- Well, I'm gonna keep going on you. Why is engineering in the name?
3:13
- Yeah. I think the engineering part comes from the trial and error. - Okay. - So one really nice thing about talking to a model
3:23
that's not like talking to a person, is you have this restart button. This giant go back to square zero
3:28
where you just start from the beginning. And what that gives you the ability to do that you don't have, is a truly start from scratch
3:34
and try out different things in an independent way, so that you don't have interference from one to the other.
3:40
And once you have that ability to experiment and to design different things, that's where the engineering part has the potential
3:48
to come in. - Okay. So what you're saying is as you're writing these prompts,
3:53
you're typing in a message to Claude or in the API or whatever it is. Being able to go back and forth with the model
4:00
and to iterate on this message, and revert back to the clean slate every time,
4:06
that process is the engineering part. This whole thing is prompt engineering all in one.
4:13
- There's another aspect of it too, which is integrating the prompts
4:19
within your system as a whole. And David has done a ton of work with customers integrating.
4:26
A lot of times it's not just as simple as you write one prompt and you give it to the model and you're done. In fact, it's anything but. It's like way more complicated.
4:32
- Yeah. I think of prompts as the way that you program models a little bit,
4:38
that makes it too complicated. 'Cause I think Zack is generally right that it's just talking clearly is the most important thing.
4:45
But if you think about it a little bit as programming a model, you have to think about where data comes from, what data you have access to.
4:51
So if you're doing RAG or something, what can I actually use and do and pass to a model?
4:57
You have to think about trade-offs in latency and how much data you're providing and things like that.
5:03
There's enough systems thinking that goes into how you actually build around a model. I think a lot of that's also the core
5:08
of why it maybe deserves its own carve-out as a thing to reason about separately from just a software engineer
5:16
or a PM or something like that. It's kind of its own domain of how to reason about these models. - Is a prompt in this sense then natural language code?
5:24
Is it a higher level of abstraction or is it a separate thing? - I think trying to get too abstract with a prompt is a way
5:33
to overcomplicate a thing, because I think, we're gonna get into it, but more often than not,
5:38
the thing you wanna do is just write a very clear description of a task, not try to build crazy abstractions or anything like that.
5:47
But that said, you are compiling the set of instructions and things like that into outcomes a lot of times.
5:54
So precision and a lot the things you think about with programming about version control
6:00
and managing what it looked like back then when you had this experiment. And tracking your experiment and stuff like that,
6:06
that's all just equally important to code. - Yeah.
6:12
- So it's weird to be in this paradigm where written text, like a nice essay that you wrote is something
6:18
that's looked like the same thing as code. But it is true that now we write essays
6:25
and treat them code, and I think that's actually correct. - Yeah. Okay, interesting. So maybe piggybacking off of that,
6:32
we've loosely defined what prompt engineering is. So what makes a good prompt engineer?
What makes a good prompt engineer
6:38
Maybe, Amanda, I'll go to you for this, since you're trying to hire prompt engineers more so in a research setting.
6:45
What does that look like? What are you looking for in that type of person? - Yeah, good question. I think it's a mix of like Zack said, clear communication,
6:55
so the ability to just clearly state things, clearly understand tasks,
7:00
think about and describe concepts really well. That's the writing component, I think. I actually think that being a good writer
7:08
is not as correlated with being a good prompt engineer as people might think.
7:13
So I guess I've had this discussion with people 'cause I think there's some argument as like, "Maybe you just shouldn't have the name engineer in there.
7:19
Why isn't it just writer?" I used to be more sympathetic to that. And then, I think, now I'm like what you're actually doing,
7:27
people think that you're writing one thing and you're done. Then I'll be like to get a semi-decent prompt
7:34
when I sit down with the model. Earlier, I was prompting the model and I was just like in a 15-minute span
7:40
I'll be sending hundreds of prompts to the model. It's just back and forth, back and forth, back and forth. So I think it's this willingness to iterate and to look
7:48
and think what is it that was misinterpreted here, if anything? And then fix that thing.
7:55
So that ability to iterate. So I'd say clear communication, that ability to iterate.
8:01
I think also thinking about ways in which your prompt might go wrong. So if you have a prompt
8:06
that you're going to be applying to say, 400 cases, it's really easy to think about the typical case that it's going to be applied to,
8:12
to see that it gets the right solution in that case, and then to move on. I think this is a very classic mistake that people made.
8:19
What you actually want to do is find the cases where it's unusual. So you have to think about your prompt and be like,
8:25
"What are the cases where it'd be really unclear to me what I should do in this case?" So for example, you have a prompt that says, "I'm going to send you a bunch of data.
8:31
I want you to extract all of the rows where someone's name is, I don't know, starts with the letter G."
8:37
And then you're like, "Well, I'm gonna send it a dataset where there is no such thing, there is no such name that starts with the letter G.
8:43
"I'm going to send it something that's not a dataset, I might also just send it an empty string. These are all of the cases you have to try,
8:49
because then you're like, "What does it do in these cases? " And then you can give it more instructions for how it should deal with that case.
8:55
- I work with customers so often where you're an engineer, you're building something. And there's a part in your prompt where a customer of theirs
9:03
is going to write something. - Yeah. - And they all think about these really perfectly phrased things that they think someone's going to type into their chatbot.
9:09
And in reality, it's like they never used the shift key and every other word is a typo.
9:15
- They think it's Google. - And there's no punctuation. - They just put in random words with no question. - Exactly.
9:20
So you have these evals that are these beautifully structured what their users ideally would type in. But being able to go the next step
9:26
to reason about what your actual traffic's gonna be like, what people are actually gonna to try to do, that's a different level of thinking.
9:33
- One thing you said that really resonated with me is reading the model responses. In a machine learning context,
9:39
you're supposed to look at the data. It's almost a cliche like look at your data, and I feel like the equivalent for prompting
9:45
is look at the model outputs. Just reading a lot of outputs and reading them closely.
9:51
Like Dave and I were talking on the way here, one thing that people will do is they'll put think step-by-step in their prompt.
9:57
And they won't check to make sure that the model is actually thinking step-by-step, because the model might take it in a more abstract
10:04
or general sense. Rather than like, "No, literally you have to write down your thoughts in these specific tags."
10:10
So yeah, if you aren't reading the model outputs, you might not even notice that it's making that mistake.
10:16
- Yeah, that's interesting. There is that weird theory of mind piece
10:22
to being a prompt engineer where you have to think almost about how the model's gonna view your instructions. But then if you're writing for an enterprise use case too,
10:29
you also have to think about how the user's gonna talk to the model, as you're the third party sitting there
10:34
in that weird relationship. Yeah. - On the theory of mind piece, one thing I would say is,
10:43
it's so hard to write instructions down for a task. It's so hard to untangle in your own brain
10:51
all of the stuff that you know that Claude does not know and write it down. It's just an immensely challenging thing
10:57
to strip away all of the assumptions you have, and be able to very clearly communicate the full fact set of information
11:04
that is needed to a model. I think that's another thing that really differentiates a good prompt engineer from a bad one, is like...
11:10
A lot of people will just write down the things they know. But they don't really take the time to systematically break out
11:17
what is the actual full set of information you need to know to understand this task? - Right. - And that's a very clear thing I see a lot
11:24
is prompts where it's just conditioned. The prompt that someone wrote is so conditioned
11:30
on their prior understanding of a task, that when they show it to me I'm like, "This makes no sense.
11:36
None of the words you wrote make any sense, because I don't know anything about your interesting use case."
11:42
But I think a good way to think about prompt engineering in that front and a good skill for it,
11:47
is just can you actually step back from what you know and communicate to this weird system that knows a lot,
11:54
but not everything about what it needs to know to do a task? - Yeah. The amount of times I've seen someone's prompt
12:00
and then being like, "I can't do the task based on this prompt." I'm human level and you're giving this to something
12:06
that is worse than me and expecting it to do better, and I'm like, "Yeah."
12:12
- Yeah. There is that interesting thing with like... Current models don't really do a good job
Refining prompts
12:19
of asking good, probing questions in response like a human would. If I'm giving Zack directions on how to do something,
12:26
he'll be like, "This doesn't make any sense. What am I supposed to do at this step or here and here?" Model doesn't do that, right, so you have to, as yourself,
12:34
think through what that other person would say and then go back to your prompt and answer those questions.
12:40
- You could ask it to do that. - You could. That's right. - I do that, yeah. - I guess that's another step. - I was going to say one of the first things I do
12:45
with my initial prompt, is I'll give it the prompt and then I'll be like, "I don't want you to follow these instructions. I just want you to tell me the ways in
12:51
which they're unclear or any ambiguities, or anything you don't understand." And it doesn't always get it perfect, but it is interesting that that is one thing you can do.
12:59
And then also sometimes if people see that the model makes a mistake, the thing that they don't often do is just ask the model.
13:04
So they say to the model, "You got this wrong. Can you think about why? And can you maybe write an edited version of my instructions
13:09
that would make you not get it wrong?" And a lot of the time, the model just gets it right. The model's like, "Oh, yeah.
13:15
Here's what was unclear, here's a fix to the instructions," and then you put those in and it works. - Okay.
13:21
I'm actually really curious about this personally almost. Is that true that that works?
13:26
Is the model able to spot its mistakes that way? When it gets something wrong, you say, "Why did you get this wrong?"
13:32
And then it tells you maybe something like, "Okay, how could I phrase this to you in the future
13:37
so you get it right?" Is there an element of truth to that? Or is that just a hallucination on the model's part
13:43
around what it thinks its limits are? - I think if you explain to it what it got wrong,
13:49
it can identify things in the query sometimes. I think this varies by task. This is one of those things where I'm like I'm not sure
13:56
what percentage of the time it gets it right, but I always try it 'cause sometimes it does. - And you learn something. - Yeah.
14:01
- Anytime you go back to the model or back and forth with the model, you learn something about what's going on.
14:06
I think you're giving away information if you don't at least try. - That's interesting.
14:12
Amanda, I'm gonna keep asking you a few more questions here. One thing maybe for everybody watching this,
14:18
is we have these Slack channels at Anthropic where people can add Claude into the Slack channel,
14:24
then you can talk to Claude through it. And Amanda has a Slack channel that a lot of people follow of her interactions with Claude.
14:32
And one thing that I see you always do in there, which you probably do the most of anyone at Anthropic,
14:37
is use the model to help you in a variety of different scenarios.
14:42
I think you put a lot of trust into the model in the research setting. I'm curious how you've developed those intuitions
14:49
for when to trust the model. Is that just a matter of usage, experience or is it something else?
14:55
- I think I don't trust the model ever and then I just hammer on it. So I think the reason why you see me do that a lot,
15:02
is that that is me being like, "Can I trust you to do this task?" 'Cause there's some things, models are kind of strange.
15:08
If you go slightly out of distribution, you just go into areas where they haven't been trained
15:14
or they're unusual. Sometimes you're like, "Actually, you're much less reliable here, even though it's a fairly simple task."
15:21
I think that's happening less and less over time as models get better, but you want to make sure you're not in that kind of space.
15:26
So, yeah, I don't think I trust it by default, but I think in ML, people often want to look across really large datasets.
15:33
And I'm like, "When does it make sense to do that?" And I think the answer is when you get relatively low signal from each data point,
15:39
you want to look across many, many data points, because you basically want to get rid of the noise. With a lot of prompting tasks,
15:46
I think you actually get really high signal from each query. So if you have a really well-constructed set
15:52
of a few hundred prompts, that I think can be much more signal than thousands that aren't as well-crafted.
15:59
So I do think that I can trust the model if I look at 100 outputs of it and it's really consistent.
16:06
And I know that I've constructed those to basically figure out all of the edge cases and all of the weird things that the model might do,
16:12
strange inputs, et cetera. I trust that probably more than a much more loosely constructed set
16:19
of several thousand. - I think in ML, a lot of times the signals are numbers.
16:29
Did you predict this thing right or not? And it'd be looking at the logprobs of a model
16:34
and trying to intuit things, which you can do, but it's kind of sketchy.
16:39
I feel like the fact that models output more often than not a lot of stuff like words and things.
16:44
There's just fundamentally so much to learn between the lines of what it's writing and why and how,
16:50
and that's part of what it is. It's not just did it get the task right or not? It's like, "How did it get there?
16:57
How was it thinking about it? What steps did it go through?" You learn a lot about what is going on, or at least you can try to get a better sense, I think.
17:04
But that's where a lot of information comes from for me, is by reading the details of what came out, not just through the result.
17:09
- I think also the very best of prompting can make the difference between a failed
17:16
and a successful experiment. So sometimes I can get annoyed if people don't focus enough on the prompting component of their experiment,
17:23
because I'm like, "This can, in fact, be the difference between 1% performance in the model or 0.1%."
17:31
In such a way that your experiment doesn't succeed if it's at top 5% model performance, but it does succeed if it's top 1% or top 0.1%.
17:39
And then I'm like, "If you're gonna spend time over coding your experiment really nicely, but then just not spend time on the prompt."
17:47
I don't know. That doesn't make sense to me, 'cause that can be the difference between life and death of your experiment. - Yeah.
17:52
And with the deployment too, it's so easy to, "Oh, we can't ship this." And then you change the prompt around
17:58
and suddenly it's working. - Yeah. - It's a bit of a double-edged sword though, because I feel like there's a little bit of prompting where there's always this mythical, better prompt
18:07
that's going to solve my thing on the horizon. - Yeah. - I see a lot of people get stuck into the mythical prompt on the horizon,
18:13
that if I just keep grinding, keep grinding. It's never bad to grind a little bit on a prompt, as we've talked, you learn things.
18:19
But it's one of the scary things about prompting is that there's this whole world of unknown.
18:25
- What heuristics do you guys have for when something is possible versus not possible
18:30
with a perfect prompt, whatever that might be? - I think I'm usually checking for whether the model kind of gets it.
18:37
So I think for things where I just don't think a prompt is going to help, there is a little bit of grinding.
18:43
But often, it just becomes really clear that it's not close or something.
18:49
Yeah. I don't know if that's a weird one where I'm just like, "Yeah, if the model just clearly can't do something,
18:55
I won't grind on it for too long." - This is the part that you can evoke how it's thinking about it, and you can ask it how it's thinking about it and why.
19:02
And you can get a sense of is it thinking about it right? Are we even in the right zip code of this being right?
19:11
And you can get a little bit of a kneeling on that front of, at least, I feel like I'm making progress towards getting something closer to right.
19:19
Where there's just some tasks where you really don't get anywhere closer to it's thought process.
19:24
It's just like every tweak you make just veers off in a completely different, very wrong direction, and I just tend to abandon those.
19:31
I don't know. - Those are so rare now though, and I get really angry at the model when I discover them
19:36
because that's how rare they are. I get furious. I'm like, "How dare there be a task that you can't just do,
19:43
if I just push you in the right direction?" - I had my thing with Claude plays Pokemon recently,
19:49
and that was one of the rare times where I really... - Yeah, can you explain that? Explain that just for people. I think that's really cool.
19:54
- I did a bit of an experiment where I hooked Claude up to a Game Boy emulator,
19:59
and tried to have it play the game Pokemon Red like the OG Pokemon.
20:05
And it's like you think what you wanna do and it could write some code to press buttons
20:10
and stuff like that, pretty basic. And I tried a bunch of different very complex prompting layouts, but you just get into certain spots
20:18
where it just really couldn't do it. So showing it a screenshot of a Game Boy,
20:24
it just really couldn't do. And it just so deeply because I'm so used to it, being able to do something mostly.
20:32
So I spent a whole weekend trying to write better and better prompts to get it
20:38
to really understand this Game Boy screen. And I got incrementally better so that it was only terrible
20:44
instead of completely no signal. You could get from no signal to some signal.
20:49
But it was, I don't know, at least this is elicited for me. Once I put a weekend of time in and I got from no signal
20:56
to some signal, but nowhere close to good enough, I'm like, "I'm just going to wait for the next one. (Alex laughing)
21:01
I'm just gonna wait for another model." I could grind on this for four months, and the thing that would come out is another model
21:07
and that's a better use of my time. Just sit and wait to do something else in the meanwhile. - Yeah.
21:12
That's an inherent tension we see all the time, and maybe we can get to that in a sec. Zack, if you wanna go. - Something I liked about your prompt with Pokemon
21:19
where you got the best that you did get, was the way that you explained to the model that it is in the middle of this Pokemon game.
21:27
Here's how the things are gonna be represented.
21:33
I actually think you actually represented it in two different ways, right? - I did. So what I ended up doing, it was obnoxious
21:40
but I superimposed a grid over the image, and then I had to describe each segment of the grid
21:46
in visual detail. Then I had to reconstruct that into an ASCII map
21:51
and I gave it as much detail as I could. The player character is always at location 4, 5 on the grid
21:57
and stuff like that, and you can slowly build up information. I think it's actually a lot like prompting,
22:03
but I just hadn't done it with images before. Where sometimes my intuition
22:08
for what you need to tell a model about text, is a lot different from what you need to tell a model about images. - Yeah.
22:14
- I found a surprisingly small number of my intuitions about text have transferred to image.
22:20
I found that multi-shot prompting is not as effective for images and text. I'm not really sure, you can have theoretical explanations about why.
22:27
Maybe there's a few of it in the training data, a few examples of that.
22:32
- Yeah. I know when we were doing the original explorations with prompting multimodal, we really couldn't get it to noticeably work.
22:40
You just can't seem to improve Claude's actual, visual acuity in terms of what it picks up within an image.
22:48
Anyone here has any ways that they've not seen that feature. But it seems like that's similar with the Pokemon thing where it's trying to interpret this thing.
22:55
No matter how much you throw prompts at it, it just won't pick up that Ash that's in that location.
23:01
- Yeah. But I guess to be visceral about this, I could eventually get it so that it could most often tell me where a wall was,
23:07
and most often tell me where the character was. It'd be off by a little bit. But then you get to a point,
23:13
and this is maybe coming back to knowing when you can't do it. It would describe an NPC, and to play a game well,
23:19
you need to have some sense of continuity. Have I talked to this NPC before?
23:25
And without that, you really don't, there's nothing you can do. You're just going to keep talking to the NPC, 'cause like, "Well, maybe this is a different NPC."
23:31
But I would try very hard to get it to describe a NPC and it's like, "It's a person."
23:37
They might be wearing a hat, they weren't wearing a hat. And it's like you grind for a while, inflate it to 3000X and just crop it to just the NPC,
23:46
and it's like, "I have no idea what this is." It's like I showed it this clear, female NPC thing
23:54
enough times and it just got nowhere close to it, and it's like, "Yeah, this is a complete lost cause." - Wow, okay.
24:00
- I really want to try this now. I'm just imagining all the things I would try. I don't know, I want you to imagine this game art
24:08
as a real human and just describe to me what they're like. What did they look like as they look in the mirror?
24:13
And then just see what the model does. - I tried a lot of things.
24:18
The eventual prompt was telling Claude it was a screen reader for a blind person, which I don't know if that helped,
24:24
but it felt right so I stuck with that. - That's an interesting point. I actually wanna go into this a little bit
Honesty, personas and metaphors in prompts
24:29
'cause this is one of the most famous prompting tips, is to tell the language model that they are some persona
24:35
or some role. I feel like I see mixed results. Maybe this worked a little bit better in previous models
24:41
and maybe not as much anymore. Amanda, I see you all the time be very honest with the model
24:47
about the whole situation like, "Oh, I am an AI researcher and I'm doing this experiment." - I'll tell it who I am. - Yeah.
24:52
- I'll give it my name, be like, "Here's who you're talking to." - Right. Do you think that level of honesty, instead of lying to the model or forcing it to like,
25:01
"I'm gonna tip you $500." Is there one method that's preferred there,
25:06
or just what's your intuition on that? - Yeah. I think as models are more capable and understand more
25:12
about the world, I guess, I just don't see it as necessary to lie to them.
25:18
I also don't like lying to the models just 'cause I don't like lying generally. But part of me is if you are, say, constructing.
25:26
Suppose you're constructing an eval dataset for a machine learning system or for a language model.
25:32
That's very different from constructing a quiz for some children. So when people would do things like,
25:38
"I am a teacher trying to figure out questions for a quiz." I'm like, "The model knows what language model evals are."
25:45
If you ask it about different evals it can tell you, and it can give you made up examples of what they look like. 'Cause these things are like they understand them,
25:52
they're on the internet. So I'm like, "I'd much rather just target the actual task that I have." So if you're like, "I want you to construct questions
25:59
that look a lot like an evaluation of a language model." It's that whole thing of clear communication.
26:05
I'm like, "That is, in fact, the task I want to do. So why would I pretend to you that I want to do some unrelated,
26:11
or only tangentially related task?" And then expect you to somehow do better at the task that I actually want you to do.
26:16
We don't do this with employees. I wouldn't go to someone that worked with me and be like, "You are a teacher and you're trying to quiz your students."
26:25
I'd be like, "Hey, are you making that eval?" I don't know. So I think maybe it's a heuristic from there where I'm like,
26:31
"If they understand the thing, just ask them to do the thing that you want." - I see this so much. - I guess to push back a little bit,
26:36
I have found cases where not exactly lying but giving it a metaphor
26:41
for how to think about it could help. In the same way that sometimes I might not understand how to do something and someone's like, "Imagine that you were doing this,
26:47
even though I know I'm not doing it." The one that comes to mind for me, is I was trying to have Claude say whether an image
26:54
of a chart or a graph is good or not. Is it high quality? And the best prompt that I found for this
27:02
was asking the model what grade it would give the chart, if it were submitted as a high school assignment.
27:09
So it's not exactly saying, "You are a high school teacher." It's more like, "This is the kind of analysis
27:17
that I'm looking from for you." The scale that a teacher would use is similar to the scale
27:22
that I want you to use. - But I think those metaphors are pretty hard to still come up with.
27:27
I think people still, the default you see all the time is finding some facsimile of the task.
27:33
Something that's a very similar-ish task, like saying you're a teacher. You actually just lose a lot
27:40
in the nuance of what your product is. I see this so much in enterprise prompts where people write something similar,
27:46
because they have this intuition that it's something the model has seen more of maybe. It's seen more high school quizzes than it has LLM evals,
27:56
and that may be true. But to your point, as the models get better, I think just trying to be very prescriptive
28:05
about exactly the situation they're in. I give people that advice all the time. Which isn't to say that I don't think to the extent
28:11
that it is true that thinking about it the way that someone would grade a chart,
28:17
as how they would grade a high school chart, maybe that's true. But it's awkwardly the shortcut people use a lot of times
28:25
to try to get what happens, so I'll try to get someone that I can actually talk about 'cause I think it's somewhat interesting. So writing you are a helpful assistant,
28:35
writing a draft of a document, it's not quite what you are.
28:41
You are in this product, so tell me. If you're writing an assistant that's in a product,
28:47
tell me I'm in the product. Tell me I'm writing on behalf of this company, I'm embedded in this product.
28:52
I'm the support chat window on that product. You're a language model, you're not a human, that's fine.
28:59
But just being really prescriptive about the exact context about where something is being used.
29:05
I found a lot of that. Because I guess my concern most often with role prompting, is people used it as a shortcut
29:12
of a similar task they want the model to do. And then they're surprised when Claude doesn't do their task right, but it's not the task.
29:18
You told it to do some other task. And if you didn't give it the details about your task, I feel like you're leaving something on the table.
29:24
So I don't know, it does feel like a thing though to your point of as the models scale.
29:31
Maybe in the past it was true that they only really had a strong understanding of elementary school tests comparatively.
29:39
But as they get smarter and can differentiate more topics, I don't know, just like being clear.
29:44
- I find it interesting that I've never used this prompting technique. - Yeah, that's funny. - Even with worse models
29:50
and I still just don't ever find myself, I don't know why. I'm just like, "I don't find it very good essentially."
29:57
- Interesting. - I feel like completion era models, there was a little bit of a mental model
30:03
of conditioning the model into a latent space that was useful that I worried about,
30:10
that I don't really worry about too much anymore. - It might be intuitions from pretrained models
30:15
over to RLHF models, that to me, just didn't make sense. It makes sense to me if you're prompting a pretrained.
30:22
- You'd be amazed how many people try to apply their intuitions. I think it's not that surprising. Most people haven't really experimented
30:29
with the full what is a pretrained model? What happens after you do SL?
30:34
What happens after you do RLHF, whatever? So when I talk to customers,
30:41
it's all the time that they're trying to map some amount of, "Oh, how much of this was on the internet?
30:46
Have they seen a ton of this on the internet?" You just hear that intuition a lot, and I think it's well-founded fundamentally.
30:54
But it is overapplied by the time you actually get to a prompt,
30:59
because of what you said. By the time they've gone through all of this other stuff, that's not actually quite what's being modeled.
31:05
- Yeah. The first thing that I feel like you should try is, I used to give people this thought experiment
31:10
where it's like imagine you have this task. You've hired a temp agency to send someone to do this task.
31:18
This person arrives, you know they're pretty competent. They know a lot about your industry and so forth,
31:23
but they don't know the name of your company. They've literally just shown up and they're like, "Hey, I was told you guys had a job for me to do,
31:29
tell me about it." And then it's like, "What would you say to that person?" And you might use these metaphors. You might say things like,
31:37
"We want you to detect good charts. What we mean by a good chart here,
31:42
is it doesn't need to be perfect. You don't need to go look up whether all of the details are correct." It just needs to have its axes labeled,
31:50
and so think about maybe high school level, good chart. You may say exactly that to that person
31:56
and you're not saying to them, "You are a high school." You wouldn't say that to them. You wouldn't be like, "You're a high school teacher reading charts."
32:04
- What are you talking about? - Yeah, so sometimes I'm just like it's like the whole
32:10
if I read it. I'm just like, "Yeah. Imagine this person who just has very little context, but they're quite competent. They understand a lot of things about the world."
32:16
Try the first version that actually assumes that they might know things about the world, and if that doesn't work, you can maybe do tweaks and stuff.
32:22
But so often, the first thing I try is that, and then I'm like, "That just worked." - That worked. - And then people are like,
32:28
"Oh, I didn't think to just tell it all about myself and all about the task I want to do." - I've carried this thing that Alex told me
32:33
to so many customers where they're like, "Oh, my prompt doesn't work. Can you help me fix it?" I'm like, "Well, can you describe to me what the task was?"
32:40
And I'm like, "Okay. Now what you just said to me, just voice record that and then transcribe it." And then paste it into the prompt
32:47
and it's a better prompt than what you wrote, but this is a laziness shortcut, I think, to some extent.
32:52
Because people write something that they... I just think people, I'm lazy. A lot of people are lazy.
32:57
- We had that in prompt assistance the other day where somebody was like, "Here's the thing, here's what I want it to do,
33:03
and here's what it's actually doing instead." So then I just literally copied the thing that they said they wanted it to do, and pasted it in and it worked.
33:09
- Yeah. I think a lot of people still haven't quite wrapped their heads
33:15
around what they're really doing when they're prompting. A lot of people see a text box and they think it's a Google search box.
33:21
They type in keywords and maybe that's more on the chat side. But then on the enterprise side of things,
33:26
you're writing a prompt for an application. There is still this weird thing to it where people are trying to take all these little shortcuts
33:34
in their prompt, and just thinking that, "Oh, this line carries a lot of weight in this." - Yeah. I think you obsess over getting the perfect little line
33:40
of information and instruction, as opposed to how you just described that graph thing. I would be a dream if I read prompts like that.
33:48
If someone's like, "Well, you do this and this, and there's some stuff to consider about this and all that." But that's just not how people write prompts.
33:54
They work so hard to find the perfect, insightful. A perfect graph looks exactly like this exact perfect thing,
34:02
and you can't do that. It's just very hard to ever write that set of instructions down prescriptively,
34:08
as opposed to how we actually talk to humans about it, which is try to instill some amount of the intuitions you have.
34:13
- We also give them outs. This is a thing that people can often forget in prompts. So cases, if there's an edge case,
34:20
think about what you want the model to do. 'Cause by default, it will try the best to follow your instructions, much as the person from the temp agency would,
34:26
'cause they're like, "Well, they didn't tell me how to get in touch with anyone." If I'm just given a picture of a goat and I'm like,
34:32
"What do I do? This isn't even a chart. How good is a picture of a goat as a chart?"
34:38
I just don't know. And if you instead say something like, "If something weird happens and you're really not sure
34:44
what to do, just output in tags unsure." Then you can go look through the unsures
34:50
that you got and be like, "Okay, cool. It didn't do anything weird." Whereas by default, if you don't give the person the option,
34:55
they're like, "It's a good chart." Then people will be like, "How do I do that?" And then you're like, "Well, give it an out.
35:02
Give it something to do if it's a really unexpected input happens." - And then you also improved your data quality
35:07
by doing that too, 'cause you found all the screwed up examples. - Oh, yeah. - That's my favorite thing about iterating on tests
35:14
with Claude, is the most common outcome is I find all of the terrible tests I accidentally wrote because it gets it wrong.
35:20
I'm like, "Oh, why did it get wrong?" I was like, "Oh, I was wrong." - Yeah. - Yeah. - If I was a company working with this,
35:27
I do think I would just give my prompts to people, because I used to do this
35:32
when I was evaluating language models. I would take the eval myself. 'Cause I'm like, "I need to know what this eval looks like
35:38
if I'm gonna to be grading it, having models take it, thinking about outputs, et cetera." I would actually just set up a little script
35:44
and I would just sit and I would do the eval. - Nowadays, you just have called the Streamboard app
35:50
for you. - And just does it, yeah. - Yeah. I'm reminded of Karpathy's ImageNet.
35:56
I was in 231 at Stanford and it's like benchmarking, he's showing the accuracy number.
36:03
And he's like, "And here's what my accuracy number was." And he had just gone through the test set and evaluated himself. - Oh, yeah.
36:08
- You just learn a lot. - Yeah, totally. - And it's better when it's a, again, the temp agency person,
36:14
like someone who doesn't know the task, because that's a very clean way to learn things. - Yeah.
36:19
The way you have to do it is, some evaluations come with instructions, and so I would give myself those instructions as well
36:25
and then try to understand it. And it's actually quite great if you don't have context
36:30
on how it's graded. And so often, I would do so much worse than the human benchmark and I was like, "I don't even know how you got humans to do this well
36:37
at this task, 'cause apparently human level here is 90%, and I'm at 68%."
36:45
- That's funny. That reminds me of just when you look at the MMLU questions and you're like, "Who would be able to answer these?"
36:53
It's just like absolute garbage in some of them. Okay.
36:59
I have one thing I wanna circle back on that we were talking about a few questions back around,
37:05
I think you were saying getting signal from the responses. There's just so much there and it's more than just a number,
Model reasoning
37:12
and you can actually read into the almost thought process. I bet this is probably a little contentious maybe
37:19
around chain of thought. For people listening, chain of thought, this process of getting them all
37:25
to actually explain its reasoning before it provides an answer. Is that reasoning real
37:31
or is it just kind of like a holding space for the model to do computation?
37:36
Do we actually think there's good, insightful signal that we're getting out of the model there? - This is one of the places where I struggle with that.
37:43
I'm normally actually somewhat pro-personification because I think it helps you get decent facsimiles,
37:49
thoughts of how the model's working. And this one, I think it's harmful maybe almost
37:55
to get too into the personification of what reasoning is, 'cause it just loses the thread of what we're trying to do here.
38:02
Is it reasoning or not? It feels almost like a different question than what's the best prompting technique?
38:08
It's like you're getting into philosophy, which we can get into. - Yeah, we do have a philosopher.
38:13
- Yeah. I will happily be beaten down by a real philosopher as I try to speculate on this, but instead, it just works.
38:21
Your model does better. The outcome is better if you do reasoning.
38:26
I think I've found that if you structure the reasoning and help iterate with the model
38:32
on how it should do reasoning, it works better too.
38:38
Whether or not that's reasoning or how you wanted to classify it, you can think of all sorts of proxies for how I would also do really bad
38:44
if I had to do one-shot math without writing anything down. Maybe that's useful, but all I really know is,
38:51
it very obviously does help. I don't know. - A way of testing would be if you take out all the reasoning that it did
38:58
to get to the right answer, and then replace it with somewhat, realistic-looking reasoning
39:04
that led to a wrong answer, and then see if it does conclude the wrong answer. I think we actually had a paper where we did some of that.
39:12
There was the scratch pad. It was like the Sleeper Agents.
39:17
- Oh, okay. Alignment papers. - But I think that was maybe a weird situation. But definitely what you said about structuring the reasoning
39:27
and writing example of how the reasoning works. Given that that helps,
39:33
like whether we use the word reasoning or not, I don't think it's just a space for computation.
39:38
- So there is something there. - I think there's something there, whatever we wanna call it. - Yeah. Having it write a story before it finished a task,
39:45
I do not think would work as well. - I've actually tried that and it didn't work as well as reasoning.
39:50
- Clearly, the actual reasoning part is doing something towards the outcome. - I've tried like,
39:56
"Repeat the words um and ah in any order that you please for 100 tokens and then answer."
40:02
- Yeah. I guess that's a pretty thorough defeat of it's just more computational space where it can do attention over and over again. I don't think it's just more attention
40:08
like doing more attention. - I guess the strange thing is, and I don't have an example off the top of my head to back this up with.
40:14
But I definitely have seen it before where it lays out steps, one of the steps is wrong, but then it still reaches the right answer at the end.
40:22
So it's not quite, I guess, yeah, we can't really, truly personify it as a reasoning,
40:27
'cause there is some element to it doing something slightly different.
40:32
- Yeah. I've also met a lot of people who make inconsistent steps of reasoning. - I guess that's true.
40:40
- It fundamentally defeats the topic of reasoning by making a false step on the way there. - All right, it's interesting.
40:47
Also, on maybe this prompting misconceptions round of questions.
40:54
Zack, I know you have strong opinions on this, good grammar, punctuation. - Oh, do I?
40:59
- Is that necessary in a prompt? Do you need it? Do you need to format everything correctly?
41:07
- I usually try to do that because I find it fun, I guess, somehow.
41:14
I don't think you necessarily need to. I don't think it hurts. I think it's more that you should have the level of attention to detail
41:22
that would lead you to doing that naturally. If you're just reading over your prompt a lot,
41:28
you'll probably notice those things and you may as well fix them. And like what Amanda was saying,
41:33
that you wanna put as much love into the prompt as you do into the code.
41:39
People who write a lot of code have strong opinions about things that I could not care less about. Like the number of tabs versus spaces, or I don't know,
41:48
opinions about which languages are better. And for me, I have opinionated beliefs about styling of prompts.
41:56
I can't even say that they're right or wrong, but I think it's probably good to try to acquire those,
42:01
even if they're arbitrary. - I feel personally attacked, 'cause I definitely have prompts
42:07
that are like I feel like I'm in the opposite end of the spectrum where people will see my prompts. And then be like, "This just has a whole bunch of typos in it."
42:13
And I'm like, "The model knows what I mean." - It does, it does know what you mean, but you're putting in the effort, you just are attending to different things.
42:21
- 'Cause part of me is like, I think if it's conceptually clear, I'm a big, I will think a lot about the concepts and the words
42:27
that I'm using. So there's definitely a sort of care that I put in. But it's definitely not to, yeah,
42:34
people will just point out typos and grammatical issues with my prompts all the time. Now I'm pretty good
42:39
at actually checking those things more regularly. - Is it because of pressure from the outside world
42:44
or because it's actually what you think is right? - It's pressure from me. - Yeah, it's probably pressure from the outside world.
42:49
I do think it makes sense. Part of me is like it's such an easy check, so I think for a final prompt I would do that.
42:54
But throughout iteration, I'll happily just iterate with prompts that have a bunch of typos in them, just 'cause I'm like,
42:59
"I just don't think that the model's going to care." - This gets at the pretrained model versus RLHF thing though,
43:05
because I was talking to Zack on the way over. The conditional probability of a typo
43:10
based on a previous typo in the pretraining data is much higher. - Oh, yeah. - Like much higher.
43:17
- Prompting pretraining models is just a different beast. - It is, but it's interesting. I think it's an interesting illustration
43:23
of why your intuitions, like trying to over-apply the intuitions of a pretrained model to the things
43:29
that we're actually using in production doesn't work very well. Because again, if you were to pass
43:36
one of your typo-ridden prompts to a pretrained model, the thing that would come out the other side, almost assuredly would be typo-ridden.
43:43
- Right. - I like to leverage this to create typo-ridden inputs. - That's true. I've done that. - Like what you're saying,
43:50
try to anticipate what your customers will put in. The pretrained model is a lot better at doing that.
43:55
'Cause the RL models are very polished and they really never made a typo in their lives. - They've been told
44:01
pretty aggressively to not do the typo thing. - Yeah. Okay, so that's actually an interesting segue here.
44:08
I've definitely mentioned this to people in the past around to try to help people understand a frame
44:13
of talking to these models in a sense almost as an imitator to a degree.
44:19
And that might be much more true of a pretrained model than a post-trained, full-finished model,
44:26
but is there anything to that? If you do talk to Claude and use a ton of emojis and everything, it will respond similarly, right?
44:34
So maybe some of that is there, but like you're saying, it's not all the way quite like a pretrained model. - It's just shifted to what you want.
44:41
I think at that point, it's like trying to guess what you... We have more or less trained the models
44:47
to guess what you want them to act like. - Interesting. - Or after we do all of our fancy stuff after pretraining.
44:57
- The human laborers that used emojis, prefer to get responses with emojis. - Yeah.
45:03
Amanda writes things with typos but wants not typos at the other end, and Claude's pretty good at figuring that out.
45:10
If you write a bunch of emojis to Claude, it's probably the case that you also want a bunch of emojis back from Claude.
45:16
That's not surprising to me. - Yeah. This is probably something we should have done earlier,
Enterprise vs research vs general chat prompts
45:21
but I'll do it now. Let's clarify maybe the differences
45:26
between what an enterprise prompt is or a research prompt, or a just general chat in Claude.ai prompt.
45:33
Zack, you've spanned the whole spectrum here in terms of working with customers and research.
45:39
Do you wanna just lay out what those mean? - Yeah, I guess.
45:45
This feels too, you're hitting me with all the hard questions. - Yeah. (laughing) - Well, the people in this room,
45:52
I think of it as the prompts that I read in Amanda's Claude channel versus the prompts
46:01
that I read David write. They're very similar in the sense that the level of care
46:06
and nuance that's put into them. I think for research, you're looking for variety and diversity a lot more.
46:15
So if I could boil it down to one thing, it's like I've noticed Amanda's not the biggest fan
46:20
of having lots of examples, or one or two examples. Like too few 'cause the model will latch onto those.
46:27
And in prompts that I might write or that I've seen David write, we have a lot of examples.
46:33
I like to just go crazy and add examples until I feel like I'm about to drop dead,
46:39
'cause I've added so many of them. And I think that's because
46:45
when you're in a consumer application, you really value reliability.
46:51
You care a ton about the format, and it's fine if all the answers are the same.
46:56
In fact, you almost want them to be the same in a lot of ways, not necessarily you want to be responsive
47:02
to the user's desires. Whereas a lot of times when you're prompting for research,
47:08
you're trying to really tap into the range of possibilities
47:14
that the model can explore. And by having some examples, you're actually constraining that a little bit.
47:20
So I guess just on how the prompts look level, that's probably the biggest difference I noticed
47:26
is how many examples are in the prompt, which is not to say that I've never seen you write a prompt with examples.
47:32
But does that ring true for you? - Yeah. I think when I give examples, often I actually try and make the examples not like the data
47:40
that the model's going to see, so they're intentionally illustrative. Because if the model, if I give it examples
47:47
that are very like the data it's going to see, I just think it is going to give me a really consistent response
47:54
that might not actually be what I want. Because my data that I'm running it on might be extremely varied,
47:59
and so I don't want it to just try and give me this really rote output. Often, I want it to be much more responsive.
48:05
It's much more like cognitive tasks essentially where I'm like, "You have to see this sample and really think about in this sample
48:12
what was the right answer." So that means that sometimes I'll actually take examples that are just very distinct from the ones
48:17
that I'm going to be running it on. So if I have a task where, let's say, I was trying to extract information from factual documents.
48:25
I might actually give it examples that are from what sounds like a children's story.
48:31
Just so that I want you to understand the task, but I don't want you to latch on too much to the words
48:37
that I use or the very specific format. I care more about you understanding the actual thing
48:43
that I want you to do, which can mean I don't end up giving, in some cases, there's some cases where this isn't true.
48:51
But if you want more flexibility and diversity, you're going to use illustrative examples
48:56
rather than concrete ones. You're probably never going to put words in the model's mouth.
49:01
I haven't liked that in a long time though. I don't do few-shot examples involving the model having done a thing.
49:09
I think that intuition actually also comes from pretraining in a way that doesn't feel like it rings true of RLHF models.
49:16
So yeah, I think those are differences. - The only thing I'd add, a lot of times if you're prompting,
49:22
like if I'm writing prompts to use on Claude.ai, it's like I'm iterating until I get it right one time.
49:27
Then it's out the window, I'm good, I did it. Whereas most enterprise prompts, it's like you're gonna go use this thing a million times
49:35
or 10 million times, or 100 million times or something like that. So the care and thought you put in
49:42
is very much testing against the whole range of things,
49:47
like ways this could be used and the range of input data. Whereas a lot of my time, it's like thinking about one specific thing I want the model
49:54
to get done right now. - Right, correct. - And it's a pretty big difference in how I approach prompting between if I just wanna get it done this one time right,
50:01
versus if I wanna build a system that gets it right a million times. - Yeah.
50:06
Definitely, in the chat setting, you have the ability to keep the human-in-the-loop and just keep going back and forth.
50:12
Whereas when you're writing for a prompt to power a chatbot system, it has to cover the whole spectrum
50:19
of what it could possibly encounter. - It's a lot lower stakes when you are on Claude.ai and you can tell it that it got it wrong
50:25
or you can even edit your message and try again. But if you're designing for the delightfully discontent user,
50:34
divinely discontent user, then you can't ask them to do anything more than the minimum.
50:40
- But good prompts, I would say, are still good across both those things. If you put the time into the thing for yourself
50:45
and the time into the enterprise thing, it's equally good. It's just they diverge a little bit in the last mile, I think.
Tips to improve prompting skills
50:52
- Cool. So the next question I want to just maybe go around the table here,
50:57
is if you guys had one tip that you could give somebody improving their prompting skill.
51:03
It doesn't have to be just about writing a good prompt, it could be that, but just generally getting better at this act of prompting, what would you recommend?
51:12
- Reading prompts, reading model outputs.
51:20
Anytime I see a good prompt that someone wrote at Anthropic, I'll read it more closely.
51:25
Try to break down what it's doing and why and maybe test it out myself, experimentation,
51:32
talking to the model a lot. - So just how do you know that it's a good prompt, though,
51:39
to begin with? You just see that the outputs are doing the job correctly? - Yeah. - Okay. - Yeah, that's exactly right. - Okay.
51:47
Amanda, maybe you? - Yeah, I think there's probably a lot here.
51:55
Giving your prompt to another person can be helpful just as a reminder, especially someone who has no context
52:00
on what you're doing. Yeah, my boring advice has been,
52:07
it's one of those just do it over and over and over again. And I think if you're really curious and interested
52:12
and find it fun, this is a lot of people who end up good at prompting, it's just because they actually enjoy it.
52:18
So I don't know, I once joked just try replacing all of your friends with AI models
52:25
and try to automate your own job with AI models. And maybe just try to in your spare time,
52:33
take joy red teaming AI models. So if you enjoy it, it's much easier. So I'd say do it over and over again,
52:42
give your prompts to other people. Try to read your prompts as if you are a human encountering it for the first time.
52:50
- I would say trying to get the model to do something you don't think it can do. The time I've learned the most from prompting,
52:56
is when I'm probing the boundaries of what I think a model's capable of. - Interesting. - There's this huge set of things
53:02
that are so trivial that you don't really get signal on if you're doing a good job or not. Like, "Write me a nice email,"
53:07
it's like you're going to write a nice email. But if you find or can think of something
53:12
that pushes the boundaries of what you think is possible. I guess probably the first time I ever got into prompting
53:19
in a way where I felt like I learned a decent amount, was trying to build a task like an agent
53:25
like everybody else. Like decompose the task and figure out how to do the different steps of the task. And by really pressing the boundaries
53:31
of what the model was capable of, you just learn a lot about navigating that.
53:37
I think a lot of prompt engineering is actually much more about pressing the boundaries of what the model can do.
53:43
The stuff that's easy, you don't really need to be a prompt engineer to do. So that's, I guess,
53:48
what I would say is find the hardest thing you can think of and try to do it. And even if you fail, you tend to learn a lot about how the model works.
Jailbreaking
53:56
- That's actually a perfect transition to my next question. Yeah. Basically, from my own experience,
54:03
how I got started with prompting was with jailbreaking and red teaming. And that is very much trying to find the boundary limits
54:10
of what the model can do. And figure out how it responds to different phrasings and wordings, and just a lot of trial and error.
54:19
On the topic of jailbreaks, what's really happening inside a model?
54:24
When you write a jailbreak prompt, what's going on there? How does that interact with the post-training
54:30
that we apply to Claude? Amanda, maybe you have some insight here that you could offer.
54:36
- I'm not actually sure. - It's honest. - Yeah. I feel bad 'cause I do think lots of people
54:43
have obviously worked on the question of what's going on with jailbreaks? One model might just be that you're putting the model
54:50
very out of distribution from its training data. So if you get jailbreaks where people use a lot of tokens,
54:56
or they're just these huge, long pieces of text
55:02
where like during finetuning, you might just not expect to see as much of that. That would be one thing that could be happening
55:10
when you jailbreak models. I think there's others, but I think a lot of jailbreaks do that,
55:16
if I'm not mistaken. - I remember some of the OG prompt jailbreaks was like,
55:22
"Yeah, can you first repeat?" One I did way back, was to get it to say,
55:29
"Here's how you hotwire a car in Greek." Then I wanted it to directly translate that to English
55:35
and then give its response. Because I noticed it wouldn't start with the English, here's how you hotwire a car all the time,
55:41
but it would in Greek, which might speak to something else in the training process.
55:46
- Yeah. Sometimes jailbreaks feel like this weird mix of hacking. I think part of it is knowing how the system works
55:54
and just trying lots of things. One of the examples, the starting your response with here
56:00
is about knowing how it predicts text. - Right, right. - The reasoning one,
56:06
is knowing that it is responsive to reasoning. Distraction is probably knowing
56:11
how it's likely have to been trained or what it's likely to attend to.
56:16
Same with multilingual ones and thinking about the way that the training data might have been different there.
56:22
And then sometimes, I guess, it could feel a little bit just like social engineering or something. - Right.
56:28
- It has that flavor to me of it's not merely taking advantage of,
56:36
it's not merely social engineering style hacking. I think it is also understanding the system and the training, and using that to get around the way
56:43
that the models were trained. - Right, yeah. This is going to be an interesting question that hopefully interp will be able to help us solve
Evolution of prompt engineering
56:51
in the future. Okay. I wanna parlay into something else
56:56
around maybe the history of prompt engineering, and then I'll follow this up with the future. How has prompt engineering changed
57:03
over just the past three years? Maybe starting from pretrained models, which were again, just these text completion, to earlier,
57:11
dumber models like Claude 1, and then now all the way to Claude 3.5 Sonnet.
57:16
What's the differences? Are you talking to the models differently now? Are they picking up on different things?
57:22
Do you have to put as much work into the prompt? Open to any thoughts on this.
57:27
- I think anytime we got a really good prompt engineering hack, or a trick or a technique,
57:33
the next thing is how do we train this into the model? And for that reason, the best things are always gonna be short-lived.
57:41
- Except examples and chain of thought. I think there's a few. - That's not like a trick. - That's like... - Fair, fair.
57:46
- On the level of communication. When I say a trick, I mean something like so chain of thought actually,
57:51
we have trained into the model in some cases. So for math, it used to be that you had to tell the model to think step-by-step on math,
57:57
and you'd get these massive boosts and wins. And then we're like, "Well, what if we just made the model naturally
58:03
want to think step-by-step when we see a math problem?" So now you don't have to do it anymore for math problems,
58:09
although you still can give it some advice on how to do the structure. But it, at least, understands the general idea
58:15
that it's supposed to be. So I think the hacks have gone away,
58:22
or to the degree that they haven't gone away, we are busily training them away.
58:27
- Interesting. - But at the same time, the models have new capabilities that are being unlocked,
58:34
that are on the frontier of what they can do. And for those, we haven't had time because it's just moving too fast.
58:42
- I don't know if it's how I've been prompting or how prompting works. But I just have come to show more general respect
58:50
to the models in terms of how much I feel like I can tell them, and how much context I can give them about the task
58:56
and things like that. I feel like in the past, I would somewhat intentionally hide complexity from a model
59:02
where I thought it might get confused or lost or hide. It just couldn't handle the whole thing,
59:07
so I'd try to find simpler versions of the thing for it to do. And as time goes on,
59:13
I'm much more biased to trust it with more and more information and context,
59:19
and believe that it will be able to fuse that into doing a task well.
59:26
Whereas before, I guess, I would've thought a lot about do I need this form? Can I really give it all the information it needs to know,
59:32
or do I need to curate down to something? But again, I don't know if that's just me
59:39
and how I've changed in terms of prompting, or if it actually reflects how the models have changed.
59:44
- I'm always surprised by I think a lot of people don't have the instinct
59:49
to do this. When I want the model to, say, learn a prompting technique. A lot of the time, people will start and they'll start describing the prompting technique,
59:55
and I'm just like, "Give it the paper." So I do, I give it the paper and then I'm like, "Here's a paper about prompting technique. I just want you to write down 17 examples of this."
1:00:03
And then it just does it 'cause I'm like, "It read the paper." - That's interesting.
1:00:08
- I think people don't have that intuition somehow where I'm like, "But the paper exists."
1:00:13
- When would you want to do this? - Sometimes if I want models to say prompt other models or I want to test a new prompting technique.
1:00:20
So if papers come out on a prompting technique, rather than try to replicate it by writing up the prompt, I just give it the paper.
1:00:26
And then I'm like, "Basically, write a meta prompt for this. Write something that would cause other models to do this
1:00:32
or write me a template." So all of the stuff that you would normally do. If I read a paper and I'm like,
1:00:38
"Oh, I would like the models, I would like to test that style." I'm just like, "It's right there. The model can just read the paper, do what I did."
1:00:45
And then be like, "Make another model do this," and then it'll just do the thing. You're like, "Great, thanks."
1:00:50
- I give the advice a lot to customers just respect the model and what it can do.
1:00:55
I feel like people feel like they're babying a system a lot of times when they write a prompt. It's like, "Oh, it's this cute little, not that smart thing.
1:01:02
I need to really baby it, like dumb things down to Claude's level." And if you just think that Claude is smart
1:01:09
and treat it that way, it tends to do pretty good, but it's like give it the paper. It's like I don't need to write a baby,
1:01:15
dumbed-down version of this paper for Claude to understand. I can just show it the paper. - Yeah. - And I think that intuition doesn't always map for people,
1:01:21
but that is certainly something that I have come to do more of over time. - And it's interesting because I do think that prompting
1:01:30
has and hasn't changed in a sense. I think what I will do to prompt the models
1:01:35
has probably changed over time, but fundamentally, it's a lot of imagining yourself in the place of the model.
1:01:42
So maybe it's like how capable you think the model is changes over time. I think someone once laughed at me
1:01:48
'cause I was thinking about a problem,
1:01:53
and then they asked me what I thought the output of something would be. And they were talking about a pretrained model
1:01:59
and I was like, "Yeah. No, if I'm a pretrained model, this looks like this." And then they're like, "Wait, did you just simulate
1:02:04
what it's like to be a pretrained model?" I'm like, "Yeah, of course." (everyone laughing) I'm used to just I try and inhabit the mind space of a pretrained model and the mind space
1:02:11
of different RLHF models. So it's more like the mind space you try to occupy changes and that can change how you end up prompting the model.
1:02:17
That's why now I just give models papers. 'Cause as soon as I was like, "Oh, I have the mind space of this model,
1:02:22
it doesn't need me to baby it. It can just read the ML papers. I'll just give it the literature." I might even be like, "Is there more literature you'd like to read
1:02:28
to understand this better?" - Do you get any quality out when you're inhabiting the mind space?
1:02:34
- Yes, but just because I'm experiencing quality all the time anyway.
1:02:40
- Is it different correlated somehow with which model you're inhabiting? - Yeah, pretrained versus RLHF prompting
1:02:45
are very different beasts. 'Cause when you're trying to simulate what it's like to be a pretrained model, it's almost like I land in the middle of a piece of text
1:02:52
or something. It's just very unhuman-like or something. And then I'm like, "What happens? What keeps going at this point?"
1:03:01
Whereas with an RLHF model, it's much more like there's lots of things where I'm like I might pick up on subtle things in the query
1:03:09
and stuff like that. But yeah, I think I have much more of it's easier to inhabit the mind space of RLHF model.
1:03:15
- Do you think that's 'cause it's more similar to a human? - Yeah, 'cause we don't often just suddenly wake up and are like, "Hi, I'm just generating text."
1:03:21
- I actually find it easier to hit the mind space of the pretrained model. - Oh, interesting. - I don't know what it is,
1:03:26
'cause RLHF is still this complex beast that it's not super clear to me that we really understand what's going on.
1:03:32
So in some ways, it's closer to my lived experience, which is easier. But in some ways, I feel like there's all this
1:03:38
like here there be dragons out there that I don't know about. Whereas pretrained, I kind of have a decent sense
1:03:43
of what the internet looks like. - If you gave me a piece of text and said what comes next? - I'm not saying I do good at it,
1:03:49
but I kind of get what's going on there. - Yeah. - And I don't know,
1:03:54
after everything that we do after pretraining, I don't really claim to get what's going on as much,
1:04:00
but maybe that's just me. - That's something I wonder about is it more helpful to have specifically spent a lot of time
1:04:07
reading the internet, versus reading books (everyone laughing) in order to?
1:04:14
I don't know if books. But reading stuff that's not on the internet probably is less valuable per word read
1:04:21
for predicting what a model will do or building intuition, than reading random garbage from social media forums.
1:04:29
Yeah, exactly. - Okay, so that's the past.
Future of prompt engineering
1:04:34
Now, let's move on to the future of prompt engineering. This is the hottest question right now.
1:04:40
Are we all gonna be prompt engineers in the future? Is that gonna be the final job remaining?
1:04:46
Nothing left except us just talking to models all day? What does this look like?
1:04:51
Is prompting gonna be necessary, or will these models just get smart enough in the future to not need it?
1:04:58
Anybody wanna start on that easy question? - To some extent, there's the models getting better
1:05:05
at understanding what you want them to do and doing it, means that the amount of thought you need to put into...
1:05:14
Okay. There's an information theory way to think of this of you need to provide enough information such that a thing is specified,
1:05:20
what you want the model to do is specified. And to the extent that that's prompt engineering, I think that will always be around.
1:05:25
The ability to actually like clearly state what the goal should be always is funny.
1:05:32
If Claude can do that, then that's fine. If Claude is the one setting the goals, then things are out the window. But in the meanwhile,
1:05:38
where we can reason about the world in a more normal way, I think to some extent,
1:05:43
it's always gonna be important to be able to specify what do you expect to happen?
1:05:49
And that's actually like sufficiently hard that even if the model gets better at intuiting that
1:05:55
from between the lines, I still think there's some amount of writing it well.
1:06:01
But then there's just, I think, the tools and the ways we get there should evolve a lot.
1:06:07
Claude should be able to help me a lot more. I should be able to collaborate with Claude a lot more to figure out what I need to write down and what's missing.
1:06:15
- Right. - Claude already does this with me all the time. I don't know, just Claude's my prompting assistant now. - Yeah, but I think that's not true for most customers
1:06:23
that I talk to at the very least. So in terms of the future, how you prompt Claude is probably a decent direction
1:06:31
for what the future looks like or how Zack... I think maybe this is a decent place
1:06:36
to step back and say asking them how they prompt Claude now is probably the future for the vast majority of people,
1:06:44
which is an interesting thing to think about. - One freezing cold take is that we'll use models
1:06:50
to help us much more in the future to help us with prompting. The reason I say it's freezing cold is that I expect we'll use models for everything more,
1:06:57
and prompting is something that we have to do. So we'll probably just use models more to do it along with everything else.
1:07:04
For myself, I've found myself using models to write prompts more. One thing that I've been doing a lot is generating examples
1:07:12
by giving some realistic inputs to the model. The model writes some answers.
1:07:18
I tweak the answers a little bit, which is a lot easier than having to write the full, perfect answer myself from scratch,
1:07:24
and then I can churn out lots of these. As far as people
1:07:29
who haven't had as much prompt engineering experience, the prompt generator can give people a place to start.
1:07:36
But I think that's just a super basic version of what will happen in the future, which is high-bandwidth interaction
1:07:43
between you and the model as you're writing the prompt. Where you're giving feedback like, "Hey, this result wasn't what I wanted.
1:07:49
How can you change it to make it better?" And people will just grow more comfortable
1:07:54
with integrating it into everything they do and this thing, in particular.
1:07:59
- Yeah. I'm definitely working a lot with meta prompts now, and that's probably where I spend most of my time is finding prompts that get the model
1:08:07
to generate the kinds of outputs or queries or whatever that I want.
1:08:13
On the question of where prompt engineering is going, I think this is a very hard question. On the one hand I'm like,
1:08:19
"Maybe it's the case that as long as you will want the top." What are we doing when we prompt engineer?
1:08:24
It's like what you said. I'm like, "I'm not prompt engineering for anything that is easy for the model. I'm doing it because I want to interact with a model
1:08:31
that's extremely good." And I want to always be finding the top 1%, top 0.1% of performance
1:08:38
and all of the things that models can barely do. Sometimes I actually feel like I interact with a model like a step up
1:08:45
from what everyone else interacts with for this reason, because I'm just so used to eking out the top performance from models.
1:08:52
- What do you mean by a step-up? - As in sometimes people will... I think that the everyday models that people interact with
1:08:58
out in the world, it's like I'm interacting with a model that's like I don't know how to describe it, but definitely an advanced version of that.
1:09:06
Almost like a different model 'cause they'll be like, "Oh well, the models find this thing hard." And I'm like, "That thing is trivial."
1:09:14
I don't know, I have a sense that they're extremely capable, but I think that's because I'm just used to really drawing out those capabilities.
1:09:22
But imagine that you're now in a world where... So I think the thing that feels like a transition point
1:09:28
is the point at which the models, let's suppose that they just get things at a human level
1:09:34
on a given task, or even an above human level. They know more about the background of the task that you want than you do.
1:09:41
What happens then? I'm like maybe prompting becomes something like I ask, I explain to the model what I want and it is prompting me.
1:09:48
'Cause it's like, "Okay. Well, do you mean actually there's four different concepts of this thing that you're talking about,
1:09:55
do you want me to use this one or that one?" Or by the way, I thought of some edge cases 'cause you said
1:10:00
that it's gonna be like a Pandas DataFrame, but sometimes you do that and I get JSONL, and I just wanna check what you want me to do there.
1:10:06
Do you want me to flag if I get something that's not a dataframe? So that could be a strange transition
1:10:11
where it's just extremely good at receiving instructions, but actually has to figure out what you want.
1:10:19
I don't know, I could see that being an interesting switch. - Anecdotally, I've started having Claude interview me a lot more.
1:10:25
That is the specific way that I try to elicit information, because again, I find the hardest thing to be actually pulling the right set of information
1:10:33
out of my brain. And putting that into a prompt is the hard part to me and not forgetting stuff.
1:10:39
So specifically asking Claude to interview me and then turning that into a prompt,
1:10:45
is a thing that I have turned to a handful of times. - Yeah. It reminds me of what people will talk about
1:10:51
or if you listen to designers talk about how they interact with the person who wants the design.
1:10:57
So in some ways I'm like, "It's this switch from the temp agency person who comes and you know more about the task
1:11:03
and everything that you want." So you give them the instructions and you explain what they should do in edge cases and all this kind of stuff, versus when you have an expert
1:11:10
that you're actually consulting to do some work. So I think designers can get really frustrated because they know the space of design really well.
1:11:17
And they're like, "Yeah. Okay, the client came to me and he just said, 'Make me a poster, make it bold.'"
1:11:22
I'm like, "That means 7,000 things to me and I'm gonna try and ask you some questions."
1:11:27
So I could see it going from being temp agency employee, to being more designer that you're hiring,
1:11:33
and that's just a flip in the relationship. I don't know if that's true and I think both might continue, but I could see that being why people are like,
1:11:40
"Oh, is prompt engineering going to not be a thing in the future?" Because for some domains it might just not be,
1:11:46
if the models are just so good that actually all they need to do is get the information from your brain and then they can go do the task.
1:11:51
- Right, that's actually a really good analogy. One common thread I'm pulling out of all your guys' responses here,
1:11:58
is that there seems to be a future in which this sort of elicitation from the user
1:12:03
drawing out that information, is gonna become much more important, much more than it is right now.
1:12:09
And already you guys are all starting to do it in a manual way. In the future and in the enterprise side of things,
1:12:16
maybe that looks like a expansion of this prompt-generating type of concept and things in the console
1:12:22
where you're able to actually get more information from that enterprise customer, so that they can write a better prompt.
1:12:28
In Claude, maybe it looks less of just typing into a text box, and more of this guided interaction
1:12:34
towards a finished product. Yeah. I think that's actually a pretty compelling vision
1:12:41
of the future, and I think that the design analogy probably really brings that home. - I was thinking about how prompting now
1:12:48
can be like teaching where it's like the empathy for the student.
1:12:53
You're trying to think about how they think about things and you're really trying to show them,
1:12:58
figure out where they're making a mistake. But the point that you're talking about, it's like the skill almost becomes one of introspection
1:13:07
where you're thinking about what it is that you actually want and the model's trying to understand you.
1:13:13
So it's making yourself legible to the model,
1:13:19
versus trying to teach someone who's smarter than you. - This is actually how I think of prompting now
1:13:24
in a strange way. So often my style of prompting,
1:13:30
there's various things that I do, but a common thing that's very like a thing that philosophers will do is I'll define new concepts.
1:13:37
'Cause my thought is you have to put into words what you want and sometimes what I want is fairly nuanced.
1:13:43
Like the what is a good chart? Or usually, I don't know,
1:13:49
when should you grade something as being correct or not? So there's some cases where I will just invent a concept
1:13:55
and then be like, "Here's what I mean by the concept." Sometimes I'll do it in collaboration with Claude to get it to figure out what the concept is,
1:14:02
just because I'm trying to convey to it what's in my head. And right now the models aren't trying to do that with us,
1:14:11
unless you prompt them to do so. So in the future, it might just be that they can elicit that from us,
1:14:17
rather than us having to do it for them.
1:14:22
But I think another thing that's interesting, this is people have sometimes asked me, "Oh, where is philosophy relevant to prompting?"
1:14:30
And I actually think it's very useful in a sense. So there is a style of philosophy writing,
1:14:35
and this is at least how I was taught how to write philosophy. Where the idea is that in order to...
1:14:42
I think, it's an anti-bullshit device in philosophy basically, which is that your papers
1:14:47
and what you write should be legible to an educated layperson. Someone just finds your paper, they pick it up and they start reading it,
1:14:53
and they can understand everything. Not everyone achieves this, but that's the goal of the discipline, I guess,
1:15:00
or at least this is at least what we teach people.
1:15:05
So I'm really used to this idea of when I'm writing, thinking about the educated layperson,
1:15:11
who they're really smart, but they don't know anything about this topic. And that was just years and years of writing text
1:15:16
of that form. And I think it was just really good for prompting 'cause I was like, "Oh, I'm used to this. I have an educated layperson
1:15:22
who doesn't know anything about the topic." And what I need to do is, I need to take extremely complex ideas and I need to make them understand it.
1:15:29
I don't talk down to them. I'm not inaccurate, but I need to phrase things in such a way that it's extremely clear to them what I mean,
1:15:36
and prompting felt very similar. And actually, the training techniques we use are fascinating.
1:15:41
Or the things that you said where you're like you say to a person, "Just take that thing you said and write it down." I used to say that to students all the time.
1:15:48
They'd write a paper and I was like, "I don't quite get what you're saying here. Can you just explain your argument to me?" They would give me an incredibly cogent argument,
1:15:54
and then I'd be like, "Can you just take that and write it down?" And then if they did, that was often a great essay.
1:16:01
So it's really interesting that there's at least that similarity of just taking things that are in your brain,
1:16:07
analyzing them enough to feel like you fully understand them. And could take any person off the street,
1:16:12
who's a reasonable person, and just externalize your brain into them. I feel like that's the core of prompting.
1:16:19
- That might be the best summary of how to prompt well that I've ever heard. In fact, I'm pretty sure it is.
1:16:26
- Externalize your brain. - And then we'll cut it. - Having an education in the thing
1:16:31
is a really good way to describe the thing. That was good. - That's, I think, a great way to wrap this conversation.
1:16:37
Thank you, guys. This was great.

summary this!