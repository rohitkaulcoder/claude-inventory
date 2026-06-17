# Claude Code Inventory & System Documentation

> **Last Updated:** 2026-06-17
> **Purpose:** Central registry of all apps, tools, automations, and documentation built with Claude Code

---

## Table of Contents
1. [Applications](#applications)
2. [Automation Systems](#automation-systems)
3. [Claude Skills](#claude-skills)
4. [Development Projects](#development-projects)
5. [Documentation](#documentation)
6. [Configuration Files](#configuration-files)
7. [LaunchAgents & Automations](#launchagents--automations)
8. [Status & Health](#status--health)

---

## Applications

### 1. Readwise Search App
- **Status:** ✅ Working
- **Type:** macOS Native Application
- **Location:** `/Users/rohitkaul/Applications/Readwise Search.app`
- **Source Code:** `/Users/rohitkaul/Documents/readwise_search/`
- **Purpose:** Search and manage Readwise highlights with system-wide hotkey access
- **Key Files:**
  - `readwise_app.py` - Main application (50KB)
  - `sync_highlights.py` - Syncs highlights from Readwise API
  - `search_engine.py` - Search functionality
  - `highlights_db.json` - Highlights database (31MB)
- **Documentation:**
  - `~/Documents/readwise_search/README.md`
  - `~/Documents/readwise_search/USAGE.md`
- **LaunchAgent:** `~/Library/LaunchAgents/com.readwise.search.plist`
- **Dependencies:** Python 3, Readwise API key
- **Last Modified:** 2024-02-16

---

## Automation Systems

### 1. Daily Podcast Roundup
- **Status:** ✅ Working
- **Type:** Multi-stage automation pipeline
- **Base Directory:** `/Users/rohitkaul/Projects/daily-podcast-roundup/`
- **Scripts Location:** `/Users/rohitkaul/`
- **Purpose:** Automatically fetch podcast transcripts, generate digests, and publish to GitHub

#### Components:

**Fetch Stage:**
- Script: `scripts/fetch_podcasts.py`
- LaunchAgent: `com.rohitkaul.podcast-step1-fetch.plist`
- Schedule: Daily at 5:00 PM
- Status: ✅ Working (Groq Whisper transcription)

**Readwise Push Stage (primary output):**
- Script: `scripts/push_to_readwise.py`
- Wrapper: `~/auto_push_readwise.sh`
- LaunchAgent: `com.rohitkaul.podcast-step2b-readwise.plist`
- Schedule: Daily at 5:15 PM (after fetch)
- Status: ✅ Working

**Generate Stage (legacy):**
- Script: `auto_generate_digest.sh`
- LaunchAgent: `com.rohitkaul.podcast-step2-generate.plist`
- Status: ✅ Working (legacy, not primary output)

**Publish Stage (legacy):**
- Script: `auto_publish_to_github.sh`
- LaunchAgent: `com.rohitkaul.podcast-step3-publish.plist`
- Status: ✅ Working (legacy, not primary output)

**Health Monitoring:**
- Script: `podcast_health_check.sh`
- LaunchAgent: `com.rohitkaul.podcast-health-check.plist`
- Notifications: `send_notification.sh`

#### Supporting Scripts:
- `auto_fetch_and_generate_all.sh` - Combined fetch + generate
- `auto_generate_and_publish.sh` - Combined generate + publish
- `setup_3step_automation.sh` - Setup script for 3-stage automation
- `vpn_connect.sh` - VPN connection helper

#### Configuration:
- `podcasts.json` - Podcast sources and metadata
- `test_podcasts.json` - Test configuration

#### Documentation:
- `AUTOMATION_GUIDE.md`
- `PODCAST_DIGEST_COMPLETE_GUIDE.md`
- `PODCAST_SETUP_COMPLETE.md`
- `PODCAST_MAGAZINE_README.md`
- `TROUBLESHOOTING_GUIDE.md`
- `MONITORING_GUIDE.md`
- `VPNSOLUTION.md`
- `.claude_podcast_magazine_instructions.md`

#### Log Files:
- `podcast_automation.log`
- `podcast_fetch.log`
- `podcast_health_check.log`
- `podcast_step1_fetch.log`
- `podcast_step2_generate.log`
- `podcast_step3_publish.log`

---

## Claude Skills

**Location:** `~/.claude/skills/`

All skills are Readwise-focused and gitignored by default:

1. **reader-daily-digest** - Generate daily digest of inbox with deep insights and quotes (Discord-accessible)
2. **book-review** - Draft long-form book reviews from Reader highlights
3. **build-persona** - Build personalized reading profile from Reader data
4. **feed-catchup** - Catch up on RSS feed with highlights
5. **follow-builders** - AI builders digest — monitors top AI builders on X and YouTube podcasts, remixes into digestible summaries
6. **highlight-graph** - Visualize highlights in interactive 2D graph
7. **now-reading-page** - Generate personal "Now Reading" webpage
8. **quiz** - Quiz yourself on recently read documents
9. **reader-recap** - Conversational briefing on recent reading
10. **readwise-cli** - How to use Readwise CLI
11. **surprise-me** - Analyze reading history for surprising insights
12. **triage** - Triage Reader inbox with personalized pitches
13. **notebooklm-import** - Batch-import NotebookLM exports (audio + PDFs) from a folder → transcribe audio (Groq Whisper), save all docs to Reader, generate highlights → push to Readwise. Also generates an **Alpha Brief** — a layered-depth synthesis document (3 zoom levels) pushed to Reader. Folder name format: `Title - Author`. Tracks processed files via `processed.json`. Caches transcripts as `.txt` sidecar files.
14. **alpha-interview** - Editorial compression of interview/podcast transcripts. Fetches a document from Reader, cuts banter/filler/housekeeping, tightens circular answers while preserving first-person voice and original questions, saves back as "Alpha - [Title]" with tag "Alpha".
15. **gemini** - Route a question to Google's Gemini via `gemini -p` for a second opinion, fact-check, or independent code review. Uses Gemini CLI (`@google/gemini-cli`, installed at `~/.npm-global/bin/gemini`). Headless only — image generation explicitly out of scope (CLI produces empty PNGs; use Gemini API directly with `gemini-2.5-flash-image` for Nano Banana). Always call serially; parallel calls hang.

---

## Development Projects

### 1. Readwise MCP Server
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/readwise-reader-mcp/`
- **Type:** Model Context Protocol Server
- **Purpose:** Enables Claude Code to interact with Readwise Reader API
- **Language:** Node.js/TypeScript

### 2. Byline
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/byline/`
- **Type:** Web Application
- **Stack:** Astro + Sanity CMS
- **Purpose:** Personal blog/content site
- **Deployment:** Vercel
- **Documentation:** `~/Projects/byline/README.md`

### 3. Daily Podcast Roundup
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/daily-podcast-roundup/`
- **Type:** GitHub-hosted digest + Readwise highlights pipeline
- **Documentation:**
  - `~/Projects/daily-podcast-roundup/README.md`
  - `~/Projects/daily-podcast-roundup/SETUP.md`

### 4. Inventory Sync System
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/claude-inventory/`
- **GitHub:** https://github.com/rohitkaulcoder/claude-inventory
- **Type:** System documentation & auto-sync
- **Purpose:** Central registry of all Claude-built systems with automatic GitHub sync
- **Components:**
  - Local inventory: `/Users/rohitkaul/CLAUDE_INVENTORY.md`
  - Sync script: `/Users/rohitkaul/sync_inventory.sh`
  - LaunchAgent: `com.rohitkaul.inventory-sync`
  - Schedule: Daily at 9:00 AM (catches up at startup if laptop was off)
- **Documentation:** `~/INVENTORY_SYNC_GUIDE.md`

### 5. Reader Digests Site
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/reader-digests/`
- **GitHub:** https://github.com/rohitkaulcoder/reader-digests
- **Live URL:** https://rohitkaulcoder.github.io/reader-digests/
- **Type:** Jekyll static site on GitHub Pages + automated email digest
- **Purpose:** Daily reading digest from Readwise Reader — published to site and emailed
- **Stack:** Jekyll, GitHub Pages, GitHub Actions, Claude (`claude -p` Sonnet + Haiku), `@readwise/cli`, Resend API
- **Schedule:** Daily at 7:00 AM IST (1:30 UTC) via cron-job.org → `workflow_dispatch`
- **Pipeline:** 3-stage: Haiku triage (top 10) → Sonnet per-article analysis (isolated calls) → Haiku assembly
- **Source:** Readwise Reader **feed only** (no library/later)
- **Email:** Sent via Resend to `rohit@rohitkaul.com` (from `onboarding@resend.dev`)
- **Cost:** ~$1.03/run (~$30/month) — optimized 2026-04-02 from $8.35/run
- **Secrets:** `ANTHROPIC_API_KEY`, `READWISE_TOKEN`, `RESEND_API_KEY`
- **Setup Date:** 2026-03-29 (pipeline optimized 2026-04-02)

### 8. Reya's Timetable Email
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/reya-timetable/`
- **GitHub:** https://github.com/rohitkaulcoder/reya-timetable
- **Type:** Automated daily email
- **Purpose:** Sends Reya's school timetable (8 SARISKA, Shiv Nadar School, Noida) daily at 8 PM IST
- **Stack:** Python, Resend, GitHub Actions
- **Schedule:** Daily at 8:00 PM IST (14:30 UTC) except Saturday, via cron-job.org → `workflow_dispatch`
- **Logic:** Mon-Thu: today + tomorrow; Friday: Friday only; Sunday: Monday only
- **Email:** Sent via Resend to rohit@rohitkaul.com (from `onboarding@resend.dev`)
- **Secrets:** `RESEND_API_KEY`, `RECIPIENT_EMAIL`
- **Cost:** Free (Resend free tier)
- **Setup Date:** 2026-04-03

### 9. Rihaan's Timetable Email
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/rihaan-timetable/`
- **GitHub:** https://github.com/rohitkaulcoder/rihaan-timetable
- **Type:** Automated daily email
- **Purpose:** Sends Rihaan's school timetable (Grade II Kanha EY, Shiv Nadar School, Noida) daily at 8 PM IST
- **Stack:** Python, Resend, GitHub Actions
- **Schedule:** Daily at 8:00 PM IST (14:30 UTC) except Saturday, via cron-job.org → `workflow_dispatch`
- **Logic:** Mon-Thu: today + tomorrow; Friday: Friday only; Sunday: Monday only
- **Email:** Sent via Resend to rohit@rohitkaul.com (from `onboarding@resend.dev`)
- **Secrets:** `RESEND_API_KEY`, `RECIPIENT_EMAIL`
- **Cost:** Free (Resend free tier)
- **Setup Date:** 2026-04-03

### 7. Daily Tech Roundup
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/daily-tech-roundup/`
- **GitHub:** https://github.com/rohitkaulcoder/daily-tech-roundup
- **Type:** Automated email digest
- **Purpose:** Daily email digest of US tech industry news from 3 sources (TBPN, TITV, MTS Live)
- **Stack:** Python, Anthropic API (Sonnet), Resend, GitHub Actions, yt-dlp + Groq Whisper
- **Schedule:** Weekdays at 7:00 AM IST (1:30 UTC) via cron-job.org → `workflow_dispatch` (GitHub Actions `schedule` trigger removed 2026-04-02)
- **Email:** Sent via Resend to recipient (from `onboarding@resend.dev`)
- **Secrets:** `ANTHROPIC_API_KEY`, `RESEND_API_KEY`, `GROQ_API_KEY`, `YOUTUBE_API_KEY`, `RECIPIENT_EMAIL`
- **Cost:** ~$6/month (Anthropic API + Groq Whisper)
- **Setup Date:** 2026-03-30
- **Forked from:** daily-podcast-roundup
- **Last source change:** 2026-05-10 — replaced Techmeme Ride Home with MTS Live ([@mtsituation](https://www.youtube.com/@mtsituation)). YouTube-only sources use yt-dlp to download audio → Groq Whisper, gated by `youtube_channel_id` in CHANNELS config and filtered to "Best Of" videos.

### 10. Podcast Highlights Feed
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/podcast-feed/`
- **Type:** Web Application
- **Stack:** Next.js 15 (App Router), Tailwind, Vercel
- **Live URL:** https://podcast-feed.vercel.app
- **Purpose:** Reels-style card feed of podcast highlights with star/dismiss, sourced from Readwise
- **Features:** Snap-scroll feed, source & topic filters, quality-scored card ordering, localStorage state
- **Data:** 6,500+ blurbs in `public/data/blurbs.json`, generated via `claude -p`
- **Pending:** Vercel KV for cross-device sync
- **Setup Date:** 2026-03

### 12. VC Feed Daily Digest
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/vc-feed/`
- **GitHub:** https://github.com/rohitkaulcoder/vc-feed
- **Type:** Automated email digest
- **Purpose:** Daily AI-curated digest of ~45 hand-picked VC/LP voices on X
- **Stack:** Python, Supabase Postgres (Mumbai), Apify (`xquik/x-tweet-scraper`), Anthropic (Haiku 4.5 enrichment + Sonnet 4.5 intro), Resend, GitHub Actions
- **Schedule:** Daily at 7:00 AM IST (1:30 UTC) via cron-job.org → `workflow_dispatch`
- **Email:** Sent via Resend to `rohit@rohitkaul.com` (from `onboarding@resend.dev`)
- **Trigger PAT:** `cron-job-trigger` fine-grained PAT (now scoped to all repos as of 2026-05-19)
- **Secrets in GitHub:** `SUPABASE_URL`, `SUPABASE_SERVICE_KEY`, `ANTHROPIC_API_KEY`, `RESEND_API_KEY`, `APIFY_TOKEN`, `VCFEED_RECIPIENT`
- **Data sources:**
  - 47 curated X handles at `Documents/Cowork/VC News/x-feed-list.csv` (45 active; HunterWalk + vaibhavbetter marked inactive)
  - ~12,000 backfilled tweets in Supabase `posts` table (250/handle day-0)
- **Pipeline (in `scripts/`):**
  1. `backfill.py` — incremental tweet ingestion via Apify HTTP API (since-date filter from `MAX(posted_at)` per handle, 6h overlap buffer)
  2. `enrich.py` — Claude Haiku classifies each post (work/personal/banter/news_pointer), tags theme, generates 1-sentence core_claim, scores importance 1-5
  3. `digest.py` — pulls last 24h of work-classified posts, applies firehose filter (TurnerNovak + HarryStebbings only at importance ≥ 3), drops Misc/Portfolio themes, asks Sonnet for "Top 5" with why-this-matters, renders 3-section HTML
- **3-section format:** ⭐ The 5 (full read, Sonnet picks) → 📌 Worth a click (importance ≥3 one-liners) → 📋 Everything else (compact index)
- **Cost:** ~$10-15/month (Apify ~$1/mo, Anthropic ~$3-5/mo, Resend + Supabase free tiers)
- **Day-0 backfill spend (one-time, 2026-05-19):** Apify $1.55 + Anthropic ~$2.50 enrichment = ~$4
- **Manual trigger:** `~/Projects/vc-feed/scripts/run_daily.sh` (requires env vars in shell)
- **Setup Date:** 2026-05-11 (storage + ingest) → 2026-05-19 (enrichment + digest + GH Actions + cron-job.org)
- **Key learning:** xquik actor at $0.15/1k tweets is the right choice; `apidojo/twitter-user-scraper` and `xtdata/twitter-x-user-info-scraper` both have hidden costs/plan-gates
- **Caveats:**
  - Anthropic API 529 overload events occasionally cause batch failures during enrichment — failed posts remain `enriched_at IS NULL` and get picked up on next run automatically
  - PostgREST aggregates disabled by default in Supabase (worked around with per-handle top-1 queries)
  - URL-encode timestamp params for PostgREST: `+00:00` → `Z` suffix

### 11. Granola Export
- **Status:** ✅ Working
- **Location:** `/Users/rohitkaul/Projects/granola-export/`
- **Type:** Utility script
- **Purpose:** Export all Granola meeting transcripts to Markdown files
- **Script:** `export_granola.py` — reads auth tokens from local Granola app, fetches all documents via API
- **Output:** `transcripts/` directory (~715 files)
- **Setup Date:** 2026-04

### 6. Discord Bot Integration
- **Status:** ✅ Working
- **Type:** Claude Code Channel Plugin
- **Purpose:** Trigger Claude Code skills from Discord (phone or desktop)
- **Bot Name:** claude_app
- **Setup Date:** 2026-03-20
- **Requirements:**
  - Claude Code v2.1.80+ ✅
  - Bun runtime v1.3.11 ✅
  - Discord bot token (configured)
- **Features:**
  - Trigger skills via DM (e.g., "digest" → runs reader-daily-digest)
  - Receive formatted responses in Discord
  - Works from any device (phone, tablet, desktop)
  - Paired and access-controlled (allowlist policy)
- **Usage:**
  - Start Claude Code with: `claude --channels plugin:discord@claude-plugins-official`
  - Send DM to bot: "digest", "reader digest", etc.
- **Primary Use Case:** Daily Reader inbox digest accessible from phone

---

## Documentation

### Primary Guides (Home Directory)
- `INVENTORY_SYNC_GUIDE.md` - Inventory system setup and usage
- `AUTOMATION_GUIDE.md` - Overall automation system guide
- `CRON_JOBS_STATUS.md` - Status of scheduled jobs
- `MONITORING_GUIDE.md` - How to monitor automations
- `TROUBLESHOOTING_GUIDE.md` - Common issues and solutions
- `PODCAST_DIGEST_COMPLETE_GUIDE.md` - Complete podcast workflow
- `PODCAST_MAGAZINE_README.md` - Magazine generation
- `PODCAST_SETUP_COMPLETE.md` - Initial setup instructions
- `VPNSOLUTION.md` - VPN configuration for podcast fetching
- `fetch_via_browser.md` - Browser-based fetching workaround

### Analysis & Research
- `webinar_registrant_analysis.md` - Webinar data analysis
- `webinar_registrant_analysis_filtered.md` - Filtered analysis
- `wes_kao_newsletters.md` - Wes Kao newsletter compilation
- `wes_kao_newsletters_complete.md` - Complete compilation
- `wes_kao_full_text.md` - Full text version

### Hidden Configuration
- `.claude/CLAUDE.md` - Global Claude Code instructions
- `.claude_podcast_magazine_instructions.md` - Podcast magazine generation instructions

---

## Configuration Files

### Readwise
- `.readwise-cli.json` - Readwise CLI configuration (92KB)
- `.readwise/` - Readwise data directory

### Application Configs
- `~/Documents/readwise_search/config.json` - Readwise Search app config
- `~/Projects/daily-podcast-roundup/data/` - Podcast data storage

### Shell Scripts
All automation shell scripts are in home directory (`~/`):
- `auto_*.sh` - Automation scripts
- `setup_*.sh` - Setup scripts
- `podcast_*.sh` - Podcast-specific scripts
- `send_notification.sh` - macOS notification helper
- `vpn_connect.sh` - VPN automation

---

## CLI Tools

Installed globally and available on PATH:

- **readwise** (`~/.npm-global/bin/readwise`, v0.5.4) — Readwise CLI for accessing highlights, documents, and Reader library. Skill: `readwise-cli`.
- **gemini** (`~/.npm-global/bin/gemini`, v0.41.2) — Google Gemini CLI. Auth: OAuth as `rohit@rohitkaul.com` + Gemini API key set in `~/.zshrc` as `NANOBANANA_API_KEY` / `GEMINI_API_KEY`. Skill: `gemini` (text only — image gen blocked by zero free-tier quota; needs API billing enabled to use Nano Banana). Nano Banana extension installed at `~/.gemini/extensions/nanobanana/`.
- **apify** (`/opt/homebrew/bin/apify`, v1.6.1, installed via Homebrew) — Apify CLI for running scrapers/actors and managing Apify projects. Logged in as `express_heron`. Note: `npm install -g apify-cli` fails due to pnpm postinstall dependency — use Homebrew.
- **yt-dlp** (`/opt/homebrew/bin/yt-dlp`, v2026.03.03, installed via Homebrew) — Download videos/audio from YouTube and 1000+ other sites. Useful for grabbing podcast episodes, extracting audio for transcription pipelines, archiving clips.
- **ffmpeg** (`/opt/homebrew/bin/ffmpeg`, v8.1, installed via Homebrew) — Audio/video conversion, trimming, transcoding. Pairs naturally with yt-dlp for audio extraction and with Whisper/Groq for transcription pipelines.
- **supabase** (`/opt/homebrew/bin/supabase`, v2.98.2, installed via Homebrew) — Supabase CLI for project management, schema migrations, db push/pull. Auth token in `~/.zshrc` as `SUPABASE_ACCESS_TOKEN`. Linked to `vc-feed` and `FoodToob` projects.
- **claude** — Claude Code itself.
- **gh** — GitHub CLI for repo/PR/issue management.

---

## LaunchAgents & Automations

**Location:** `~/Library/LaunchAgents/`

### Readwise
- `com.readwise.search.plist` - Readwise Search app launcher

### Podcast Automation
- `com.rohitkaul.podcast-step1-fetch.plist` - Stage 1: Fetch podcasts (5:00 PM)
- `com.rohitkaul.podcast-step2b-readwise.plist` - Stage 2b: Push highlights to Readwise (5:15 PM) ← primary output
- `com.rohitkaul.podcast-step2-generate.plist` - Stage 2: Generate HTML digest (legacy)
- `com.rohitkaul.podcast-step3-publish.plist` - Stage 3: Publish to GitHub (legacy)
- `com.rohitkaul.podcast-health-check.plist` - Health monitoring
- `com.rohitkaul.podcast-full-automation.plist` - Full pipeline (legacy)
- `com.rohitkaul.podcastfetch.plist` - Simple fetch (legacy)

### System Maintenance
- `com.rohitkaul.inventory-sync.plist` - Auto-sync inventory to GitHub (daily)

### Management Commands
```bash
# List running LaunchAgents
launchctl list | grep rohitkaul

# Load/unload specific agent
launchctl load ~/Library/LaunchAgents/com.rohitkaul.podcast-step1-fetch.plist
launchctl unload ~/Library/LaunchAgents/com.rohitkaul.podcast-step1-fetch.plist

# Start immediately
launchctl start com.rohitkaul.podcast-step1-fetch
```

---

## Status & Health

### Working ✅
- Readwise Search App
- Readwise MCP Server
- Byline website
- Reader Digests Site (GitHub Pages)
- Podcast roundup — full pipeline (fetch + Readwise push)
- Podcast Highlights Feed (Vercel)
- Health check monitoring
- All 14 Claude Skills
- Reya & Rihaan timetable emails
- Daily Tech Roundup
- Granola Export
- Discord Bot Integration

### Not Working ❌
- None currently identified

### Known Issues
1. **LaunchAgent reboot persistence**: Podcast LaunchAgents have `RunAtLoad: false` and get unloaded after macOS reboots. Must manually `launchctl load` them. Has happened at least twice (2026-04-02, 2026-04-19). Consider setting `RunAtLoad: true`.
2. **Incremental Indexing**: Readwise app should use incremental indexing (don't rebuild from scratch)

---

## Quick Reference

### Common Tasks

**Check podcast automation status:**
```bash
~/podcast_health_check.sh
```

**Manual podcast fetch:**
```bash
python3 ~/fetch_podcasts.py
```

**View automation logs:**
```bash
tail -f ~/podcast_automation.log
```

**Launch Readwise Search:**
```bash
open ~/Applications/Readwise\ Search.app
```

**Check LaunchAgent status:**
```bash
launchctl list | grep rohitkaul
```

---

## Maintenance Notes

### Regular Checks
- [ ] Podcast automation logs (weekly)
- [ ] Readwise highlights sync (monthly)
- [ ] LaunchAgent status (monthly)
- [ ] Documentation updates (as needed)

### Backup Locations
- Podcast data: `~/Projects/daily-podcast-roundup/` (Git-backed)
- Readwise highlights: `~/Documents/readwise_search/highlights_db.json`
- Scripts: All in `~/` (should be backed up)

---

## Future Improvements

1. Consolidate scattered podcast scripts into Projects directory
2. Set up proper version control for automation scripts
3. Implement incremental indexing for Readwise app
4. Set `RunAtLoad: true` on podcast LaunchAgents to survive reboots
5. Create central backup strategy
6. Podcast Feed: add Vercel KV for cross-device sync

---

**Note:** This inventory should be updated whenever new tools, apps, or automations are created or modified.
