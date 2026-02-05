# MEMORY_public.md

This file is auto-generated from MEMORY.md with secrets redacted.
Do NOT add secrets here. Edit MEMORY.md instead.

GeneratedAt: 2026-02-05T21:05:12

﻿# MEMORY.md - Long-Term Memory

## (Operational notes moved)
- Operational/playbook-style notes were moved to `AGENTS.md` under **"Operational Playbook"**.
- `MEMORY.md` should focus on durable facts/decisions/IDs/state.

## 🔄 Spectra Sync Automation (현재 운영)

### Cron (단일 파이프라인)
- **cron job:** `spectra-sync-all (wrapper)`
- **주기:** 2시간마다 (even-hour align)
- **cron id:** `82a4be25-909a-4b4c-8812-c14b2c886073`
- **동작:** Cron → `spectra-sync-all` skill → wrapper script 실행(2-step)
  1) `spectra_snapshot_sync.py` (dataset → `D:\dataset\data_CR_repo`)
  2) `spectra_git_push_update.py` (dataset → `C:\Users\user\PHS`)
- **정책:** PHS repo에서는 **오직 `spectra_latest_1.npy`만** 업데이트/푸시

### Python Runtime
- `C:\Users\user\miniconda3\python.exe`

### 폴더/스킬 최신 트리 (2026-02-05)

**bot 폴더**
```text
C:\Users\user\bot
+---archive
|   \---large
+---core-md
+---docs
+---keys
+---repos
|   \---moltbot
+---skills
|   +---context-reset
|   |   \---scripts
|   +---context-summarize-memory
|   |   \---scripts
|   +---core-md-git-push
|   +---discord-admin
|   +---discord-browser
|   +---git-pull-rebase
|   +---github-create-repo
|   +---github-create-repo-hyoseokp
|   +---spectra-count-n
|   \---spectra-sync-all
+---skills_scripts
\---work
    +---bat
    +---notebooks
    +---ps1
    +---py
    \---text

```

**skills 폴더**
```text
C:\Users\user\bot\skills
+---context-reset
|   |   SKILL.md
|   |
|   \---scripts
|           reset_session.py
|
+---context-summarize-memory
|   |   SKILL.md
|   |
|   \---scripts
|           debug_structure.py
|           summarize_context.py
|
+---core-md-git-push
|       SKILL.md
|
+---discord-admin
|       SKILL.md
|
+---discord-browser
|       SKILL.md
|
+---git-pull-rebase
|       SKILL.md
|
+---github-create-repo
|       SKILL.md
|
+---github-create-repo-hyoseokp
|       SKILL.md
|
+---spectra-count-n
|       SKILL.md
|
\---spectra-sync-all
        SKILL.md

```

### 스킬/구조 변경 메모
- `git-push-data-cr` (DEPRECATED) 스킬 제거됨.
- `spectra-snapshot-sync`, `spectra-git-push` 스킬 폴더는 wrapper 중복이라 제거됨.
  - 단, 실제 실행 스크립트(`bot\skills_scripts\spectra_snapshot_sync.py`, `spectra_git_push_update.py`)는 wrapper가 사용하므로 유지.
