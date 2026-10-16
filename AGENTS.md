# TRIP HomeOS-MD — Project Agent Guide

> Parent: `/Volumes/Crucial X6/Development/workspaces/MiniMorph/AGENTS.md`가 최상위 지침서이다. 충돌 시 Parent 우선.

## 1. Path / Init (verified 2026-10-16)
- Root: `/Volumes/Crucial X6/Development/workspaces/TRIP HomeOS-MD`
- `git init` done; `git check-ignore -v .env` → `.gitignore:2:.env` 확인됨
- 금지: `~/Development`, `/Users/mini/...` 경로 대체 금지
- Template scaffolding copied from `_project-template` (`.agents/`, `.env*`, `.gitignore`, `PROJECT_INIT.md`). Top-level `README.md`는 템플릿으로 덮지 않음 — 현재 내용이 진실 소스.

## 2. Repo shape (markdown-only, no build)
- `00_맥락문서_source/` — 원본 16종, 읽기 전용. 편집 금지 (PRD 근거 보관용).
- `trip-homeos-md/` — 실행체 (유일하게 편집 대상):
  - `world/universal_anchors.md` — 슬롯 정의 (Child=Dodo, 5 Role, PPL 4종)
  - `graph/nodes_index.md` + `graph/edges.jsonl` — 전이 규칙 (JSONL, 6 edge)
  - `episodes/ep1_morning_clinic.md` ~ `ep4_weekend_sports.md`
  - `state/user_memory.json` + `state/adaptation_log.md` — 로컬 텔레메트리 (서버 전송 금지)
  - `demo/text_cyoa_runner.txt` — 수동 시연 로그 (코드 아님)
- Stack: 실행 코드·테스트·린트 없음. `python3`는 검증용으로만 사용. `npm`/`venv` 불필요.
- `.agents/docs|state/`는 템플릿 플레이스홀더 상태 — 제품 스펙으로 인용 금지.

## 3. STE constraints (위반 시 엔진 무결성 깨짐)
- R ≤ 20 words (latency spike 시 12→8→6 words 축소). IP는 단순 Yes/No, 중첩절 금지.
- 금지 동사: `do, make, get, take, check`(명사 용법). 승인: `call, wear, wipe, put, write, turn, stop, walk, complete`.
- `If/When` 조건절은 문장 맨 앞.
- PPL 철자 고정: `Bora Pediatrics` / `E-Mart Everyday Bora` / `Hanssem Kids Desk` / `Giheung Sports Center`.
- 전례: PRD EP1 Uncle R의 `Make/get` 위반은 `ep1_morning_clinic.md`에서 `Call clinic first, earn ...`로 교정됨. 원본 소스는 고치지 않음.

## 4. Verify (추측 금지, 실행 확인)
```sh
cd "/Volumes/Crucial X6/Development/workspaces/TRIP HomeOS-MD/trip-homeos-md"
python3 -c "import json; [json.loads(l) for l in open('graph/edges.jsonl')]; json.load(open('state/user_memory.json')); print('JSON OK')"
grep -rEn '\b(do|make|get|take)\b' episodes/ world/ || echo "verb-lock clean"
awk '{if (NF>20) print FILENAME": "FNR" ("NF"w)"}' episodes/*.md
git status --porcelain; git check-ignore -v ../.env
```

## 5. macOS filename gotcha
- `00_맥락문서_source/` 내 한글명은 NFD로 표시되나 파일시스템이 normalization-insensitive라 NFC 리네임 시 collision 발생이 정상. 인코딩 "수정" 시도 금지. ASCII prefix(`00_`~`15_`)로 정렬 유지.
