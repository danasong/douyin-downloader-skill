# douyin_downloader

## Purpose / 定位

Provide a practical OpenClaw skill wrapper for downloading Douyin videos from share links through a **local private downloader script**.

这是一个面向 OpenClaw 的实用型抖音下载 skill，用于通过**本地私有下载脚本**处理抖音分享链接、下载视频并返回结构化结果。

它的目标不是公开下载器源码，而是把：
- 触发条件
- 调用流程
- 输出结构
- 使用边界

明确写进 skill 本体，让执行逻辑稳定、可复用、可维护。

---

## When to use / 何时使用

Use this skill when:
- the user provides a Douyin share link
- the user asks to download a Douyin video
- the user asks to save a Douyin video locally
- the workflow needs local download plus title/author/video ID extraction

以下场景适合启用：
- 用户提供抖音分享链接
- 用户明确要求“下载抖音视频”
- 用户说“保存这个视频”并附带抖音链接
- 工作流需要本地下载，并返回标题、作者、视频 ID 等基础元信息

---

## Trigger Rules / 触发规则

Trigger this skill when any of the following is true:

- the message contains `douyin.com`
- the message contains `v.douyin.com`
- the user explicitly asks for Douyin video download
- the task requires saving a Douyin video to a local directory

满足以下任一条件时启用：
- 消息中包含 `douyin.com`
- 消息中包含 `v.douyin.com`
- 用户明确要求下载抖音视频
- 任务要求把抖音视频保存到本地目录

---

## Private Implementation Rule / 私有实现铁律

### Core Rule / 核心铁律

This skill must use the following **private local script** as its primary execution backend:

此 skill 执行时，默认必须优先调用以下**私有本地脚本**：

```bash
/Users/jacksong/.openclaw/workspace/douyin_downloader.py
```

### Important / 重要说明

- This script is a **private implementation**
- It is allowed for local execution in the owner's environment
- It must **not** be published into public GitHub repositories, public skill repositories, or public-facing documentation as source code

- 该脚本属于**私有实现**
- 允许在主人本机环境中本地调用
- **绝对不允许**把该脚本源码公开发布到 GitHub、公开 skill 仓库或对外文档中

### Public Repository Rule / 公开仓库规则

In public repositories, this skill may describe:
- the capability
- the workflow
- the expected inputs and outputs
- the integration pattern

But it must not expose:
- the private script source code
- private environment coupling details beyond the minimum required path note
- secrets, cookies, sessions, or credentials

公开仓库里可以写：
- 功能能力
- 工作流程
- 输入输出结构
- 接入方式

但不能公开：
- 私有脚本源码本体
- 超出必要范围的私有环境耦合细节
- 密钥、Cookie、Session、凭据

---

## Inputs / 输入

Required:
- Douyin share URL / 抖音分享链接

Optional:
- Output directory / 输出目录

Default output directory:

```bash
~/Desktop/视频下载/
```

---

## Outputs / 输出

The skill should return:
- local file path / 本地文件路径
- title / 标题
- author / 作者
- video ID / 视频 ID
- size / 文件大小
- structured execution result / 结构化执行结果

If the local script returns JSON-like result payload, preserve and reuse it.

如果本地脚本输出结构化 JSON 结果，应优先直接复用。

---

## Execution Workflow / 执行流程

### Standard Flow / 标准流程

1. Validate the provided Douyin URL  
   校验用户提供的抖音链接
2. Decide output directory  
   确定输出目录（默认 `~/Desktop/视频下载/`）
3. Invoke the private local downloader script  
   调用私有本地下载脚本
4. Parse returned metadata and file path  
   解析返回的文件路径与元信息
5. Confirm local download success  
   确认下载结果
6. Return structured result to the user  
   向用户返回结构化结果
7. Optionally propose next-step actions  
   按需建议后续操作

### Invocation Command / 调用命令

```bash
python3 /Users/jacksong/.openclaw/workspace/douyin_downloader.py "抖音分享链接" [输出目录]
```

### Recommended Post-actions / 推荐后续动作

After a successful download, the assistant may ask whether the user wants:
- keyframe extraction / 提取关键帧
- subtitle or transcript generation / 转录字幕
- upload or archive workflow / 上传或归档
- content analysis / 内容分析

---

## Planning and Delivery Logic / 规划与交付逻辑

This skill should not stop at “download succeeded”. It should treat the download as part of a larger workflow.

这个 skill 不应只停留在“下载成功”，而应把下载视为更大工作流中的一个节点。

### Decision Flow After Receiving a Douyin Link / 收到抖音链接后的决策流程

