# Universal Anchor Set & Hyper-Local PPL Bindings

Source: `00_맥락문서_source/00_TRIP-HomeOS-MD-PRD.md` §2 + `01_공통-초기값-세계관.md`

## Core Tokens
- `{CHILD}` = "Dodo" (도도) — 나이/학년 중립형 아명
- `{ROLE}` = ["Mom", "Dad", "Uncle", "Grandma", "Teacher"]

## Space Tokens (`{SPACE}`)
- The Kitchen Table (식탁)
- The Front Door (현관)
- The Bus Stop (버스 정류장)
- The Classroom (교실)

## Object Tokens (`{OBJECT}`)
- The milk cup (우유 컵)
- The blue towel (파란 수건)
- The yellow bus / shuttle (노란 버스 / 셔틀)
- The red folder (레드 폴더)

## Hyper-Local PPL Slot Map (Giheung / Bora-dong Baseline)
- `{CLINIC}` = "Bora Pediatrics" (보라소아과)
- `{RETAIL}` = "E-Mart Everyday Bora" (이마트에브리데이 보라점)
- `{FURNITURE}` = "Hanssem Kids Desk" (한샘 키즈데스크)
- `{FACILITY}` = "Giheung Sports Center" (기흥구민체육센터)

## Constraint Rules (ASD-STE100 Subset)
- Max words per Procedure (R): 20 words (12 words if latency spike, 8 words on EP2 fallback, 6 words on recovery variant)
- Prohibited verbs: do, make, get, take, check-as-noun
- Approved verbs: call, wear, wipe, put, write, turn, stop, walk, complete
- Conditional rule: Always place `If / When` clause at sentence index 0.
