# Architecture — Sub-GHz Telemetry Radio

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- RF matching
- PA current pulses
- antenna connector
- mixed RF/digital

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Radio device and band plan

- Which packet radio transceiver is selected, and what evidence from its datasheet shows it covers 902–928 MHz with the intended modulation?
- Is the radio a discrete transceiver, a pre-certified module, or an MCU+radio SoC, and what does that choice cost or save in RF layout risk?
- What channel plan, data rate, and packet structure does the design assume, and which of those are the transceiver's constraints rather than assumptions?
- What is the datasheet-stated RF port impedance and does the part require a single-ended or differential match?
- What reference clock accuracy does the chosen modulation demand, and does a crystal meet it or is a TCXO required?

## Front end: whether to add PA/LNA, and how much

- Does the bare transceiver already reach the range goal, or is a front end genuinely needed — what calculation decides this?
- If a front end is used, is it an integrated FEM or discrete PA/LNA/switch, and what drove that split?
- What TX output power does the front end deliver at the connector after matching and filter loss, and from which datasheet curve?
- What receive noise figure and gain does the LNA path contribute, and how is LNA saturation on close-range links avoided?
- What bias, enable, and TX/RX timing signals must the MCU generate, and do they meet the front end's switching timing?
- What is the front end's thermal dissipation during transmit, and does the board area and copper support it?

## Matching, filtering and the antenna path

- What is the complete chain from transceiver pin to SMA centre pin, component by component?
- How were the matching component values derived — from the vendor reference design, from a datasheet-stated impedance, or from simulation — and which source is cited for each?
- What harmonic and out-of-band filtering is present, and what attenuation does it provide at the harmonics of 902–928 MHz?
- What insertion loss does the total match-plus-filter path add, and how is that carried into the link budget?
- What component tolerance, Q, and self-resonance assumptions underlie the match, and how sensitive is return loss to them?
- How will the match be verified in hardware, and does the layout provide the access to do so?

## RF layout, stackup and RF/digital partitioning

- Which vendor reference layout is being followed, by name and revision, and where does this board deviate from it and why?
- What layer count and stackup does the board adopt — dielectric, thickness, copper weights — given that the metadata calls 4 layers likely rather than required, and what trace geometry does that choice imply for the controlled-impedance RF trace?
- Where is the boundary between the RF section and the digital/power sections, and what physically enforces it?
- How is the RF ground return kept continuous under the transmission line, and where are the stitching vias?
- Which digital signals, clocks, and switching regulator nodes run near the RF section, and what keeps their harmonics out of the receive band?
- Is a shield can or keepout area required, and what does that add to the mechanical envelope?

## Power architecture and transmit current pulses

- What are the peak and average supply currents during transmit, and from which datasheet numbers for the chosen radio and front end?
- What supply droop is tolerable at the PA and transceiver pins, and what bulk plus local decoupling is needed to hold it?
- What rail voltages are required, and what regulator topology feeds each — what argument decides LDO versus switching for the RF-adjacent rails?
- If a switching regulator supplies any RF-adjacent rail, where does its switching frequency and its harmonics land relative to the receive band?
- What is the current path from the selected supply, through whatever regulation is chosen, to the transmit stage, and does its impedance support the pulse without ringing on the rail?
- What are the documented power-current assumptions the brief requires, stated as a table with sources?

## USB-C, battery input and source management

- Is USB-C used for data, for power, or both, and what CC configuration and current advertisement follow from that?
- What battery chemistry and voltage range does the input accept, and what happens at the low and high ends of it?
- Is charging performed on this board, and if so under what current and thermal limits?
- If USB-C is given a power role, how are USB and battery arbitrated — priority, ORing, hot-swap — and what happens if both are present during a transmit pulse?
- What protection does each power input carry against reverse polarity, overcurrent, and inrush?
- How does the battery input physically terminate — connector, terminal, or solder pads — and how is it secured and keyed?

## Antenna connector and mechanical interface

- The brief fixes the connector as SMA — which gender and body style is chosen, and what evidence supports it mating with the intended antenna?
- How is the connector launch designed so the transmission line's impedance is maintained through the transition?
- How does the connector resist the torque and side load of repeated antenna mating, and does the footprint alone carry that load?
- Where on the board outline does the connector sit, and what does that fix about the board's shape and mounting?
- What are the board dimensions, mounting holes, and enclosure assumptions that follow from the connector and battery placement?

## MCU, control and telemetry payload

- Which MCU is chosen, and what peripheral, memory, and timing capabilities does the radio interface require of it?
- What is the telemetry payload — onboard sensors, an expansion header, or external I/O — and what does the brief actually oblige here versus what is a design choice?
- What bus connects MCU to transceiver and front end, and does its speed and length work across the RF/digital boundary?
- What programming and debug access is provided, and how is it isolated during RF operation?
- What is the MCU's sleep and duty-cycle behaviour, and how does it shape the average current figure in the power budget?

## Protection, robustness and interference

- What ESD exposure do the SMA port, USB-C, and battery input actually see in this node's use, and what protection follows?
- If protection is placed on the RF path, what capacitance does it add and what does that do to return loss at 928 MHz?
- How is the receiver protected from nearby transmitters, and does the front end need additional selectivity?
- What happens to the transmit stage and its supply if the antenna is disconnected or shorted during transmit?

## Regulatory and emissions posture

- Which regulatory rule set for the 902–928 MHz band is the design written against, and is that a brief requirement or a design assumption?
- What conducted output power and spurious emission levels does the design predict at the connector, and against what limits?
- Does the chosen modulation and channel behaviour satisfy the rules the design targets, and what evidence shows it?
- Is pre-certified module use or full certification the intended path, and what does that impose on layout and antenna choice?

## Manufacturability, test and bring-up

- What fabricator and process class is assumed, and does the RF trace geometry and stackup fall inside its published capability?
- Is assembly single- or double-sided, and does the SMA connector or the battery termination force a hand-assembly step?
- What test points allow the match, the rails, and the transmit current pulse to be measured without cutting the board?
- What is the bring-up sequence, and what measurement at each step confirms the RF chain before transmit power is enabled?
- Which claims in this document remain assumptions until hardware measurement, and how are they flagged as such?

## Answers still owed

All of them. See [status.md](status.md).
