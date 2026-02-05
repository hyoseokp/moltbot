# MEMORY_public.md

This file is auto-generated from MEMORY.md with secrets redacted.
Do NOT add secrets here. Edit MEMORY.md instead.

GeneratedAt: 2026-02-05T19:26:24

﻿# MEMORY.md - Long-Term Memory

## ?쬇 OpenClaw Browser Extension

### Browser Automation Tip
- **Extension connection issue:** When browser extension disconnects (error: "tab not found"), can automatically click the extension icon using `browser act` action
- **How to use:** Instead of asking Hyoseok to manually click the extension icon, use:
  ```
  browser action=act request={"kind": "click", "ref": "<extension_icon_ref>"}
  ```
- **Benefit:** More efficient automation - no need to wait for manual clicks to reconnect extension
- **Status:** Discovered 2026-02-04, Hyoseok confirmed this method works

### Browser Control Limitations
- Extension CDP (Chrome DevTools Protocol) connection can be unstable
- Navigate works even when screenshot fails (tab not found error)
- Full page screenshots require stable tab connection
- Sometimes need browser restart to reset extension connection state

## ?뙋 Web Tools
- Use `web_fetch` for lightweight page access without browser automation
- Use `browser` action for interactive automation (navigate, screenshot, click)

## ?뱤 Jupyter Lab Integration
- Hyoseok uses Jupyter Lab with data_gen.ipynb for data visualization
- Located at: `http://localhost:8888/lab/workspaces/auto-r/tree/data_gen.ipynb`
- ?좑툘 **DO NOT use browser screenshot** - it halts running cells (CDP interference)
- Instead use PIL method (see below)

## ?벝 Screen Capture Method
- **Use PIL (Python Imaging Library)** instead of browser extension
- **Script location:** `C:\Users\user\bot\work\py\screenshot_pil.py`
- **How it works:** Uses Python PIL to capture full desktop screen
- **Advantage:** Zero interference with Jupyter execution, Chrome tabs stay unaffected
- **Command:** `powershell -NoProfile -Command "& 'C:\Users\user\miniconda3\python.exe' 'C:\Users\user\bot\work\py\screenshot_pil.py'"`
- **Output:** Screenshots saved to `C:\Users\user\.openclaw\media\screenshots\screenshot_YYYYMMDD_HHMMSS.png`
- **Status:** Verified working 2026-02-04 18:21 GMT+9

## 🧩 Skill Prompt Standard (for reliable automation)

When creating/updating skills (especially cron/automation skills), use this standard prompt/spec format:

- **Task**: what to do (one paragraph)
- **Steps**: ordered list (1..n)
- **Rules/Constraints**: hard requirements (what must/must not happen)
- **Outputs**: what to send/produce (e.g., Discord summary template)
- **Failure policy**: stop/continue/retry, and how to alert

(Keep it concise and deterministic. Prefer templates/checklists over prose.)

## 📁 Skill scripts location rule (recommended)

- **Default:** Put reusable/executable Python scripts in:
  - `C:\Users\user\bot\skills_scripts\`
- **Exception (allowed):** If a script is a *skill-private helper* (only used by one skill, not intended for reuse), it may live under that skill folder:
  - `C:\Users\user\bot\skills\<skill-name>\scripts\`

Rule of thumb:
- shared / cron-called / pipeline core → `bot\skills_scripts\`
- single-skill helper / internal tooling → `bot\skills\<skill>\scripts\`

## 🗂 bot 폴더 구조 (2026-02-05)

`C:\Users\user\bot` 아래는 OpenClaw/봇 관련 파일을 한 곳에 모아둔 디렉토리다.

- `archive\large\` : 실수로 생성된 대용량/이상한 이름 파일 보관
- `core-md\` : AGENTS/SOUL/USER/TOOLS/HEARTBEAT/IDENTITY/MEMORY/BOOTSTRAP 등 코어 md 원본(루트에는 하드링크로 남겨 호환 유지)
- `docs\` : 문서/메모
- `keys\` : 키 파일(예: sg980222)
- `skills\` : OpenClaw 스킬 폴더들(각 폴더에 SKILL.md)
- `skills_scripts\` : 스킬이 실행하는 파이썬 스크립트들
- `work\` : 실험/작업용 스크립트 및 파일들
  - `work\py\` : 파이썬 작업 스크립트
  - `work\ps1\` : PowerShell 스크립트
  - `work\bat\` : bat/cmd
  - `work\notebooks\` : ipynb
  - `work\text\` : txt/xml/js 등

현재 트리(요약):

```
C:\Users\user\bot
+---archive\large\
+---core-md\
+---docs\
+---keys\
+---skills\
|   +---context-reset\
|   +---context-summarize-memory\
|   +---git-pull-rebase\
|   +---git-push-data-cr\
|   +---spectra-count-n\
|   +---spectra-git-push\
|   +---spectra-snapshot-sync\
|   \---spectra-sync-all\
+---skills_scripts\
|   count_N.py
|   git_pull_rebase.py
|   git_push_auto.py
|   spectra_git_push_update.py
|   spectra_snapshot_sync.py
|   spectra_sync_all.py
\---work\
    +---bat\
    +---notebooks\
    +---ps1\
    +---py\
    \---text\
