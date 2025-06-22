# Power Systems

## Core Insight
The heartbeat of spacecraft - converting sunlight, nuclear decay, or stored chemistry into the electricity that runs everything, with no grid to plug into and no room for outages.

Power in space is existential. Run out, and your spacecraft becomes a tumbling tomb. Generate too much, and thermal control suffers. Every watt is precious, every efficiency gain celebrated, every redundancy necessary.

Power generation options reveal mission priorities:
- **Solar panels**: Free energy, but need sunlight
- **RTGs**: Radioisotope decay, constant but declining
- **Fuel cells**: High power density, limited duration
- **Batteries**: Energy storage, cycle life limits
- **Nuclear reactors**: Massive power, massive politics

Solar panel realities:
- 30% efficient silicon (at best)
- Degradation from radiation damage
- Temperature affects efficiency
- Dust accumulation (Mars problem)
- Distance from sun: 1/r² is cruel
- Articulation adds complexity

Battery challenges:
- Lithium-ion: High energy, careful management
- Charge/discharge cycles limited
- Temperature sensitivity extreme
- Depth of discharge affects lifetime
- Safety concerns (thermal runaway)

Power distribution complexities:
- Voltage regulation across loads
- Fault protection without breakers
- EMI from switching supplies
- Grounding in floating spacecraft
- Redundancy without weight penalty

The power budget dominates design:
- Peak power sizing arrays/batteries
- Average power sizing thermal
- Contingency power for failures
- End-of-life power after degradation
- Emergency power for survival

Mission examples:
- ISS: Football field of panels, 120kW
- Voyager: RTG still working after 45 years
- Mars rovers: Dust storms can kill
- CubeSats: Body-mounted cells, watts precious
- James Webb: Single solar array, always pointed

In space, power is life. Every subsystem begs for watts. Every efficiency improvement enables new capability. Every failure mode threatens darkness.

## Connections
→ [[solar_arrays]] (primary generation)
→ [[batteries]] (energy storage)
→ [[power_distribution]] (getting power around)
→ [[RTG]] (nuclear option)
→ [[power_budget]] (the accounting)
← [[spacecraft_design]] (power drives size)
← [[thermal_control]] (power generates heat)
← [[mission_operations]] (power management)

---
Level: L2
Date: 2025-06-21
Tags: #component #power #critical