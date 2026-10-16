
TRIP HomeOS-MD: Interactive Demo & Native PPL Engine

Technical & Product Specification (v1.0)
Target Environment: Zero-Network, On-Device Local-First Markdown Engine with Implicit Telemetry Calibration

1. System Architecture & Privacy Guarantee


1.1 Local-First State Machine

• Zero-Cloud Telemetry: No user voice, raw text, child name, or location logs are transmitted to external servers. All parsing, latency tracking, and state transitions execute within the client runtime (IndexedDB + localStorage).
• Volatile Memory: Session logs (adaptation_log.md equivalent in memory) auto-purge at midnight local time.
• Slot-Token Architecture: Raw input is sanitized via local regex/dictionary matching before rendering. User entities are strictly bound to local slot variables ({CHILD}, {ROLE}, {SPACE}, {OBJECT}, {PPL_POI}).

1.2 Directory & File Manifest

text
trip-homeos-md/
├── README.md
├── world/
│   └── universal_anchors.md       # Base entity slots & default PPL mappings
├── graph/
│   ├── nodes_index.md             # Node metadata & transition weights
│   └── edges.jsonl                # Conditional edge rules (If-Then-Else + Latency thresholds)
├── episodes/
│   ├── ep1_morning_clinic.md      # 08:00 AM PPL: Bora Pediatrics + Milk
│   ├── ep2_afterschool_route.md   # 15:45 PM PPL: E-Mart Everyday Bora
│   ├── ep3_evening_desk.md        # 19:30 PM PPL: Hanssem Kids Desk
│   └── ep4_weekend_sports.md      # 10:00 AM PPL: Giheung Sports Center
└── state/
    ├── user_memory.json           # Local telemetry (role velocity, IP latency, PPL conversion)
    └── adaptation_log.md          # Real-time self-calibrating markdown stream
Use code with caution.

2. Universal Anchor & PPL Injection Schema (world/universal_anchors.md)

markdown
# Universal Anchor Set & Hyper-Local PPL Bindings

## Core Tokens
* {CHILD}      = "Dodo" (도도)
* {ROLE}       = ["Mom", "Dad", "Uncle", "Grandma", "Teacher"]

## Hyper-Local PPL Slot Map (Giheung / Bora-dong Baseline)
* {CLINIC}     = "Bora Pediatrics" (보라소아과)
* {RETAIL}     = "E-Mart Everyday Bora" (이마트에브리데이 보라점)
* {FURNITURE}  = "Hanssem Kids Desk" (한샘 키즈데스크)
* {FACILITY}   = "Giheung Sports Center" (기흥구민체육센터)

## Constraint Rules (ASD-STE100 Subset)
* Max Words per Procedure (R): 20 words (12 words if latency spike detected)
* Prohibited Verbs: do, make, get, take, check-as-noun
* Conditional Rule: Always place `If / When` clause at sentence index 0.
Use code with caution.

