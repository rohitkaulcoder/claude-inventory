# Claude Code Inventory & System Documentation

> **Last Updated:** 2026-04-09
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
- Script: `fetch_podcasts.py`
- LaunchAgent: `com.rohitkaul.podcast-step1-fetch.plist`
- Schedule: Daily
- Status: ⚠️ Not working (API/VPN issues)

**Generate Stage:**
- Script: `auto_generate_digest.sh`
- LaunchAgent: `com.rohitkaul.podcast-step2-generate.plist`
- Status: ✅ Working

**Publish Stage:**
- Script: `auto_publish_to_github.sh`
- LaunchAgent: `com.rohitkaul.podcast-step3-publish.plist`
- Status: ✅ Working

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

1. **reader-daily-digest** ⭐ NEW - Generate daily digest of inbox with deep insights and quotes (Discord-accessible)
2. **book-review** - Draft long-form book reviews from Reader highlights
3. **build-persona** - Build personalized reading profile from Reader data
4. **feed-catchup** - Catch up on RSS feed with highlights
5. **highlight-graph** - Visualize highlights in interactive 2D graph
6. **now-reading-page** - Generate personal "Now Reading" webpage
7. **quiz** - Quiz yourself on recently read documents
8. **reader-recap** - Conversational briefing on recent reading
9. **readwise-cli** - How to use Readwise CLI
10. **surprise-me** - Analyze reading history for surprising insights
11. **triage** - Triage Reader inbox with personalized pitches
12. **notebooklm-import** - Batch-import NotebookLM exports (audio + PDFs) from a folder → transcribe audio (Groq Whisper), save all docs to Reader, generate highlights → push to Readwise. Also generates an **Alpha Brief** — a layered-depth synthesis document (3 zoom levels) pushed to Reader. Folder name format: `Title - Author`. Tracks processed files via `processed.json`. Caches transcripts as `.txt` sidecar files.

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
- **Purpose:** Daily email digest of US tech industry news from 3 podcasts (TBPN, TITV, Techmeme Ride Home)
- **Stack:** Python, Anthropic API (Sonnet), Resend, GitHub Actions
- **Schedule:** Weekdays at 7:00 AM IST (1:30 UTC) via cron-job.org → `workflow_dispatch` (GitHub Actions `schedule` trigger removed 2026-04-02)
- **Email:** Sent via Resend to recipient (from `onboarding@resend.dev`)
- **Secrets:** `ANTHROPIC_API_KEY`, `RESEND_API_KEY`, `GROQ_API_KEY`, `YOUTUBE_API_KEY`, `RECIPIENT_EMAIL`
- **Cost:** ~$6/month (Anthropic API + Groq Whisper)
- **Setup Date:** 2026-03-30
- **Forked from:** daily-podcast-roundup

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

## LaunchAgents & Automations

**Location:** `~/Library/LaunchAgents/`

### Readwise
- `com.readwise.search.plist` - Readwise Search app launcher

### Podcast Automation
- `com.rohitkaul.podcast-step1-fetch.plist` - Stage 1: Fetch podcasts
- `com.rohitkaul.podcast-step2-generate.plist` - Stage 2: Generate digest
- `com.rohitkaul.podcast-step3-publish.plist` - Stage 3: Publish to GitHub
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
- Podcast digest generation (stages 2 & 3)
- Health check monitoring
- All Claude Skills

### Partially Working ⚠️
- Podcast fetching (Stage 1) - API/VPN issues
- Overall podcast automation pipeline

### Not Working ❌
- None currently identified

### Known Issues
1. **Podcast Fetch**: API access issues, possibly VPN-related
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
4. Fix podcast fetching API issues
5. Create central backup strategy
6. Add comprehensive error handling to all automations

---

**Note:** This inventory should be updated whenever new tools, apps, or automations are created or modified.
