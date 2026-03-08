# douyin_downloader Skill Notes

## Overview / 概述

`douyin_downloader` is a focused media utility skill for OpenClaw. It is designed to connect user-provided Douyin share links with a local downloader execution path.

`douyin_downloader` 是一个聚焦媒体处理的 OpenClaw skill，用来把用户提供的抖音分享链接接入本地下载执行链路。

## Responsibilities / 责任范围

- Validate incoming Douyin links / 校验传入的抖音链接
- Call a local downloader implementation / 调用本地下载实现
- Normalize returned metadata / 规范化返回元信息
- Produce output suitable for automation / 产出适合自动化继续处理的结果

## Recommended downstream actions / 推荐下游动作

- subtitle extraction / 提取字幕
- keyframe generation / 关键帧生成
- content review / 内容审阅
- media archive organization / 媒体归档整理

## Public repository notes / 公开仓库说明

This repository intentionally excludes secrets, cookies, tokens, and private execution context.

本仓库有意排除了密钥、Cookie、Token 以及任何私有执行上下文，适合公开展示与学习参考。
