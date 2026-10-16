# 키노트 시연 시나리오: 사용 → 광고BM 인젝션 (7분)
- 목표: 관객이 "쓰다 보니 광고가 동작한다"를 눈으로 확인. 배너 0회, STE 문장만.
- 소재: `trip-homeos-md/` 실파일 + `00_맥락문서_source/07_실전-광고-인젝션.md` 예시(EP3 수학 빈칸 3일 연속 No).

## 등장 요소
- 사용자: 맞벌이 가정, Mom-mode 기본 (앵커 `B-1-L-S1-P`)
- 엔진: `world/universal_anchors.md` → `episodes/` → `graph/edges.jsonl` → `state/adaptation_log.md`
- 광고주: 파트너 수학앱 (가명 `[Partner Math App]`), 과금 = IP Yes 완료 시 CPA 1건

## Scene 1 (1분): 일상 사용 — PPL이 지시문으로 녹는 순간
- 키노트 자막: "광고가 아니라 동선 지시"
- 러너 실행:
  - T: `Dodo has a mild cough. Milk cup slipped on the kitchen table.`
  - R: `1. Call Bora Pediatrics for a 9 AM slot. Wear the mask. 2. Wipe the milk off with the blue towel.`
  - IP: `Is the clinic booked and table dry? [1: Yes]` → 관객이 `1` 입력
- 로그: `PPL Verified: Bora Pediatrics → CPA 1건`. 멘트: "엄마는 병원 광고를 본 게 아니라, 아침 할 일을 끝냈다."

## Scene 2 (1분 30초): 마찰 발생 — 엔진이 배우는 지점
- EP2 하교길: `Stop at E-Mart Everyday Bora. Buy one milk carton.` → 관객 입력 `2 (No)`, 타이머 62s
- 화면 분할: 왼쪽 러너, 오른쪽 `state/adaptation_log.md`에 `LATENCY SPIKE → cap 20→8 words` 기록되는 장면
- EP3 진입 3일차 설정: "수학 빈칸 3일 연속 No" 자막. 기존 광고라면 여기서 배너가 뜨지만, 아무것도 안 뜸을 보여줄 것.

## Scene 3 (1분): 상태 벡터 — 서버가 모르는 것 (프라이버시 하이라이트)
- 화면에 전송되는 키만 표시:
  - `{ node: EP3_HOMEWORK, cond: math_blank x3, role: Dad, latency_band: high }`
- 멘트: "이름·주소·성적표는 기기 밖으로 안 나간다. 나가는 건 이 한 줄뿐이다."
- 대조 슬라이드: 전통 타깃팅(쿠키·GPS·30대 여성) vs TRIP(지금 막힌 상태).

## Scene 4 (1분 30초): 스폰서드 STE 인젝션 — 같은 말투로 제안
- 동일 Dad-mode 말투로 R만 교체 (배너 없음):
  - T: `The math page has three hard blocks.`
  - R: `1. Open [Partner Math App] for 5 minutes. 2. Write the answer.`
  - IP: `Is the block solved? [1: Yes / 2: No]`
- 원칙 자막 3줄: 슬롯 직결 / 동선 동기화 / 제어력 유지(≤20 words, 금지동사 없음).
- 관객 입력 `1` → 아이가 실제로 5분 풀고 답을 씀 (사전 녹화 10초 클립 재생 가능).

## Scene 5 (1분 30초): 완료 과금 — 클릭이 아니라 해결에 돈이 붙는다
- IP Yes 순간 `LOG_PPL_CONVERSION` → 광고주 대시보드에 `Verified Completion 1` 점등, CPM/CPC 0원 표시
- 실패 분기 데모 (선택): 관객이 `2`를 누르면 과금 0원 + 다음날 같은 R 재제안. "안 풀리면 광고주도 돈을 못 번다."
- 클로징 지표: `VFR 14→1/day, CL 18s, P-CPA 3/4, CM-Err 0%` + "잔소리는 줄고, 동네 가게·앱은 해결될 때만 벌었다."

## 진행자 치트시트
- 입력 실패 대비: 관객이 엉뚱한 키를 누르면 `R_Recovery: "Wear mask. Step to door."`로 수습 후 "이게 폴백"이라고 넘길 것.
- 시간 초과 시 Scene 2 로그 화면 생략, Scene 4→5 직행.
- Q&A 예상: "개인정보?" → Scene 3 키 재표시. "광고 거부감?" → Scene 1·4 동일 말투 강조.
