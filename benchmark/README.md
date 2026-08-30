# Benchmark entry — board 23 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_SubGHz_Telemetry` |
| Board id | `subghz_telemetry` |
| Category | rf-radio |
| Difficulty | 4 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | RF matching, PA current pulses, antenna connector, mixed RF/digital |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

A difficulty-4 mixed RF/digital board whose brief supplies only a band, a device class and a short list of things to provide, so the agent must derive an entire RF architecture without being handed one. It targets the four stressors the metadata lists — RF matching, PA current pulses, the antenna connector, and mixed RF/digital — on a stackup the metadata calls a likely 4 layers but never fixes. It also makes evidence a deliverable in its own right: the matching/filter network and the power-current assumptions must be documented, and vendor RF reference layouts must be followed. The interesting failure mode is a plausible-looking radio whose match, range claim and current budget cannot be traced to any datasheet.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