```

## 🔄 Spectra Sync Automation (2026-02-05 UPDATED)

### Three Cron Jobs Running Every 2 Hours:

1. **spectra_snapshot_sync** (ID: 410f89b2-8bf8-4d6f-880d-1e385b7c212b)
   - Copies `D:\dataset\spectra_result\spectra_latest_1.npy` ??`D:\dataset\data_CR_repo\spectra_latest_1.npy`
   - Runs git add/commit/push to main branch
   - Discord notification to channel 1468499965461663917
   - **Key:** Never touches spectra_latest_0.npy

2. **spectra-git-push** (ID: 958f2b00-33ca-4b3d-8386-e0ba387dfcec)
   - Runs `C:\Users\user\bot\work\py\spectra_git_push_update.py` from PHS directory
   - Handles special git push scenarios with fetch/pull fallback

3. **git-push-data-CR** (ID: 616f4640-d4dc-484d-9f45-4bb5ab42fa19)
   - Runs `C:\Users\user\bot\work\py\git_push_auto.py` from PHS directory
   - **Fixed 2026-02-05:** Changed master?뭢ain, removed unused requests import, added UTF-8 encoding fix
   - Discord notification to file at `C:\Users\user\bot\work\text\git_push_notification.txt`

### Python Path & Encoding
- **Python (Miniconda):** `C:\Users\user\miniconda3\python.exe`
- **Encoding fix applied:** UTF-8 wrapper in git_push_auto.py for Windows Korean console

### Python Path
- **Python (Miniconda):** `C:\Users\user\miniconda3\python.exe`
- **NumPy ?뚯씪 遺꾩꽍:** N=44998遺??紐⑤몢 0?쇰줈 梨꾩썙吏?(361 MB, LFS)

## ?봽 Spectra Sync Automation (2026-02-05 OPTIMIZED)

### 理쒖쟻?붾맂 援ъ“
- **Python Scripts ??μ냼:** `C:\\Users\\user\\bot\\skills_scripts\\`
- **Skill ??μ냼:** `C:\\Users\\user\\bot\\skills\\`
- **Cron Jobs:** 媛?Skill??2?쒓컙留덈떎 ?ㅽ뻾

### Cron Jobs (??紐⑤몢 Skill ?몄텧濡?蹂寃??꾨즺!)

| Cron Job ID | Skill ?몄텧 | ?ㅽ겕由쏀듃 | ?곹깭 |
|-------------|-----------|---------|------|
| 410f89b2-8bf8-4d6f-880d-1e385b7c212b | spectra-snapshot-sync | spectra_snapshot_sync.py | ???섏젙??(2026-02-05 11:02) |
| 958f2b00-33ca-4b3d-8386-e0ba387dfcec | spectra-git-push | spectra_git_push_update.py | ???섏젙??(2026-02-05 11:02) |
| 616f4640-d4dc-484d-9f45-4bb5ab42fa19 | git-push-data-cr | git_push_auto.py | ???섏젙??(2026-02-05 11:02) |

**援ъ“ 蹂寃?**
- ?댁쟾: `Cron ??湲??꾨＼?꾪듃 ??Python 吏곸젒 ?ㅽ뻾`
- ?꾩옱: `Cron ??媛꾨떒??Skill ?몄텧 ??Skill.md ??Python ?ㅽ뻾`

### Skill 紐⑸줉

#### 1. context-reset
```
?꾩튂: C:\\Users\\user\\bot\\skills\\context-reset\
湲곕뒫: ?몄뀡 而⑦뀓?ㅽ듃 ?꾩쟾 珥덇린??紐낅졊: "context reset discord" ?먮뒗 "context reset main"
```

#### 2. context-summarize-memory
```
?꾩튂: C:\\Users\\user\\bot\\skills\\context-summarize-memory\
湲곕뒫: ?몄뀡 ?붿빟 ??MEMORY.md ???紐낅졊: "context ?붿빟 諛??κ린湲곗뼲???
```

#### 3. spectra-snapshot-sync
```
?꾩튂: C:\\Users\\user\\bot\\skills\\spectra-snapshot-sync\
?ㅽ겕由쏀듃: C:\\Users\\user\\bot\\skills_scripts\\spectra_snapshot_sync.py
湲곕뒫: spectra_latest_1.npy ?숆린??+ git ?몄떆
鍮덈룄: 2?쒓컙留덈떎
```

#### 4. spectra-git-push
```
?꾩튂: C:\\Users\\user\\bot\\skills\\spectra-git-push\
?ㅽ겕由쏀듃: C:\\Users\\user\\bot\\skills_scripts\\spectra_git_push_update.py
湲곕뒫: PHS ?붾젆?좊━ spectra ?뚯씪 ?몄떆
鍮덈룄: 2?쒓컙留덈떎
```

#### 5. git-push-data-cr
```
?꾩튂: C:\\Users\\user\\bot\\skills\\git-push-data-cr\
?ㅽ겕由쏀듃: C:\\Users\\user\\bot\\skills_scripts\\git_push_auto.py
湲곕뒫: PHS ??μ냼 ?먮룞 而ㅻ컠 諛??몄떆
鍮덈룄: 2?쒓컙留덈떎
```

### ?ㅽ궗 ?앹꽦 泥댄겕由ъ뒪??- [ ] Python ?ㅽ겕由쏀듃: `C:\\Users\\user\\bot\\skills_scripts\\` (怨듭쑀 寃쎈줈)?????- [ ] Skill ?대뜑: `C:\\Users\\user\\bot\\skills\\[skill-name]\` ?앹꽦
- [ ] SKILL.md ?묒꽦 (name + description + ?ㅽ겕由쏀듃 寃쎈줈 紐낆떆)
- [ ] UTF-8 ?몄퐫???섑띁 異붽? (Windows ?쒓? ???
  ```python
  import sys
  sys.stdout = __import__('io').TextIOWrapper(sys.stdout.buffer, encoding='utf-8')
  ```
- [ ] Skill??SKILL.md???ㅽ겕由쏀듃 ?ㅽ뻾 紐낅졊 湲곕줉:
  ```bash
  C:\Users\user\miniconda3\python.exe C:\\Users\\user\\bot\\skills_scripts\\[script_name].py
  ```
- [ ] Miniconda Python?쇰줈 ?뚯뒪??(`C:\Users\user\miniconda3\python.exe`)
- [ ] MEMORY.md Skill 紐⑸줉??異붽?

## ?㎛ Key Technical Notes
- GLM 4.7 紐⑤뜽 ?ъ슜 以?(?꾩옱??gpt-5.2濡?蹂寃??꾨즺)
- Discord 梨꾨꼸: 1468499965461663917 (紐고듃遊??곌뎄)
- OpenClaw v2026.2.1
- **Python Runtime:** `C:\Users\user\miniconda3\python.exe`

## ?뱥 紐낅졊???⑦꽩
- **"openclaw status"** ????긽 `openclaw status` 紐낅졊 ?ㅽ뻾?댁꽌 Channels & Sessions ?뺣낫 蹂댁뿬二쇨린
- ?ㅽ뻾 諛⑸쾿: `exec command="openclaw status"`

- **"N媛?泥댄겕"** ??spectra_latest_1.npy??理쒖떊 N媛?0?쇰줈 梨꾩썙吏湲??쒖옉 ?몃뜳?? ?뚮젮二쇨린
- 紐낅졊?? `check_n_value.py` ?ㅽ뻾
- ?덉쟾 N媛? 44998 (2026-02-04 20:51 ?뺤씤??

## ?뵍 沅뚰븳 臾몄젣 ?닿껐梨?(2026-02-04)

### Windows ?쒖뒪???뱀꽦
- Windows?먯꽌 **sudo 紐낅졊???놁쓬**
- 愿由ъ옄 沅뚰븳???꾩슂???묒뾽? "愿由ъ옄濡??ㅽ뻾" ?꾩슂

### 沅뚰븳 ?닿껐梨?1. **?ㅽ뻾 ??愿由ъ옄 沅뚰븳:**
   - ?뚯씪 ?고겢由???"愿由ъ옄濡??ㅽ뻾"
   - ?먮뒗 PowerShell?먯꽌 "愿由ъ옄 沅뚰븳?쇰줈 ?ㅽ뻾"

2. **Task Scheduler 沅뚰븳:**
   - ?묒뾽 ?앹꽦 ??`/ru SYSTEM` ?ъ슜
   - `/rl HIGHEST`濡??곗꽑?쒖쐞 理쒓퀬 ?ㅼ젙
   - ?깅줉?섎㈃ GUI(`taskschd.msc`)?먯꽌 ?뺤씤 媛??
3. **PowerShell 愿由ъ옄 沅뚰븳 ?ㅽ뻾:**
   ```powershell
   Start-Process powershell -Verb RunAs -ArgumentList "-NoProfile", "-Command", "紐낅졊??
   ```

### ?κ린 硫붾え由?- ?묒뾽 ?ㅼ?以꾨윭 ?깅줉 臾몄젣 沅뚰븳 ??愿由ъ옄 沅뚰븳 ?뺤씤
- ?뚯씪 蹂듭궗/?곌린 臾몄젣 TEMP 寃쎈줈 ?닿껐

---

*Updated: 2026-02-04 21:25*
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


