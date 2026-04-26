# TikTok Reach

TikTok Reach is a Codex skill for browsing public Douyin video share links. It helps an agent parse video metadata, extract visible text or captions, summarize the content, and optionally fetch a no-watermark download link when needed.

## What It Does

- Parses Douyin share links such as `https://v.douyin.com/...`
- Extracts video title, creator, publish time, captions, and visible text when available
- Summarizes the video content in the user's language
- Produces concise key points for products, claims, locations, prices, dates, and calls to action
- Uses Agent Reach's Douyin tools instead of hardcoded scraping logic

## Requirements

This skill expects the local Codex environment to have `agent-reach` and its Douyin MCP channel available.

The main commands used by the skill are:

```bash
mcporter call 'douyin.parse_douyin_video_info(share_link: "https://v.douyin.com/xxx/")'
mcporter call 'douyin.extract_douyin_text(share_link: "https://v.douyin.com/xxx/")'
mcporter call 'douyin.get_douyin_download_link(share_link: "https://v.douyin.com/xxx/")'
```

## Example Prompts

```text
帮我看一下这个抖音视频讲了什么 https://v.douyin.com/xxx/
```

```text
提取这个抖音里的文案和重点
```

```text
这个抖音视频有没有无水印下载链接？
```

```text
批量总结这几个抖音链接
```

## Notes

- Public Douyin share links usually do not require login.
- The skill avoids guessing visual details unless they appear in metadata, extracted text, or inspected media.
- If the Douyin channel is unavailable, check `agent-reach doctor` or `mcporter_list_servers()`.
