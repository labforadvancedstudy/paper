# Specific Impulse

## Core Insight
The fuel economy rating for rockets - how many seconds of thrust you get per unit of propellant weight, measuring the efficiency of turning mass into momentum.

Specific impulse (ISP, Isp) is deceptively simple: thrust divided by propellant weight flow rate. But this number determines everything about mission possibility. High ISP means less propellant for same delta-v. Low ISP means brute force and diminishing returns.

The numbers tell stories:
- Solid rockets: 250-280s (simple but wasteful)
- Kerolox: 300-350s (the reliable middle)
- Hydrolox: 450s (performance king of chemicals)
- Ion drives: 3000-10,000s (patience required)
- Nuclear thermal: 900s (if politics allowed)
- Photon rockets: 30,000,000s (theoretical limit)

Why seconds? Historical accident that stuck. It's really exhaust velocity divided by Earth gravity. But seconds is universal - works in metric and imperial.

The fundamental trade-off:
- High ISP engines have low thrust
- High thrust engines have low ISP
- Chemical rockets can't break ~500s
- Electric can reach 10,000s at millinewtons
- No free lunch in physics

ISP determines mission architecture:
- Launch needs high thrust (low ISP acceptable)
- Deep space needs high ISP (low thrust acceptable)
- Hybrid solutions emerging (chemical + electric)

The rocket equation is merciless:
Δv = ISP × g × ln(initial mass/final mass)

Double your ISP, double your delta-v for same mass ratio. But doubling chemical ISP is impossible. We're near theoretical limits, fighting for single-digit improvements.

ISP is why Mars is hard and stars are impossible (with rockets).

## Connections
→ [[exhaust_velocity]] (ISP × g)
→ [[thrust]] (the other half)
→ [[propellant_choice]] (determines ISP)
→ [[engine_cycle]] (affects ISP)
→ [[nozzle_design]] (optimizes ISP)
← [[rocket_equation]] (ISP is key variable)
← [[mission_design]] (constrained by ISP)
← [[engine_selection]] (ISP vs thrust trade)

---
Level: L1
Date: 2025-06-21
Tags: #fundamental #efficiency #measure