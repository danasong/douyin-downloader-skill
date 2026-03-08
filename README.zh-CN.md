# 抖音下载 Skill

这是一个面向 OpenClaw 的抖音下载 skill 示例仓库，聚焦于**抖音分享链接接入、本地下载脚本调用、无水印视频获取、基础元信息抽取，以及结果回传**。

## 项目定位

这个仓库不是在做“花哨但不可落地”的展示，而是把一个真实可执行的本地下载流程，整理成适合公开发布、可复用、可二次集成的 skill 结构。

它适合：
- 想把抖音下载能力接入 agent 工作流的人
- 需要一个公开、安全、文档完整的 skill 仓库模板的人
- 想把视频下载结果继续用于转录、整理、归档的人

## 核心能力

- 接收抖音分享链接
- 调用本地下载器脚本执行解析与下载
- 在工作流支持的前提下获取无水印视频
- 提取标题、作者、视频 ID 等基础信息
- 以结构化形式返回执行结果，方便下游自动化继续处理

## 能力边界

本仓库不会虚构以下能力：
- 不声称是官方 API
- 不承诺所有链接都一定成功
- 不提供云端托管服务
- 不内置任何账号、Cookie、Token 或私有凭据

## 推荐仓库结构

```text
.
├── README.md
├── README.zh-CN.md
├── README.en.md
├── LICENSE
└── skills/
    └── douyin_downloader/
        ├── SKILL.md
        └── README.md
```

## 典型接入思路

1. 用户提供抖音分享链接
2. Skill 层做输入校验
3. 调用本地下载脚本
4. 脚本解析真实视频资源地址
5. 提取视频元信息并保存文件
6. 返回结构化结果给上层 agent 或自动化系统

## 适用场景

- 个人内容归档
- 素材收集
- 自动化下载任务
- 与字幕提取、内容分析、媒体整理联动

## 文档入口

- 双语首页：[README.md](./README.md)
- English: [README.en.md](./README.en.md)
- Skill 定义：[skills/douyin_downloader/SKILL.md](./skills/douyin_downloader/SKILL.md)
- Skill 说明：[skills/douyin_downloader/README.md](./skills/douyin_downloader/README.md)

## 协议说明

本仓库允许查看、学习、修改，但**不允许商用**。详见 [LICENSE](./LICENSE)。
