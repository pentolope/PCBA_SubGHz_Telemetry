# PCBA_SubGHz_Telemetry — Sub-GHz Telemetry Radio

**Benchmark ID:** 23  
**Difficulty:** 4/5  
**Brief detail:** 2/5  
**Category:** rf-radio  
**Likely layer count:** 4  
**Primary stressors:** RF matching, PA current pulses, antenna connector, mixed RF/digital

## Design brief

Design a sub-GHz telemetry node for the 902–928 MHz ISM band using a modern packet radio transceiver and an MCU. Target materially longer range than a bare low-power radio by including an appropriate front-end or PA/LNA solution if justified. Provide USB-C, a battery input, and an SMA antenna connector. Follow vendor RF reference layouts and document the matching/filter network and power-current assumptions.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
