# instagram-saved-analyzer

**English** · [한국어](README.ko.md)

A Claude skill that reads the Instagram posts you saved and never went back to, then files them into folders you define.

Built and used daily for three weeks before release.

> **Requires Claude Code.** The skill drives a browser through Playwright MCP, so a terminal is needed for setup. Mac and Windows both work in principle — only Mac is verified so far.

---

## What it does

- Opens your saved posts and reads **the text written inside carousel slides**, not just the caption
- Re-sorts everything into **topics you define yourself** (three, five, whatever you want — you name them)
- Saves the result as dated `.md` files in a folder per topic
- Flags posts that say "comment for the free resource" and asks whether you already received the link

Read only. It never likes, follows, comments, or sends DMs.

---

## Install

### 1. Get the skill (the easy way)

Download [`SKILL.md`](plugins/instagram-saved-analyzer/skills/instagram-saved-analyzer/SKILL.md), hand the file to Claude, and say:

```
put this skill in my skills folder
```

That is it. Claude places it at `~/.claude/skills/instagram-saved-analyzer/SKILL.md` for you.

<details>
<summary>Or install as a plugin (Claude Code terminal only)</summary>

```
/plugin marketplace add H-967/instagram-saved-analyzer
/plugin install instagram-saved-analyzer@h967-skills
```

</details>

### 2. Playwright MCP (needed to drive the browser)

Paste this into your terminal. Requires Node.js 18 or newer.

```
claude mcp add playwright npx @playwright/mcp@latest
```

Run `/mcp` inside Claude Code — if playwright shows up as connected, you are set.

### 3. Log into Instagram

Log in through Chrome yourself. The skill never asks for or stores your username or password.

---

## How to use it

### First run — set up your folders

In Claude Code, just say:

```
read my saved posts
```

The first time, it asks three things.

**1) Where to save the results**

```
~/Desktop/instagram-notes
```

💡 **Point it at a Google Drive or iCloud sync folder and the results show up on your phone.** No integration needed — the files sync on their own.

```
~/Google Drive/My Drive/instagram-notes
```

**2) How many topics, and what to call them**

```
Three. Design / Marketing / AI tools
```

Any number works. Two is fine. Six is fine.

**3) What belongs in each topic**

```
Design → layout, color, typography, references
Marketing → content planning, copy, account strategy
AI tools → tool intros, prompts, automation
```

These lines become the sorting rules. Vague descriptions produce vague sorting.

Your answers are stored at `~/.claude/instagram-saved-analyzer/설정.md`. **You are never asked again.**

### After that

```
read my saved posts
```

That is the whole command. You can also narrow it down.

```
only analyze the design collection
```

### Changing your topics

```
I want to change my topics
```

It edits the config file. Existing folders are left alone.

### How long it takes

About 5 to 10 minutes for 20 posts. Carousels are slow because it steps through every slide and reads the image. A browser window moving on its own is expected.

---

## Before you use it

This skill drives a browser to read the saved collection of your own account. Instagram Terms of Use restrict automated access without prior permission, so this approach may fall under that restriction.

- I used it once a day on my own account for three weeks with no account issues
- That said, the chance of a restriction is not zero, and **account risk is yours to accept**
- Do not run it repeatedly in a short window. Once a day is plenty
- If it errors mid-run, stop and do not retry immediately

The following are deliberately absent and will stay absent.

- Automating likes, follows, comments, or DMs
- Automated login or password storage
- Scraping other people's accounts or bulk-collecting public accounts
- Detection evasion

---

## Limitations

- Reels: caption and thumbnail only. Spoken content is not transcribed
- Instagram UI changes can stop a run midway
- Large saved collections take a while

---

## Roadmap

- Save directly to a Notion database
- Resume from where the last run stopped
- Windows verification
- A version that works without a terminal

Open an issue if you want something.

---

## License

MIT
