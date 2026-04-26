---
name: tiktok-reach
description: Parse Douyin/TikTok China share links and summarize video content using Agent Reach Douyin tools. Use when the user provides a Douyin share URL, v.douyin.com short link, douyin.com video link, or asks to browse, parse, read, summarize, extract text from, or get metadata/download links for Douyin videos.
---

# TikTok Reach

## Quick Start

Use the Douyin channel from `agent-reach` first. It does not require login for public share links.

```bash
mcporter call 'douyin.parse_douyin_video_info(share_link: "https://v.douyin.com/xxx/")'
mcporter call 'douyin.extract_douyin_text(share_link: "https://v.douyin.com/xxx/")'
mcporter call 'douyin.get_douyin_download_link(share_link: "https://v.douyin.com/xxx/")'
```

## Workflow

1. Normalize the input into a single Douyin share URL.
   - Accept `v.douyin.com`, `www.douyin.com`, copied share text containing a URL, or plain video links.
   - If the user gives multiple links, process them one at a time and label each result.
2. Parse metadata with `douyin.parse_douyin_video_info`.
3. Extract visible/caption text with `douyin.extract_douyin_text`.
4. Fetch the download URL with `douyin.get_douyin_download_link` only when the user asks for download/no-watermark media or when media inspection is necessary.
5. Summarize the content in the user's language.

## Output Shape

Prefer concise structured output:

- `标题`: video title or caption headline when available
- `作者`: creator/account when available
- `发布时间`: publish time when available
- `视频内容`: short summary of what happens in the video
- `文案/字幕`: extracted text, cleaned and deduplicated
- `关键点`: 3-5 bullets for useful facts, claims, products, locations, or calls to action
- `链接`: original share URL and download URL only if requested or needed

If a field is missing from the tool output, omit it instead of guessing.

## Reliability Rules

- Do not claim visual details that are not present in metadata, extracted text, or inspected media.
- Treat copied Douyin share text as noisy: extract the first Douyin URL before calling tools.
- Preserve important numbers, names, prices, locations, and dates exactly as returned.
- If the short link fails, try the expanded `douyin.com` URL when available.
- If the Douyin tools fail because the MCP server or channel is unavailable, say the local Douyin channel is unavailable and suggest checking `agent-reach doctor` or `mcporter_list_servers()`.
- Avoid login/cookie instructions unless the tool output explicitly indicates authentication is required.

## Example Requests

- "帮我看一下这个抖音视频讲了什么 https://v.douyin.com/xxx/"
- "提取这个抖音里的文案和重点"
- "这个抖音视频有没有无水印下载链接？"
- "批量总结这几个抖音链接"
