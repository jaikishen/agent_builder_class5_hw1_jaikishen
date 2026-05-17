HW 1 TASKS
-----------
TASK 1

After adding the third tool I asked a comparison question - "Which is taller, Falcon 9 or Starship? Compare their heights." and noticed the agent did use the third tool.

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon 9'}
  observation: {"first_flight": "2010-06-04", "height_m": 70, "diameter_m": 3.7, "mass_kg": 549054, "thrust_kn": 7607, "payload_to_leo_kg": 22800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Workhorse rocket. First s...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 2: action ---
  tool: compare
  args: {'a': 70, 'b': 120, 'label': 'height_m'}
  observation: height_m: a=70.0, b=120.0

--- step 3: final answer ---
Starship is taller than Falcon 9, with a height of 120 meters compared to Falcon 9's 70 meters.

TASK 2
------
Added a random number generator tool. And asked agent the question "Compare Falcon Heavy and Starship. Which has higher thrust, and how many successful missions has each flown?". The fourth tool was not called unnecessarily. 


--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon Heavy'}
  observation: {"first_flight": "2018-02-06", "height_m": 70, "diameter_m": 12.2, "mass_kg": 1420788, "thrust_kn": 22819, "payload_to_leo_kg": 63800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Heavy-lift variant wit...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 1: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Falcon Heavy' AND success = 1;"}
  observation: [{"n": 2}]

--- step 1: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Starship' AND success = 1;"}
  observation: [{"n": 2}]

--- step 2: action ---
  tool: compare
  args: {'a': 22819, 'b': 74000, 'label': 'thrust_kn'}
...
  observation: [{"n": 2}]

--- step 3: final answer ---
The Starship has a higher thrust of 74,000 kN compared to the Falcon Heavy's 22,819 kN. Both the Falcon Heavy and Starship have successfully completed 2 missions each.



TASK 3
------
Modified vehicles specification json document and added a new key crew_capacity. Asked the agent "Which of our rockets can carry the most crew, and how many people?" which requires the key. The agent pulled it out correctly.

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Crew Dragon'}
  observation: UNKNOWN VEHICLE: 'Crew Dragon'. Allowed: ['Falcon 1', 'Falcon 9', 'Falcon Heavy', 'Starship']

--- step 2: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon 9'}
  observation: {"first_flight": "2010-06-04", "height_m": 70, "diameter_m": 3.7, "mass_kg": 549054, "thrust_kn": 7607, "payload_to_leo_kg": 22800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Workhorse rocket. First s...

--- step 2: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon Heavy'}
  observation: {"first_flight": "2018-02-06", "height_m": 70, "diameter_m": 12.2, "mass_kg": 1420788, "thrust_kn": 22819, "payload_to_leo_kg": 63800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Heavy-lift variant wit...

--- step 2: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 3: final answer ---
The SpaceX rocket that can carry the most crew is the Starship, which is designed to accommodate up to 100 people. It is a fully reusable super-heavy rocket intended for missions to Mars and beyond.

TASK 4
------
# Increased temperature of model to 0.7. Ran the same question thrice to observe. Observed that tools were called in same order. Traces were almost the same except final answer was a bit more wordy.

========== run 1 (temperature=0.7) ==========
USER: Which is taller, Falcon 9 or Starship? Compare their heights.

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon 9'}
  observation: {"first_flight": "2010-06-04", "height_m": 70, "diameter_m": 3.7, "mass_kg": 549054, "thrust_kn": 7607, "payload_to_leo_kg": 22800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Workhorse rocket. First s...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 2: action ---
  tool: compare
  args: {'a': 70, 'b': 120, 'label': 'height_m'}
  observation: height_m: a=70.0, b=120.0

--- step 3: final answer ---
Starship, at 120 meters tall, is significantly taller than Falcon 9, which stands at 70 meters.

========== run 2 (temperature=0.7) ==========
USER: Which is taller, Falcon 9 or Starship? Compare their heights.

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon 9'}
  observation: {"first_flight": "2010-06-04", "height_m": 70, "diameter_m": 3.7, "mass_kg": 549054, "thrust_kn": 7607, "payload_to_leo_kg": 22800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Workhorse rocket. First s...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 2: action ---
  tool: compare
  args: {'a': 70, 'b': 120, 'label': 'height_m'}
  observation: height_m: a=70.0, b=120.0

--- step 3: final answer ---
Starship is taller than Falcon 9, measuring 120 meters compared to Falcon 9's height of 70 meters.

========== run 3 (temperature=0.7) ==========
USER: Which is taller, Falcon 9 or Starship? Compare their heights.

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon 9'}
  observation: {"first_flight": "2010-06-04", "height_m": 70, "diameter_m": 3.7, "mass_kg": 549054, "thrust_kn": 7607, "payload_to_leo_kg": 22800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Workhorse rocket. First s...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 2: action ---
  tool: compare
  args: {'a': 70, 'b': 120, 'label': 'height_m'}
  observation: height_m: a=70.0, b=120.0

--- step 3: final answer ---
Starship is taller than Falcon 9, with a height of 120 meters compared to Falcon 9's height of 70 meters.

TASK 5
------
Got permission denied error when I changed my model. Updated permissions in open ai platform to enable gpt-3.5-turbo.
Both models gave the same answer however, the order in which the tools were called differ.


gpt-4o-mini
-----------
USER: Compare Falcon Heavy and Starship. Which has higher thrust, and how many successful missions has each flown?

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon Heavy'}
  observation: {"first_flight": "2018-02-06", "height_m": 70, "diameter_m": 12.2, "mass_kg": 1420788, "thrust_kn": 22819, "payload_to_leo_kg": 63800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Heavy-lift variant wit...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 1: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Falcon Heavy' AND success = 1;"}
  observation: [{"n": 2}]

--- step 1: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Starship' AND success = 1;"}
  observation: [{"n": 2}]

--- step 2: action ---
  tool: compare
  args: {'a': 22819, 'b': 74000, 'label': 'thrust_kn'}
  observation: thrust_kn: a=22819.0, b=74000.0

--- step 2: action ---
  tool: compare
  args: {'a': 2, 'b': 2, 'label': 'successful missions'}
  observation: successful missions: a=2.0, b=2.0

--- step 3: final answer ---
The Starship has a higher thrust of 74,000 kN compared to Falcon Heavy's 22,819 kN. Both rockets have successfully completed 2 missions each.


gpt-3.5-turbo
-------------
USER: Compare Falcon Heavy and Starship. Which has higher thrust, and how many successful missions has each flown?

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Falcon Heavy'}
  observation: {"first_flight": "2018-02-06", "height_m": 70, "diameter_m": 12.2, "mass_kg": 1420788, "thrust_kn": 22819, "payload_to_leo_kg": 63800, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Heavy-lift variant wit...

--- step 1: action ---
  tool: vehicle_specs
  args: {'vehicle': 'Starship'}
  observation: {"first_flight": "2021-03-03", "height_m": 120, "diameter_m": 9, "mass_kg": 5000000, "thrust_kn": 74000, "payload_to_leo_kg": 250000, "stages": 2, "reusable": true, "active": true, "manufacturer": "SpaceX", "notes": "Fully reusable super-he...

--- step 2: action ---
  tool: compare
  args: {'a': 22819, 'b': 74000, 'label': 'thrust_kn'}
  observation: thrust_kn: a=22819.0, b=74000.0

--- step 3: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Falcon Heavy' AND success = 1"}
  observation: [{"n": 2}]

--- step 3: action ---
  tool: query_launches
  args: {'sql': "SELECT COUNT(*) AS n FROM launches WHERE vehicle = 'Starship' AND success = 1"}
  observation: [{"n": 2}]

--- step 4: final answer ---
The Starship rocket has a higher thrust of 74,000 kN compared to Falcon Heavy's 22,819 kN. Both Falcon Heavy and Starship have flown 2 successful missions each.



TASK 6
------
Each step appends 1 AIMessage plus one ToolMessage per tool call. The LLM re-reads the entire growing list every step.