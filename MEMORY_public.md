# MEMORY_public.md

This file is auto-generated from MEMORY.md with secrets redacted.
Do NOT add secrets here. Edit MEMORY.md instead.

GeneratedAt: 2026-02-05T20:24:08

﻿# MEMORY.md - Long-Term Memory

## (Operational notes moved)
- Operational/playbook-style notes were moved to `AGENTS.md` under **"Operational Playbook"**.
- `MEMORY.md` should focus on durable facts/decisions/IDs/state.

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
   - **Fixed 2026-02-05:** 브랜치명 `master`→`main` 변경, unused `requests` import 제거, Windows 한글 콘솔 UTF-8 출력(Wrapper) 적용
   - Discord notification to file at `C:\Users\user\bot\work\text\git_push_notification.txt`

### Python Path & Encoding
- **Python (Miniconda):** `C:\Users\user\miniconda3\python.exe`
- **Encoding fix applied:** UTF-8 wrapper in git_push_auto.py for Windows Korean console

### Python Path
- **Python (Miniconda):** `C:\Users\user\miniconda3\python.exe`
- **NumPy 파일 분석:** `spectra_latest_1.npy`의 유효 데이터 행 수 N=44998 (약 361MB, LFS)

## 🔧 Spectra Sync Automation (2026-02-05 OPTIMIZED)

### 최적화된 구조
- **공유 Python 스크립트 위치:** `C:\Users\user\bot\skills_scripts\`
- **Skill 폴더 위치:** `C:\Users\user\bot\skills\`
- **Cron Jobs:** 각 skill을 **2시간마다** 실행

### Cron Jobs (모두 Skill 호출 방식으로 변경 완료)

| Cron Job ID | 실행 Skill | 실행 스크립트 | 상태 |
|---|---|---|---|
| 410f89b2-8bf8-4d6f-880d-1e385b7c212b | spectra-snapshot-sync | spectra_snapshot_sync.py | (2026-02-05 11:02) 반영 |
| 958f2b00-33ca-4b3d-8386-e0ba387dfcec | spectra-git-push | spectra_git_push_update.py | (2026-02-05 11:02) 반영 |
| 616f4640-d4dc-484d-9f45-4bb5ab42fa19 | git-push-data-cr | git_push_auto.py | (2026-02-05 11:02) 반영 |

**구조 변경 요약**
- 이전: `Cron이 Python 스크립트를 직접 실행`
- 현재: `Cron이 Skill을 호출 → Skill이 Python 스크립트 실행`

### Skill 목록 (요약)

#### 1) context-reset
- 위치: `C:\Users\user\bot\skills\context-reset\`
- 기능: 세션 컨텍스트 초기화
  - 명령: `context reset discord` 또는 `context reset main`

#### 2) context-summarize-memory
- 위치: `C:\Users\user\bot\skills\context-summarize-memory\`
- 기능: 현재 컨텍스트 요약 후 `MEMORY.md`에 저장

#### 3) spectra-snapshot-sync
- 위치: `C:\Users\user\bot\skills\spectra-snapshot-sync\`
- 스크립트: `C:\Users\user\bot\skills_scripts\spectra_snapshot_sync.py`
- 기능: `spectra_latest_1.npy` 스냅샷 복사 + git 커밋/푸시
- 주기: 2시간

#### 4) spectra-git-push
- 위치: `C:\Users\user\bot\skills\spectra-git-push\`
- 스크립트: `C:\Users\user\bot\skills_scripts\spectra_git_push_update.py`
- 기능: PHS repo로 `spectra_latest_1.npy` 복사 + git 커밋/푸시
- 주기: 2시간

#### 5) git-push-data-cr
- 위치: `C:\Users\user\bot\skills\git-push-data-cr\`
- 스크립트: `C:\Users\user\bot\skills_scripts\git_push_auto.py`
- 기능: PHS repo 자동 커밋/푸시
- 주기: 2시간

### 새 Skill 생성 체크리스트
- [ ] 공용 Python 스크립트는 `C:\Users\user\bot\skills_scripts\`에 둔다
- [ ] Skill 폴더는 `C:\Users\user\bot\skills\[skill-name]\`에 만든다
- [ ] `SKILL.md`에 실행 커맨드/경로를 명확히 적는다
- [ ] Windows 콘솔 한글 깨짐 방지: stdout UTF-8 wrapper 적용
  ```python
  import sys
  sys.stdout = __import__('io').TextIOWrapper(sys.stdout.buffer, encoding='utf-8')
  ```
- [ ] Miniconda Python으로 테스트:
  ```bash
  C:\Users\user\miniconda3\python.exe C:\Users\user\bot\skills_scripts\[script_name].py
  ```
- [ ] 필요한 경우 `MEMORY.md`에 “결정/ID/상태”만 요약해서 추가

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


