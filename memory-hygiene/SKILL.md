---
name: memory-hygiene
description: Audit, clean, and optimize Clawdbot's vector memory (LanceDB). Use when memory is bloated with junk, token usage is high from irrelevant auto-recalls, or setting up memory maintenance automation.
homepage: https://github.com/xdylanbaker/memory-hygiene
---

# Memory Hygiene

Keep vector memory lean. Prevent token waste from junk memories.

## Quick Commands

**Audit:** Check what's in memory
```
memory_recall query="*" limit=50
```

**Wipe:** Clear all vector memory
⚠️ **반드시 백업 후 실행** — 백업 없이 실행 금지
```bash
# 1단계: 백업
cp -r ~/.clawdbot/memory/lancedb/ ~/.clawdbot/memory/lancedb-backup-$(date +%Y%m%d)/

# 2단계: 삭제
rm -rf ~/.clawdbot/memory/lancedb/
```
Then restart gateway: `clawdbot gateway restart`

**Reseed:** After wipe, store key facts from MEMORY.md
```
memory_store text="<fact>" category="preference|fact|decision" importance=0.9
```

## Config: Disable Auto-Capture

The main source of junk is `autoCapture: true`. Disable it:

```json
{
  "plugins": {
    "entries": {
      "memory-lancedb": {
        "config": {
          "autoCapture": false,
          "autoRecall": true
        }
      }
    }
  }
}
```

Use `gateway action=config.patch` to apply.

## What to Store (Intentionally)

✅ Store:
- User preferences (tools, workflows, communication style)
- Key decisions (project choices, architecture)
- Lessons learned

❌ Never store:
- Heartbeat status ("HEARTBEAT_OK", "No new messages")
- Transient info (current time, temp states)
- Raw message logs (already in files)
- OAuth URLs or tokens
- Credentials, API keys, passwords, or their file locations

## Monthly Maintenance Cron

Set up a monthly wipe + reseed:
⚠️ **백업 단계가 반드시 포함되어야 함**

```
cron action=add job={
  "name": "memory-maintenance",
  "schedule": "0 4 1 * *",
  "text": "Monthly memory maintenance: 1) Backup ~/.clawdbot/memory/lancedb/ to lancedb-backup-YYYYMMDD/ 2) Wipe ~/.clawdbot/memory/lancedb/ 3) Parse MEMORY.md 4) Store key facts to fresh LanceDB 5) Report completion + backup path"
}
```

## Storage Guidelines

When using memory_store:
- Keep text concise (<100 words)
- Use appropriate category
- Set importance 0.7-1.0 for valuable info
- One concept per memory entry
