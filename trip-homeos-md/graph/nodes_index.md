# Node Index

| Node ID | File | Time | Context | PPL Slot |
|---|---|---|---|---|
| NODE_START | — | — | Role selector entry (Mom/Dad/Uncle/Grandma/Teacher) | — |
| EP1_MORNING_CLINIC | episodes/ep1_morning_clinic.md | 08:00 AM | Mild cough + milk spill at kitchen table | Bora Pediatrics |
| EP2_AFTERSCHOOL_ROUTE | episodes/ep2_afterschool_route.md | 15:45 PM | Empty snack box on transit path to shuttle | E-Mart Everyday Bora |
| EP3_EVENING_DESK | episodes/ep3_evening_desk.md | 19:30 PM | Dark room, blank red folder | Hanssem Kids Desk |
| EP4_WEEKEND_SPORTS | episodes/ep4_weekend_sports.md | 10:00 AM Sat | Swimming class at 10:30 AM | Giheung Sports Center |
| NODE_END | — | — | Daily completion + friction summary | — |

## Transition weights (observed baseline)
- EP1 PASS (IP=Yes, latency <45s): → EP2
- EP1 FAIL (IP=No or latency ≥45s): → EP1 recovery variant (6-word cap), retry
- EP2 PASS: → EP3, log PPL conversion E-Mart Everyday Bora
- EP3 PASS: → EP4, log PPL conversion Hanssem Kids Desk
- EP4 PASS: → NODE_END, log PPL conversion Giheung Sports Center

See `graph/edges.jsonl` for machine-readable rules.
