# Sub-GHz Telemetry Radio

A 902–928 MHz ISM sub-GHz telemetry node built on a packet radio transceiver plus an MCU, with USB-C, a battery input and an SMA antenna connector.

This repository holds a sub-GHz telemetry node for the 902–928 MHz ISM band, built around a packet radio transceiver and an MCU, with USB-C, a battery input and an SMA antenna connector. The brief asks for materially longer range than a bare low-power radio, naming an added front-end or PA/LNA solution as the means it contemplates and leaving its inclusion conditional on justification, and it requires the RF layout to follow vendor reference layouts with the matching/filter network and power-current assumptions documented.

Beyond those points the brief is deliberately thin (detail 2/5). No transceiver, MCU, front-end, regulator, connector variant or antenna is named; no output power, sensitivity, range figure, board outline, battery chemistry, rail voltage or impedance target is stated; the brief never says what function USB-C serves, so whether it supplies board power is itself an open choice; and the telemetry payload interfaces are unspecified. Layer count 4 comes from benchmark metadata as a "likely" figure, not from the brief prose. The brief's own instruction is to treat stated requirements as authoritative and, where it leaves choices open, to make and document reasonable engineering decisions rather than invent hidden user requirements. Selecting parts, fixing the RF topology and defining the mechanical and power architecture are therefore the design agent's work, and every such choice belongs in `docs/architecture.md` with its evidence rather than being treated as a pre-existing user requirement.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 14 requirements and deliberately leaves
20 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Category | rf-radio | metadata |
| Difficulty / brief detail | Difficulty 4/5, brief detail 2/5 (most architecture left open) | metadata |
| Likely layer count | 4 | metadata |
| Primary stressors | RF matching, PA current pulses, antenna connector, mixed RF/digital | metadata |
| Operating band | 902–928 MHz ISM band | brief |
| Radio | A modern packet radio transceiver — no device, vendor or modulation family named | brief |
| Digital controller | An MCU — no architecture, family, package or vendor named | brief |
| Range goal | Materially longer range than a bare low-power radio (no distance or dB figure given) | brief |
| RF front end | An appropriate front-end or PA/LNA solution, included if the design justifies it | brief |
| Antenna interface | An SMA antenna connector (gender and mounting style unspecified) | brief |
| Wired interface | USB-C must be provided; the brief assigns it no function, so data, power, both, and any negotiation are unspecified | brief |
| Power sources | A battery input is required (chemistry, voltage range, charging not stated); the brief gives USB-C no power role, so any second supply path is a design choice | brief |
| RF layout method | Follow vendor RF reference layouts | brief |
| Required documentation | The matching/filter network and the power-current assumptions must be written up | brief |
| Decision discipline | Stated requirements are authoritative; open choices are the agent's to make and document, not to fill with invented user requirements | brief |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 23 of 32 |
| Category | rf-radio |
| Difficulty | 4 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | RF matching, PA current pulses, antenna connector, mixed RF/digital |

A difficulty-4 mixed RF/digital board whose brief supplies only a band, a device class and a short list of things to provide, so the agent must derive an entire RF architecture without being handed one. It targets the four stressors the metadata lists — RF matching, PA current pulses, the antenna connector, and mixed RF/digital — on a stackup the metadata calls a likely 4 layers but never fixes. It also makes evidence a deliverable in its own right: the matching/filter network and the power-current assumptions must be documented, and vendor RF reference layouts must be followed. The interesting failure mode is a plausible-looking radio whose match, range claim and current budget cannot be traced to any datasheet.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the accountability-review skill [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_SubGHz_Telemetry.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `ee4315d0ed7f1c528618d4ce7ee9c4663cab2e846e038f775629c1eee1abfd79`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