When a user sends a Douyin link, the assistant should follow this sequence instead of jumping straight into download.

当用户发来抖音链接时，助手不应一上来就直接下载，而应按以下顺序判断：

#### Step 1 / 第一步：先确认用户意图
Ask or infer what the user actually wants:
- download the video / 下载视频
- parse the content / 解析内容
- analyze and learn from the content / 分析学习内容
- do all of the above / 全部都做

优先确认或判断用户真正要的是：
- 下载视频
- 解析内容
- 分析学习
- 还是全部都做

Recommended quick reply style:

```text
收到抖音链接后，可优先确认：
1. 是否下载？
2. 是否解析内容？
3. 是否分析学习？
```

#### Step 2 / 第二步：如果用户要下载
If the user clearly wants download:
1. invoke the private local downloader script
2. return local file path + metadata
3. ask whether follow-up processing is needed

如果用户明确要下载：
1. 调用私有本地下载脚本
2. 返回本地路径 + 元信息
3. 再询问是否需要后续处理

#### Step 3 / 第三步：如果用户要解析
If the user wants parsing instead of direct download:
- extract title, author, video ID, topic, and visible page text when possible
- summarize what the content is about
- identify whether it points to a tool, project, workflow, or opinion

如果用户要解析：
- 提取标题、作者、视频 ID、主题、页面可见文本
- 总结视频内容在讲什么
- 识别它是在介绍工具、项目、流程还是观点

#### Step 4 / 第四步：如果用户要“分析学习”
If the user wants learning or analysis:
- summarize the key idea
- explain the real value behind the content
- distinguish marketing language from actual engineering value
- suggest how it can be adapted into the user's own workflow or skill system

如果用户要“分析学习”：
- 提炼核心观点
- 分析真正价值点
- 区分宣传话术和实际工程价值
- 给出如何接入用户自身工作流 / skill 体系的建议

#### Step 5 / 第五步：如果用户没说清楚
If the user only sends a link and the intent is unclear:
- do not assume download immediately
- ask a short clarification question first
- default clarification options: download / parse / analyze

如果用户只是发了链接但没说明需求：
- 不要默认立刻下载
- 优先用一句短问句澄清
- 默认澄清选项：下载 / 解析 / 分析学习

Recommended clarification format:

```text
这条抖音你想让我：
1. 直接下载
2. 先解析内容
3. 做分析学习
4. 全部处理
```

### Planning Layer / 规划层

When a Douyin link is received, the skill should think in this order:

1. What does the user really want first: download, parse, analyze, or all?  
   用户第一诉求到底是下载、解析、分析，还是全都要？
2. Is the user only asking for the raw video file?  
   用户是不是只要原视频文件？
3. Does the user likely want follow-up processing?  
   用户是否大概率还需要后处理？
4. Should the result be returned as local file only, or also prepared for downstream workflows?  
   结果是否只需本地交付，还是需要为后续流程做准备？

### Delivery Layer / 交付层

A good delivery should include:
- whether download succeeded / 是否下载成功
- where the file is saved / 文件保存位置
- what the title/author/video ID are / 标题、作者、视频 ID
- what can be done next / 下一步还能做什么

Recommended final delivery format:

```text
✅ 下载完成
- 标题：...
- 作者：...
- 视频ID：...
- 路径：...
- 大小：...

如需，我可以继续帮你：提取关键帧 / 转字幕 / 做内容分析
```

---

## Failure Handling / 失败处理

If download fails, the skill should clearly distinguish the cause when possible:

- invalid share link / 链接无效
- video ID not resolved / 无法提取视频 ID
- media URL not resolved / 无法解析视频地址
- target download blocked / 下载被限制
- file write error / 文件写入失败

Recommended failure reply structure:

```text
❌ 下载失败
- 原因：...
- 链接：...
- 建议：重新提供分享链接 / 更换目录 / 稍后重试
```

---

## Boundaries / 边界

- No embedded credentials / 不内置任何凭据
- No public release of the private downloader script / 不公开私有下载脚本源码
- No guarantee for every unsupported, expired, or blocked link / 不保证对所有失效或受限链接都成功
- No commercial usage rights granted by this repository license / 本仓库协议不授予商用权利

---

## Summary / 一句话总结

This skill is a **public-safe wrapper around a private local Douyin downloader implementation**.

这个 skill 本质上是：

**一个围绕私有本地抖音下载器构建的公开安全包装层。**

公开的是：工作流、能力边界、触发规则、输入输出。  
不公开的是：私有脚本本体。
