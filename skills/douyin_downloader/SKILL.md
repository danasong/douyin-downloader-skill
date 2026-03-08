# douyin_downloader

## Purpose

Provide a practical OpenClaw skill wrapper for downloading Douyin videos from share links through a local downloader script.

提供一个面向 OpenClaw 的实用 skill，用于通过本地下载脚本处理抖音分享链接并下载视频。

## When to use / 何时使用

Use this skill when:
- the user provides a Douyin share link
- the user asks to download a Douyin video
- the workflow needs local video download plus basic metadata extraction

以下场景适合启用：
- 用户提供抖音分享链接
- 用户要求下载抖音视频
- 工作流需要本地下载并返回基础元信息

## Inputs / 输入

- Douyin share URL / 抖音分享链接
- Optional output directory / 可选输出目录

## Outputs / 输出

- Local file path / 本地文件路径
- Basic metadata / 基础元信息
- Structured execution result / 结构化执行结果

## Workflow / 工作流程

1. Validate the provided URL / 校验输入链接
2. Invoke the local downloader script / 调用本地下载器脚本
3. Resolve media resource and metadata / 解析视频资源与元信息
4. Save files locally / 将文件保存到本地
5. Return structured results / 返回结构化结果

## Boundaries / 边界

- No embedded credentials / 不内置任何凭据
- No guarantee for every unsupported or expired link / 不保证对所有失效或异常链接都成功
- No commercial usage rights granted by this repository license / 本仓库协议不授予商用权利
