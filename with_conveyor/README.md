## Update: Conveyor System Integration (v1.1)

This update enhances the raw material transport stage of the manufacturing 
cell digital twin by replacing the abstract Transporter delay with a 
physics-based **SimEvents Conveyor System** block.

### What changed
- Added a **Conveyor System** block downstream of the Transporter in each 
  raw material line (RM1/RM2/RM3), modeling entity movement based on real 
  belt length and speed rather than a fixed abstract delay.
- Configured conveyor parameters:
  - **Length:** 10 units
  - **Speed:** 2 units/time
  - **Entity length:** 1 unit (belt capacity ≈ 10 entities)
  - **Blocked output behavior:** Pause — the conveyor halts movement when 
    the downstream station is blocked, then resumes once capacity frees up, 
    simulating realistic conveyor jams/back-pressure.
- Enabled **live occupancy tracking** ("Number of entities in block, n") 
  wired to a Scope, allowing visual monitoring of belt congestion over the 
  simulation run.

### Why
The previous model used a single-value Transporter delay, which didn't 
capture physical belt constraints like finite capacity, transit time based 
on distance/speed, or blocking behavior when downstream stations are busy. 
The Conveyor System block adds this realism, making the model better 
reflect actual material-handling dynamics and bottleneck formation — a key 
requirement for a functional digital twin.

### Next steps
- Extend the conveyor upgrade to all three raw material lines
- Add fault/jam events for further realism
- Log and visualize occupancy data (Scope) across the full 1000-unit 
  simulation run to identify congestion patterns