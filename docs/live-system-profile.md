# Live System Profile: Jarvis on Hermes

This document captures the **audited live state** of the Hermes/Jarvis deployment that powers the broader workflow described in the repo root README.

Audit date: **2026-05-02**

## 1. Runtime identity

### Hermes version

```text
Hermes Agent v0.12.0 (2026.4.30)
Project: /opt/hermes
Python: 3.11.15
OpenAI SDK: 2.32.0
Up to date
```

### Active launcher

- `/hermes.sh`

Observed launcher behaviors:

- changes into `/opt/data` first, or `/root` as fallback
- uses `/opt/hermes/venv/bin/hermes`
- checks `/opt/data/.env` for `TELEGRAM_BOT_TOKEN`
- starts the gateway with `hermes gateway run --replace`
- attempts stale lock cleanup under `~/.local/state/hermes/gateway-locks`

### Active gateway process observed

```text
/opt/hermes/venv/bin/python3 /root/.local/bin/hermes gateway run
```

## 2. Config profile

Config file:

- `/opt/data/config.yaml`

### Core settings observed

- Primary provider: `openai-codex`
- Default model: `gpt-5.4`
- Fallback models:
  - `openrouter / deepseek/deepseek-v4-pro`
  - `openrouter / anthropic/claude-sonnet-latest`
- Terminal backend: `local`
- Terminal persistence: enabled
- Browser local/private URL fallback: enabled
- Checkpoints: enabled
- Compression: enabled
- Session retention: 90 days
- Smart model routing: disabled
- Session reset: both idle + scheduled daily reset
- Home Telegram channel configured in config

### Safety and operational settings observed

- Approvals: `manual`
- Cron approvals: `deny`
- Secret redaction: enabled
- Tirith enabled: `true`
- Tool loop warnings: enabled
- Curator: enabled

## 3. Data layout

Live root:

- `/opt/data`

Key directories discovered:

- `/opt/data/audio_cache`
- `/opt/data/backups`
- `/opt/data/bin`
- `/opt/data/cache`
- `/opt/data/checkpoints`
- `/opt/data/cron`
- `/opt/data/google-oauth-venv`
- `/opt/data/hooks`
- `/opt/data/image_cache`
- `/opt/data/images`
- `/opt/data/import`
- `/opt/data/logs`
- `/opt/data/memories`
- `/opt/data/migration_bootstrap`
- `/opt/data/pairing`
- `/opt/data/pastes`
- `/opt/data/platforms`
- `/opt/data/profiles`
- `/opt/data/sandboxes`
- `/opt/data/scripts`
- `/opt/data/sessions`
- `/opt/data/skills`
- `/opt/data/state-snapshots`
- `/opt/data/workspace`

This is one of the strongest signals that the system has moved beyond experimentation. There is a real operational directory model with storage for memory, sessions, scripts, backups, checkpoints, profiles, and outputs.

## 4. Obsidian vault

Location:

- `/opt/data/workspace/obsidian-vault`

Observed state:

- exists: yes
- git repo: yes
- markdown file count: **590**
- current branch: `main`
- remote: `https://github.com/realgradientdescent/hermes-vault.git`

### Recent vault activity sample

Observed recent git log entries:

- `532d530 chore: daily vault sync 2026-05-01`
- `362602f mark browser workflow QA agent built`
- `907a432 update AI Idea Radar backlog and reports`

This is useful portfolio evidence because it shows the vault is actively used, actively synced, and tied to real work output.

## 5. Memories

Memory directory:

- `/opt/data/memories`

Observed files:

- `MEMORY.md`
- `USER.md`
- plus lock files for each

### Capacity snapshot

- `MEMORY.md`: **2191 chars**
- `USER.md`: **1383 chars**

Configured limits in `config.yaml`:

- environment/system memory cap: **2200**
- user profile cap: **1375**

### Interpretation

The deployment is using memory as a compact high-value state layer, not as a dumping ground.

The stored information includes things like:

- mount/path realities
- vault repo details
- automation job IDs
- OAuth setup quirks
- user operating preferences

That is exactly the kind of information a serious agent should persist.

## 6. Skills system

Skills root:

- `/opt/data/skills`

