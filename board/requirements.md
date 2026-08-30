# Requirements — Sub-GHz Telemetry Radio

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `ee4315d0ed7f1c528618d4ce7ee9c4663cab2e846e038f775629c1eee1abfd79`.

## Fixed by the brief

### REQ-01 — The board is a sub-GHz telemetry node operating in the 902–928 MHz ISM band.

Brief text:

> Design a sub-GHz telemetry node for the 902–928 MHz ISM band

### REQ-02 — The radio must be a modern packet radio transceiver (device class fixed; specific part not).

Brief text:

> ISM band using a modern packet radio transceiver and an MCU.

### REQ-03 — The board must carry an MCU alongside the transceiver.

Brief text:

> using a modern packet radio transceiver and an MCU. Target materially longer range

### REQ-04 — The design must target materially longer range than a bare low-power radio would achieve.

Brief text:

> Target materially longer range than a bare low-power radio

### REQ-05 — The brief names an appropriate front-end or PA/LNA solution as the means it contemplates for reaching that range, with inclusion conditional on being justified; it neither mandates a front end nor rules out other ways of gaining range.

Brief text:

> by including an appropriate front-end or PA/LNA solution if justified.

### REQ-06 — Provide a USB-C connector.

Brief text:

> Provide USB-C, a battery input, and an SMA antenna connector.

### REQ-07 — Provide a battery input.

Brief text:

> Provide USB-C, a battery input, and an SMA antenna connector.

### REQ-08 — Provide an SMA antenna connector as the antenna interface (SMA, not a reverse-polarity or other family).

Brief text:

> Provide USB-C, a battery input, and an SMA antenna connector.

### REQ-09 — The RF layout must follow vendor RF reference layouts.

Brief text:

> Follow vendor RF reference layouts and document the matching/filter network

### REQ-10 — The matching/filter network must be documented as a deliverable, not merely drawn.

Brief text:

> document the matching/filter network and power-current assumptions.

### REQ-11 — The power-current assumptions must be documented as a deliverable.

Brief text:

> Follow vendor RF reference layouts and document the matching/filter network and power-current assumptions.

### REQ-12 — Where the brief is open, the design agent must make and document reasonable engineering decisions instead of inventing hidden user requirements.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-13 — The repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

### REQ-14 — Requirements the brief does state are authoritative: they may not be loosened, reopened as choices, or traded away in the course of making the open decisions.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open

## Open — the design agent decides

### OPEN-01 — Which packet radio transceiver to use — vendor, part, modulation scheme (FSK/LoRa-class/other), interface, and package.

The brief specifies only "a modern packet radio transceiver" and names no device, vendor, or modulation family.

*Decision:* **not yet made.**

### OPEN-02 — Which MCU to use — architecture, memory, peripheral set, package, and whether radio and MCU are separate devices or a combined SoC/module.

The brief says only "an MCU" and does not constrain family, performance, or integration level.

*Decision:* **not yet made.**

### OPEN-03 — Whether to fit a front end at all, and if so which topology: an integrated front-end module versus discrete PA, LNA and antenna switch.

The brief makes the front-end/PA/LNA conditional — "if justified" — so both inclusion and topology are the agent's call to argue.

*Decision:* **not yet made.**

### OPEN-04 — How "materially longer range" is quantified: target TX power, receive sensitivity, link budget, assumed antenna gain and path model, and what evidence closes the claim.

The brief gives a comparative goal with no distance, dBm, or dB figure attached.

*Decision:* **not yet made.**

### OPEN-05 — Matching network topology and component values, plus harmonic/band filtering choice (discrete LC, SAW, integrated filter).

The brief requires the network be documented but fixes no topology, impedance, or values.

*Decision:* **not yet made.**

### OPEN-06 — Antenna path arrangement: shared TX/RX path versus separate paths, switch selection, and bias/control sequencing from the MCU.

The brief names only the SMA connector at the end of the chain and is silent on the path behind it.

*Decision:* **not yet made.**

### OPEN-07 — Battery input specifics — chemistry, cell count, voltage range, how the input physically terminates, and whether charging, protection, or fuel gauging are on this board.

The brief asks for "a battery input" and states no chemistry, voltage, termination, or charging behaviour.

*Decision:* **not yet made.**

### OPEN-08 — Power architecture: rail voltages, regulator topology (LDO versus switching) per rail, and how the supply holds up under transmit current pulses.

The brief requires power-current assumptions to be documented but states no rails, currents, or regulator approach.

*Decision:* **not yet made.**

### OPEN-09 — Whether USB-C supplies board power at all and, if it does, how it and the battery are arbitrated — ORing, priority, hot-swap behaviour, and inrush handling.

