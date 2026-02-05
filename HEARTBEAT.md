# HEARTBEAT.md

ops heartbeat rules (혼합형/압축). If nothing actionable → reply `HEARTBEAT_OK`.

- quiet hours: none

1) spectra cron health (`82a4be25-909a-4b4c-8812-c14b2c886073`)
- check MOST RECENT run only
- alert if: `lastStatus!=ok` OR `now-lastRunAt>3h` (for 2h job)
- include: `nextRunAt`
- ignore older failures if latest ok

2) daily note + memory maintenance cron (00:00 KST)
- job: `7b999e6b-9b7d-4bc4-848d-72af0204dc6c`
- missing/disabled → alert

3) disk free
- check C:, D:
- critically low → alert

4) security
- if `openclaw status` shows CRITICAL → alert with fix summary

5) trash retention (30d)
- run: `C:\Users\user\miniconda3\python.exe C:\Users\user\bot\skills_scripts\trash_cleanup.py --days 30`
- alert only on failure