3. Episode Markdown Specifications (episodes/*.md)


📄 episodes/ep1_morning_clinic.md

markdown
# Node: EP1_MORNING_CLINIC (08:00 AM)
* Context: Mild cough + milk spill at kitchen table.

## Variants by Role (T - R - IP)

### [Mom] (Default Matrix: B-1-L-S1-P)
* T: Dodo has a mild cough. Milk cup slipped on the kitchen table.
* R: 
  1. Call Bora Pediatrics for a 9 AM slot. Wear the mask.
  2. Wipe the milk off with the blue towel.
* IP: Is the clinic booked and table dry? [1: Yes / 2: No]

### [Dad] (Strict Condition Mode)
* T: 8 AM departure. Cough reported.
* R: Book Bora Pediatrics now. Wear mask, walk to car.
* IP: Is mask on? [1: Yes / 2: No]

### [Uncle] (Mission Deal Mode)
* T: Morning cough.
* R: Make clinic call first, get 5 min extra tablet time.
* IP: Did you call Bora Pediatrics? [1: Yes / 2: No]

### [Grandma] (Visual Safety Mode)
* T: Dodo coughs near the wet table.
* R: Step back from milk. Wear warm coat and mask.
* IP: Are you wearing the mask? [1: Yes / 2: No]

### [Teacher] (Formal STE Protocol)
* T: Health symptom and surface spill logged.
* R: 
  1. Execute medical notification to Bora Pediatrics.
  2. Apply absorbent towel to surface.
* IP: Are protocols completed? [1: Yes / 2: No]

## Recovery Fallback Variant (Triggered if Latency > 45s or IP = No)
* R_Recovery: "Wear mask. Step to door." (6 words cap)
Use code with caution.

📄 episodes/ep2_afterschool_route.md

markdown
# Node: EP2_AFTERSCHOOL_ROUTE (15:45 PM)
* Context: Empty snack box on transit path to shuttle.

## Variants by Role
* [Mom] T: The snack box is empty.  
  R: Stop at E-Mart Everyday Bora. Buy one milk carton.  
  IP: Did you buy the milk? [1: Yes / 2: No]
* [Dad] T: Transit stop in 3 minutes.  
  R: Enter E-Mart Everyday Bora, grab milk, exit fast.  
  IP: Is milk in bag? [1: Yes / 2: No]
* [Uncle] T: Afternoon hunger.  
  R: Pick milk at E-Mart Everyday Bora, walk with friends.  
  IP: Got the receipt? [1: Yes / 2: No]
* [Grandma] T: School ends.  
  R: Hold handrail, walk into E-Mart Everyday Bora.  
  IP: Are you safe inside? [1: Yes / 2: No]
* [Teacher] T: Transit waypoint active.  
  R: Execute supply stop at E-Mart Everyday Bora.  
  IP: Is waypoint cleared? [1: Yes / 2: No]
Use code with caution.

📄 episodes/ep3_evening_desk.md

markdown
# Node: EP3_EVENING_DESK (19:30 PM)
* Context: Dark room, blank red folder.

## Variants by Role
* [Mom] T: The room is dark. Red folder is open.  
  R: Turn on Hanssem desk lamp. Write three sentences.  
  IP: Is lamp on and writing done? [1: Yes / 2: No]
* [Dad] T: No games before study.  
  R: Power on Hanssem desk lamp, complete 3 lines.  
  IP: Folder verified? [1: Yes / 2: No]
* [Uncle] T: 3 sentences = game unlock.  
  R: Sit at Hanssem desk, write 3 lines, show verification.  
  IP: 3 sentences complete? [1: Yes / 2: No]
* [Grandma] T: Bedtime approaches.  
  R: Turn Hanssem desk lamp on, put red folder flat.  
  IP: Desk ready? [1: Yes / 2: No]
* [Teacher] T: Evening study session.  
  R: Illuminate Hanssem desk workspace. Execute writing task.  
  IP: Task submitted? [1: Yes / 2: No]
Use code with caution.

📄 episodes/ep4_weekend_sports.md

markdown
# Node: EP4_WEEKEND_SPORTS (10:00 AM Saturday)
* Context: Swimming class at 10:30 AM.

## Variants by Role
* [Mom] T: Swimming class starts at 10:30.  
  R: Pack towel in bag. Walk to Giheung Sports Center.  
  IP: Are you at the center? [1: Yes / 2: No]
* [Dad] T: 10:15 arrival target.  
  R: Grab bag, step out to Giheung Sports Center.  
  IP: Gear packed? [1: Yes / 2: No]
* [Uncle] T: Pool time.  
  R: Bring towel, head to Giheung Sports Center lobby.  
  IP: At lobby? [1: Yes / 2: No]
* [Grandma] T: Morning walk to pool.  
  R: Hold umbrella, walk straight to Giheung Sports Center.  
  IP: Walking safely? [1: Yes / 2: No]
* [Teacher] T: Athletic curriculum event.  
  R: Report to Giheung Sports Center check-in desk.  
  IP: Attendance logged? [1: Yes / 2: No]
Use code with caution.

4. Conditional Edge & Telemetry Rules (graph/edges.jsonl)

json
{"edge_id": "E01_START_TO_EP1", "from": "NODE_START", "to": "EP1_MORNING_CLINIC", "condition": "ROLE_SELECTED"}
{"edge_id": "E02_EP1_PASS", "from": "EP1_MORNING_CLINIC", "to": "EP2_AFTERSCHOOL_ROUTE", "condition": "IP == 1 && LATENCY < 45s", "action": "LOG_PPL_CONVERSION:Bora Pediatrics"}
{"edge_id": "E03_EP1_FAIL", "from": "EP1_MORNING_CLINIC", "to": "EP1_MORNING_CLINIC", "condition": "IP == 2 || LATENCY >= 45s", "action": "INJECT_RECOVERY_VARIANT"}
{"edge_id": "E04_EP2_PASS", "from": "EP2_AFTERSCHOOL_ROUTE", "to": "EP3_EVENING_DESK", "condition": "IP == 1", "action": "LOG_PPL_CONVERSION:E-Mart Everyday Bora"}
{"edge_id": "E05_EP3_PASS", "from": "EP3_EVENING_DESK", "to": "EP4_WEEKEND_SPORTS", "condition": "IP == 1", "action": "LOG_PPL_CONVERSION:Hanssem Kids Desk"}
{"edge_id": "E06_EP4_PASS", "from": "EP4_WEEKEND_SPORTS", "to": "NODE_END", "condition": "IP == 1", "action": "LOG_PPL_CONVERSION:Giheung Sports Center"}
Use code with caution.

5. Self-Calibrating Telemetry Log (state/adaptation_log.md Live Snapshot)

markdown
# Live Adaptation Log (Client-Side State Stream)
* Session ID: `S-20261016-BORA01`
* Inferred Matrix Anchor: `B-1-L-S1-P` (Confidence: 0.92)

## [08:00:12] EP1_MORNING_CLINIC
* Selected Role: `Mom`
* Rendered R: `1. Call Bora Pediatrics for a 9 AM slot. Wear the mask. 2. Wipe the milk off with the blue towel.`
* User Input: `1 (Yes)` | Latency: `28.4s`
* Status: `PASSED`
* PPL Verified Event: `Bora Pediatrics` -> Slot Conversion Recorded (CPA Trigger Ready)

## [15:45:05] EP2_AFTERSCHOOL_ROUTE
* Selected Role: `Mom`
* Rendered R: `Stop at E-Mart Everyday Bora. Buy one milk carton.`
* User Input: `2 (No)` | Latency: `62.1s`
* Status: `LATENCY SPIKE DETECTED`
* Calibration Action: Dynamic word cap reduced (`20 words` ➔ `8 words`). Next session triggers short-form R.
* PPL Event: `E-Mart Everyday Bora` -> Impression Logged (Non-converted, retrying via Mom-Dad handoff)

## [19:30:18] EP3_EVENING_DESK
* Role Shift Telemetry Suggestion: Auto-promoted `Dad` role due to evening time constraint.
* Selected Role: `Dad`
* Rendered R: `Power on Hanssem desk lamp, complete 3 lines.`
* User Input: `1 (Yes)` | Latency: `14.2s`
* Status: `OPTIMAL PASSED`
* PPL Verified Event: `Hanssem Kids Desk` -> Verified Completion

## [10:00:00 Sat] EP4_WEEKEND_SPORTS
* Selected Role: `Mom`
* Rendered R: `Pack towel in bag. Walk to Giheung Sports Center.`
* User Input: `1 (Yes)` | Latency: `21.0s`
* Status: `PASSED`
* PPL Verified Event: `Giheung Sports Center` -> Verified Completion
Use code with caution.

6. Business & PPL Performance Metrics (WICA KPI Specification)


Metric Code	Definition	Target Benchmark	Measurement Method
VFR (Vocal Friction Rate)	Daily parent nagging occurrences	< 3.0 / day (Down from 14.0)	Local input frequency counter
CL (Compliance Latency)	Time from R render to IP Yes click	< 30 seconds	Client timestamp delta
P-CPA (Protocol-Verified CPA)	Action completion rate on PPL slots	> 74% conversion	IP Yes confirmation per POI tag
CM-Err (Code-Mixing Error)	Unauthorized L1/L2 or unapproved verb usage	0.0%	Regex validator against STE dictionary