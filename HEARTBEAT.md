# HEARTBEAT.md

## Heartbeat checklist (ops)

Run these checks on each heartbeat; keep responses minimal. If nothing needs attention, reply `HEARTBEAT_OK`.

- Quiet hours: **none** (24/7 operation).

1) **Spectra cron health**
   - Check cron job `spectra-sync-all (wrapper)` (id `82a4be25-909a-4b4c-8812-c14b2c886073`): last run status + next run time.
   - If last run FAILED or no runs recently → alert in Discord channel 1468499965461663917.

2) **Daily memory note cron**
   - Ensure daily note cron exists: `daily-memory-note (22:00 KST)` (id `e7c40716-6b78-4e87-9872-5287025300f2`).
   - If missing/disabled → alert.

3) **Disk space sanity (lightweight)**
   - Quick check free space for `D:` and `C:` (spectra file is large). Alert if critically low.

4) **Security reminders (only if status shows critical)**
   - If `openclaw status` security audit shows CRITICAL again, alert with the recommended fix summary.

# Notes
# - Keep this file small to reduce token burn.
# - Avoid long summaries; only alert on actionable issues.

