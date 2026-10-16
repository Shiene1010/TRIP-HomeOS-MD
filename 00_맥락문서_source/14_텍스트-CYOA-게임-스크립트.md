프로젝트 전체 구조와 노드·엣지 관계, 그리고 바로 실행할 수 있는 텍스트 CYOA 게임 스크립트입니다.

📁 디렉토리 및 파일 구조 (Project File Tree)

text
trip-homeos-cyoa/
├── README.md
├── world/
│   └── universal_anchors.md
├── episodes/
│   ├── ep1_morning_spill.md
│   ├── ep2_bus_transit.md
│   └── ep3_evening_homework.md
├── graph/
│   └── nodes_and_edges.md
└── demo/
    └── text_cyoa_runner.txt
Use code with caution.

📄 1. world/universal_anchors.md


Universal Anchor Set (공통 세계관)


Child Token

• Dodo (도도)

Role Tokens

• Mom (엄마)
• Dad (아빠)
• Uncle (삼촌)
• Grandma (할머니)
• Teacher (선생님)

Space Tokens

• The Kitchen Table (식탁)
• The Front Door (현관)
• The Bus Stop (버스 정류장)
• The Classroom (교실)

Object Tokens

• The milk cup (우유 컵)
• The blue towel (파란 수건)
• The yellow bus (노란 버스)
• The red folder (레드 폴더)

📄 2. graph/nodes_and_edges.md


Node and Edge State Graph


Node Definition (Node ID)

• NODE_START: 호칭 선택 진입점
• EP1_CHOICE: 07:45 AM 우유 쏟음 상황
• EP1_RECOVERY: 지각 위기 응급 수습
• EP2_CHOICE: 15:30 PM 셔틀 대기 상황
• EP3_CHOICE: 19:30 PM 과제 및 디바이스 잠금
• NODE_END: 일과 완료 및 피드백 요약

Edge Transition Rules (If-Then-Else)

1. NODE_START --(Select Role)--> EP1_CHOICE
2. EP1_CHOICE --(IP = Yes)--> EP2_CHOICE
3. EP1_CHOICE --(IP = No / Delay > 5m)--> EP1_RECOVERY -> EP2_CHOICE
4. EP2_CHOICE --(IP = Yes)--> EP3_CHOICE
5. EP3_CHOICE --(IP = Yes)--> NODE_END

📄 3. episodes/ep1_morning_spill.md


Episode 1: Morning Rush (07:45 AM)

• Context: Dodo spilled milk near the table. Shoes are off.

Mom-mode Variant

• T: The milk cup slipped near Dodo.
• R: 1. Dodo, wipe the milk off with the blue towel. 2. Put sneakers on by the front door.
• IP: Is the kitchen table dry? [1: Yes / 2: No]

Dad-mode Variant

• T: The bus leaves in 5 minutes.
• R: Wipe spill, wear shoes, stand by the front door.
• IP: Are shoes on? [1: Yes / 2: No]

Uncle-mode Variant

• T: Table is wet.
• R: Finish wiping first, then grab your backpack, Dodo.
• IP: Can we leave before wiping? [1: Yes-No / 2: No]

Grandma-mode Variant

• T: The floor near Dodo is wet and cold.
• R: Step back. Use the blue towel, Dodo.
• IP: Did you step back safely? [1: Yes / 2: No]

Teacher-mode Variant

• T: Spill detected at station.
• R: 1. Apply towel to surface. 2. Place footwear in position.
• IP: Is surface clear? [1: Yes / 2: No]

🎮 4. demo/text_cyoa_runner.txt (텍스트 CYOA 플레이 시연)

text
==================================================
[TRIP HomeOS CYOA Engine v1.0] - Universal Dodo Edition
==================================================

[STEP 0] Select Your Voice (Enter 1-5):
1. 👩 Mom (엄마표)
2. 👨 Dad (아빠표)
3. 🧔 Uncle (삼촌표)
4. 👵 Grandma (할머니표)
5. 👩‍🏫 Teacher (선생님표)

> [User Input]: 1 (Mom selected)

--------------------------------------------------
[EPISODE 1] 07:45 AM - Kitchen & Front Door
--------------------------------------------------
[T - Story] : The milk cup slipped near Dodo.
[R - Action]: 
  1. Dodo, wipe the milk off with the blue towel.
  2. Put sneakers on by the front door.
[IP - Check]: Is the kitchen table dry? (Type Y or N)

> [Child/User Input]: Y

[System Log] -> Compliance Latency: 32s | Stress: 0
Transitioning to -> [EPISODE 2]

--------------------------------------------------
[EPISODE 2] 15:30 PM - Bus Stop
--------------------------------------------------
[T - Story] : The yellow shuttle arrives at the bus stop.
[R - Action]: If clock shows 3:35, Dodo walks to the bus stop.
[IP - Check]: Where are you at 3:35? (Type 'Bus stop' or 'Play')

> [Child/User Input]: Bus stop

[System Log] -> Slot Lock: Verified | Code-mix Error: 0%
Transitioning to -> [EPISODE 3]

--------------------------------------------------
[EPISODE 3] 19:30 PM - Homework Desk
--------------------------------------------------
[T - Story] : The red folder is open.
[R - Action]: 
  1. Write three sentences, Dodo.
  2. Close folder.
[IP - Check]: Are three sentences done? (Type Y or N)

> [Child/User Input]: Y

==================================================
[SESSION COMPLETE] All 3 Trips Cleared!
Daily Friction Score: 0/14 (Optimal)
==================================================