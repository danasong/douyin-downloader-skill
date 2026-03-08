# Douyin Downloader Skill

This repository provides a public-friendly OpenClaw skill example for handling Douyin share links through a local downloader workflow.

## Project Positioning

This is not a flashy mock repository. It is a practical, documented skill wrapper for a real local workflow: ingesting Douyin share URLs, invoking a local downloader script, collecting metadata, and returning structured results for downstream automation.

It is useful for:
- people integrating Douyin download capability into agent workflows
- teams wanting a clean public repository template for a media skill
- builders who want to chain download results into captioning, analysis, or archival pipelines

## Core Capabilities

- Accept Douyin share links
- Invoke a local downloader script
- Download watermark-free video when supported by the local workflow
- Extract basic metadata such as title, author, and video id
- Return structured results for follow-up automation

## Boundaries

This repository does not pretend to provide:
- an official Douyin API
- guaranteed success for every possible link format
- a hosted cloud service
- embedded credentials, cookies, or private tokens

## Suggested Repository Layout

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

## Typical Integration Flow

1. User provides a Douyin share link
2. The skill validates the input
3. A local downloader script is invoked
4. The script resolves the real media resource
5. Metadata is extracted and files are saved locally
6. Structured results are returned to the calling agent or automation layer

## Use Cases

- personal media archiving
- asset collection workflows
- automated download pipelines
- downstream captioning, review, and media organization

## Documentation

- Bilingual landing page: [README.md](./README.md)
- Chinese documentation: [README.zh-CN.md](./README.zh-CN.md)
- Skill definition: [skills/douyin_downloader/SKILL.md](./skills/douyin_downloader/SKILL.md)
- Skill notes: [skills/douyin_downloader/README.md](./skills/douyin_downloader/README.md)

## License

This repository allows viewing, studying, and modification for personal or internal use, but **commercial use is prohibited**. See [LICENSE](./LICENSE).
