# MEMORY_public.md

This file is auto-generated from MEMORY.md with secrets redacted.
Do NOT add secrets here. Edit MEMORY.md instead.

GeneratedAt: 2026-02-05T20:59:58

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

## 2026-02-05 10:34:33 - Main Session

**Decisions & Changes:**
- OpenClaw status Overview ?뚢??????????????????р???????????????????????????????????????????????????????????????????????????????????????????????????????Ite...
- # ???꾨즺?먯뒿?덈떎! ## ?뱤 **Cron Jobs 紐⑤뜽 蹂寃??꾨즺** ``` Sessions ?쒋? Main (濡쒖뺄)              : claude-haiku-4-5 ?쒋? Discord 梨꾨꼸             : delivery-mirror (OpenAI ...
- System: [2026-02-05 10:18:43 GMT+9] Exec completed (briny-gl, code 0) :: ??????????????????????????????????????????닳?????????닳???????????닳???????????????...

**Key Learnings:**
- {   "status": "error",   "tool": "edit",   "error": "Missing required parameter: newText (newText or new_string)" }
- {   "status": "error",   "tool": "edit",   "error": "Missing required parameter: newText (newText or new_string)" }
- {   "status": "error",   "tool": "edit",   "error": "Could not find the exact text in C:\\Users\\user\\.openclaw\\agents\\main\\sessions\\sessions.jso...

**Next Steps:**
- [Thu 2026-02-05 10:32 GMT+9] context rest discord , main ?대윴?앹쑝濡?留먰븯硫?洹??몄뀡??而⑦뀓?ㅽ듃瑜?珥덇린???섎룄濡앺빐. 洹몃━怨?而⑦뀓?ㅽ듃瑜??붿빟?댁꽌 0.5k ?좏겙?쇰줈 以꾩뿬??memory.md????μ떆?ㅻ뒗 skill??留뚮뱾怨좎떢?? c...
- Successfully wrote 2328 bytes to C:\\Users\\user\\bot\\skills\\context-summarize-memory\SKILL.md

## 🛡️ Discord Admin Skill (discord-admin)

## 🌐 Discord Browser Skill (discord-browser)

디스코드에서 OpenClaw **브라우저(openclaw 프로필)**를 안전한 문법으로 제어하는 스킬.

### Discord에서 입력하는 커맨드
- `?command` → 커맨드 목록 출력
- `?browser start`
- `?browser open <url>`
- `?browser navigate <url>`
- `?browser snapshot`
- `?browser click <ref>`
- `?browser type <ref> <text>`
- `?browser press <key>`
- `?browser stop`

### 안전 규칙(요약)
- `http(s)`만 허용, `file://`, `chrome://`, `about:` 등 차단
- `localhost` 및 사설 IP 대역 차단(SSRF 방지)
- 비밀번호/토큰 등 민감정보 입력 요청은 거부


디스코드에서 **임의 PowerShell 실행은 금지**하고, 아래 **허용된 명령만** 실행하도록 만든 안전한 관리자 스킬.

### Discord에서 입력하는 커맨드(allowlist)
- `?command` → 커맨드 목록 출력
- `?gateway status`
- `?gateway restart` *(2-step confirm 필요)*
- `?model show`
- `?model set <provider/model>` *(2-step confirm 필요)*
  - 예: `?model set openai-codex/gpt-5.2`

### 내부에서 수행되는 동작(요약)
- `?gateway status` → `openclaw gateway status` 실행
- `?gateway restart` → `gateway action=restart`
- `?model show` → `gateway action=config.get` 후 `agents.defaults.model.primary` 표시
- `?model set ...` → `gateway action=config.patch`로 `agents.defaults.model.primary` 변경(적용 과정에서 재시작 발생)

### 운영 메모
- OpenClaw에서 `!`는 bash alias라서 Discord 명령 prefix로 쓰면 충돌할 수 있음 → `?gateway ...`, `?model ...` 권장.
- `gateway stop`은 디스코드에서 실행하면 게이트웨이가 꺼져서 **다시 켤 통로가 사라질 수 있으므로** 지원하지 않는 방향이 안전.