The brief requires a battery input and a USB-C connector but never says USB-C powers the board, so both the existence of a second supply and any arbitration between the two are unstated.

*Decision:* **not yet made.**

### OPEN-10 — USB-C role and configuration: whether it carries data, supplies power, or both; CC termination and current advertisement; and whether USB reaches the MCU directly or through a bridge.

The brief names the connector but assigns it no function.

*Decision:* **not yet made.**

### OPEN-11 — SMA connector gender and mounting — jack versus plug, edge-launch versus through-hole versus vertical, and mechanical retention against mating torque.

The brief fixes the connector as "an SMA antenna connector" but states no gender, orientation, or mechanical constraint; the connector type itself is not open.

*Decision:* **not yet made.**

### OPEN-12 — Board outline, dimensions, mounting holes, enclosure interface, and connector edge placement.

The brief states no mechanical envelope, size, or mounting scheme at all.

*Decision:* **not yet made.**

### OPEN-13 — Layer count and stackup detail beyond the metadata's likely 4 layers: dielectric material and thickness, copper weights, layer ordering, and the controlled-impedance target for the RF trace.

Layer count is benchmark metadata guidance stated as "likely" rather than a brief-stated constraint, and no impedance or material is specified anywhere.

*Decision:* **not yet made.**

### OPEN-14 — RF/digital partitioning strategy: placement zoning, ground pour and stitching scheme, return-path management, and whether a shield can is used.

The brief mandates following vendor reference layouts but does not say how the digital side is separated from the RF side on this particular board.

*Decision:* **not yet made.**

### OPEN-15 — Protection strategy for the antenna port, USB-C, and the battery input — ESD, reverse polarity, overcurrent — and the capacitance budget any RF-path protection consumes.

The brief imposes no protection requirement; nothing in it names ESD, surge, or fault handling.

*Decision:* **not yet made.**

### OPEN-16 — Regulatory posture for the 902–928 MHz band: which rule set and limits the design targets, duty-cycle and spurious-emission strategy, and whether certification is in scope.

The brief names the band only; it states no regulatory regime, power limit, or certification goal.

*Decision:* **not yet made.**

### OPEN-17 — What the node actually telemeters — onboard sensors, expansion I/O, or external interfaces — and the electrical form of those interfaces.

"Telemetry node" describes the role, but the brief lists no sensor, payload interface, or I/O count.

*Decision:* **not yet made.**

### OPEN-18 — Reference clock selection: crystal versus TCXO, frequency, load capacitance, and the accuracy the chosen modulation demands.

The brief is silent on timing, and accuracy requirements follow from the transceiver choice, which is itself open.

*Decision:* **not yet made.**

### OPEN-19 — Programming, debug, and test provisions — SWD/JTAG or other access, RF test point or coupling for bring-up, and any production-test access.

The brief lists no debug or test interface among the things it requires be provided.

*Decision:* **not yet made.**

### OPEN-20 — Indicators and user controls (LEDs, buttons, reset) and any local status/UI behaviour.

The brief mentions no human interface elements.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Range claims are the softest spot: "materially longer range" invites a stated distance with nothing behind it. Any range figure must fall out of a link budget assembled from datasheet TX power, front-end gain, path loss and RX sensitivity, with the antenna and environment assumptions written down.
- Matching network values are easy to invent. Every L and C should trace to the vendor reference design, to the transceiver's stated port impedance, or to a simulation whose inputs are recorded — not to plausible-looking round numbers.
- "Follows the vendor RF reference layout" is a claim that must name the reference design and revision. A layout that resembles a reference without citing it, or that silently diverges from it, is unsubstantiated.
- PA current pulses invite generic decoupling boilerplate. The brief demands documented power-current assumptions, so peak transmit current, tolerable rail droop, and the decoupling that meets it need to be computed for the chosen parts, not asserted.
- Stackup is metadata, not brief: layer count 4 is offered as "likely", so treating it as a hard requirement or silently deviating from it both misrepresent the source. Controlled-impedance RF routing likewise cannot be claimed without the fabricator's dielectric and thickness data plus an actual trace-geometry calculation; a stated width with no stackup behind it is fabrication.
- The brief is detail 2/5 — the temptation is to fill the vacuum with invented user requirements: an enclosure size, a battery chemistry, a certification target, a sensor payload, an environmental rating, or a power role for USB-C that the brief never assigns. None of those are stated; each is a design decision that must be labelled as such.
- The opposite error is loosening what the brief does fix. "An SMA antenna connector" means SMA, not RP-SMA or a substitute family; stated requirements are authoritative and are not to be reopened as design choices while filling the gaps.
- Protection parts placed on the antenna path can quietly wreck the match; adding a TVS to the RF line without accounting for its capacitance at 900 MHz is a common unforced error, and the brief never asked for one.