Observed counts:

- top-level category directories: **28**
- `SKILL.md` files: **125**

This means Jarvis is backed by a substantial procedural library.

The skills layer matters because it turns repeated success into reusable operating instructions. In practice, it is how the system scales from a general assistant into a domain-adapted operator.

## 7. Sessions and continuity

Sessions directory:

- `/opt/data/sessions`

Observed top-level item count:

- **180**

This is the broader recall layer behind memory. Sessions preserve prior work, while the memory layer stores only the most durable facts.

That division is good architecture:

- memory for stable truths
- session search for historical context

## 8. Automation scripts

Scripts directory:

- `/opt/data/scripts`

Observed Python scripts include:

- `vault_git_sync.py`
- `gmail_send_attachment.py`
- `create_qa_google_doc.py`
- `google_docs_minimal_oauth.py`
- `google_docs_write_oauth.py`
- `mobile_portfolio_qa.py`
- `qa_report_helper.py`
- `update_weekly_calendar_md_link.py`
- `fix_weekly_calendar_readable_pdf.py`
- `create_weekly_backlog_calendar.py`
- `generate_ai_radar_attachments.py`
- `x_idea_radar_fetch.py`
- `x_idea_radar_daily.py`
- `x_idea_radar_weekly.py`

This is important because it shows that Jarvis is not only model-driven. It is also script-augmented where reliability or integration depth matters.

## 9. Cron jobs

Cron data:

- `/opt/data/cron/jobs.json`

Observed recurring jobs include:

### AI Agent Idea Radar — Daily Morning Brief

- job id: `95e662b5c0d8`
- schedule: `0 13 * * *`
- source script: `x_idea_radar_daily.py`
- output behavior: generates a markdown brief + PDF, then emails/attaches it

### AI Agent Idea Radar — Weekly Ideas and Backlog

- job id: `a9ae6cd6bf83`
- schedule: `30 13 * * 0`
- source script: `x_idea_radar_weekly.py`
- output behavior: generates a weekly markdown report, updates backlog, updates a calendar event

### Daily Hermes vault git sync

- job id: `be365b4e838e`
- schedule: `30 4 * * *`
- source script: `vault_git_sync.py`
- output behavior: checks, commits, and pushes vault changes when needed

### Why this matters

These jobs prove that the system creates value while the user is not actively chatting with it. That is a major step up from an on-demand assistant.

## 10. GitHub sync implementation

The vault sync script deserves its own note because it shows strong operational judgment.

### What the script does

- loads token from `/opt/data/.env` if needed
- uses a GitHub HTTPS auth header rather than storing credentials in the remote URL
- disables interactive prompts for unattended runs
- preflights the remote before trying to push
- fetches remote state
- commits only when changes exist
- emits concise success/failure output for cron delivery

### Why this is good engineering

- safer than embedding credentials in the remote URL
- more robust in containers/headless shells
- friendly to automation
- easy to reason about when something fails

## 11. Google Workspace bridge

Observed dedicated environment:

- `/opt/data/google-oauth-venv`

This supports scripts that integrate with:

- Gmail
- Google Docs
- Calendar-linked workflows

This matters because it moves Jarvis beyond local tooling and into actual delivery channels.

## 12. gbrain / qmd reality check

Observed migration helper:

- `/opt/data/migration_bootstrap/bootstrap_gbrain_obsidian_qmd.sh`

The script expects:

- `GBRAIN_DIR="$HOME/gbrain"`
- a QMD-indexed Obsidian vault

But in the audited live container:

- `/root/gbrain` does not exist
- `gbrain` command not found
- `qmd` command not found

### Accurate conclusion

The architecture clearly anticipated gbrain/QMD integration, and migration tooling exists for it.

But this specific live container snapshot is not currently running that component.

That is the correct technical statement.

## 13. What this system says about the builder

This setup signals more than familiarity with AI tools.
It signals:

- systems thinking
- operational discipline
- appetite for automation
- concern for durable knowledge capture
- ability to bridge product needs with technical infrastructure
- willingness to handle ugly real-world details like auth, sync, lock files, path drift, and unattended execution

That is exactly why the project is worth documenting publicly.
