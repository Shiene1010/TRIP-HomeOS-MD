# Node: EP1_MORNING_CLINIC (08:00 AM)
- Context: Mild cough + milk spill at kitchen table.

## Variants by Role (T - R - IP)

### [Mom] (Default Matrix: B-1-L-S1-P)
- T: Dodo has a mild cough. Milk cup slipped on the kitchen table.
- R:
  1. Call Bora Pediatrics for a 9 AM slot. Wear the mask.
  2. Wipe the milk off with the blue towel.
- IP: Is the clinic booked and table dry? [1: Yes / 2: No]

### [Dad] (Strict Condition Mode)
- T: 8 AM departure. Cough reported.
- R: Book Bora Pediatrics now. Wear mask, walk to car.
- IP: Is mask on? [1: Yes / 2: No]

### [Uncle] (Mission Deal Mode)
- T: Morning cough.
- R: Call clinic first, earn 5 min extra tablet time.
- IP: Did you call Bora Pediatrics? [1: Yes / 2: No]

### [Grandma] (Visual Safety Mode)
- T: Dodo coughs near the wet table.
- R: Step back from milk. Wear warm coat and mask.
- IP: Are you wearing the mask? [1: Yes / 2: No]

### [Teacher] (Formal STE Protocol)
- T: Health symptom and surface spill logged.
- R:
  1. Execute medical notification to Bora Pediatrics.
  2. Apply absorbent towel to surface.
- IP: Are protocols completed? [1: Yes / 2: No]

## Recovery Fallback Variant (Triggered if Latency > 45s or IP = No)
- R_Recovery: "Wear mask. Step to door." (6 words cap)
