# TRIP HomeOS-MD — 실행 가능한 로컬-퍼스트 마크다운 엔진

Zero-network, on-device. 상세 스펙: `00_맥락문서_source/00_TRIP-HomeOS-MD-PRD.md`

## 구조
```
trip-homeos-md/
├── README.md
├── world/universal_anchors.md
├── graph/nodes_index.md
├── graph/edges.jsonl
├── episodes/ep1_morning_clinic.md
├── episodes/ep2_afterschool_route.md
├── episodes/ep3_evening_desk.md
├── episodes/ep4_weekend_sports.md
├── state/user_memory.json
├── state/adaptation_log.md
└── demo/text_cyoa_runner.txt
```

## STE 제약 (검증 규칙)
- R ≤ 20 words (latency spike 시 12/8/6 words로 축소)
- 금지 동사: do, make, get, take, check(명사 용법)
- `If / When` 조건절은 문장 맨 앞
- IP는 단순 Yes/No, 중첩절 금지
- PPL 토큰 철자 고정: Bora Pediatrics / E-Mart Everyday Bora / Hanssem Kids Desk / Giheung Sports Center

## KPI
- VFR < 3.0/day, CL < 30s, P-CPA > 74%, CM-Err 0.0%
