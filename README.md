# TRIP HomeOS-MD

정리일: 2026-10-16 / 원본 16개 문서 → 소스 + 실행체 분리

## 폴더 구성
- `00_맥락문서_source/` — 원본 16종 (개념·매트릭스·PPL·데모, 읽기 전용 권장)
  - `00_TRIP-HomeOS-MD-PRD.md` — 전체 PRD/스펙 v1.0 (실행체 생성 근거)
  - `01_~02_` — 세계관·TRIP체인 정의
  - `03_~05_` — STE 원칙·그레이드/페르소나 매트릭스
  - `06_~07_` — PPL/광고 인젝션 원칙
  - `08_~11_` — 노드/엣지·프롬프트·실행명령·체크리스트
  - `12_~15_` — 적응로그·러너 데모·CYOA 스크립트/시연
- `trip-homeos-md/` — PRD §1.2대로 생성된 실행 가능한 엔진 (world/graph/episodes/state/demo)

## 핵심 요약
- 목표: Zero-network 로컬-퍼스트 STE 명령 엔진. 잔소리→조건+행동 단문, Working Memory 절약, IP로 핑계 차단.
- 슬롯: Child=Dodo, Role 5종, Space/Object 4종씩, PPL 4종(보라소아과/이마트에브리데이 보라점/한샘키즈데스크/기흥구민체육센터).
- 루프: T(스토리) → R(구동사 명령, ≤20단어) → IP(Yes/No) → edges.jsonl 분기 → adaptation_log 보정.
- 개인화: B-1-L-S1-P(초저 맞벌이 공립형)가 기본 앵커. Role Velocity·IP latency로 암묵 보정, 서버 저장 없음.
- BM: 배너 대신 STE 문장에 PPL 슬롯 직결, IP Yes 완료 시에만 CPA 과금.

## 발견된 이슈 1건 (수정함)
- PRD EP1 Uncle R이 금지동사 위반 (`Make clinic call first, get 5 min...`) → `trip-homeos-md/episodes/ep1_morning_clinic.md`에서 `Call clinic first, earn 5 min extra tablet time.`으로 교정. 원본은 유지.

## 다음 작업 제안
1. `graph/edges.jsonl` + `state/user_memory.json` 파서 검증 스크립트 추가
2. EP1~EP4 R/IP 전수 STE 검증 (20단어·금지동사·If선행)
3. CYOA 러너를 실제 `.py/.js`로 구현할지 결정
