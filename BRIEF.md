# PCBA_SubGHz_Telemetry — Sub-GHz Telemetry Radio
## Design brief

Design a sub-GHz telemetry node for the 902–928 MHz ISM band using a modern packet radio transceiver and an MCU. Target materially longer range than a bare low-power radio by including an appropriate front-end or PA/LNA solution if justified. Provide USB-C, a battery input, and an SMA antenna connector. Follow vendor RF reference layouts and document the matching/filter network and power-current assumptions.

## Functional requirements

- Channel, data rate and output power shall be firmware-settable at run time across 902–928 MHz.
- The board shall run from USB-C alone and from the battery alone, switching over unattended.
- A documented link budget at the SMA plane shall substantiate the range gain over the bare transceiver.

## RF chain and antenna interface

- The transceiver-to-SMA path shall be a 50 Ω controlled-impedance structure, with its geometry recorded.
- Harmonics and spurs shall be filtered on the board, with margin against the target regime's limits.
- The matching and filter network shall be documented — topology, values, target impedances, tuning method — and tunable by substitution.
- A fitted PA/LNA shall be switched so the LNA never sees transmit power.
- The frequency reference shall meet the accuracy the channel plan and data rate demand.

## Power and rails

- Rails shall be derived from USB-C VBUS at 5 V nominal and from the battery over its full declared range, holding regulation through transmit turn-on and peak transmit current.
- Converters shall not desensitise the receiver; sensitivity with them active and loaded shall be reported.
- A current budget for sleep, receive, full-power transmit and USB operation shall be documented, with duty cycle and battery life.

## Connectors, layout and placement

- The antenna port shall be an SMA connector whose launch and ground return follow vendor guidance, with clearance to mate a cable.
- The USB-C receptacle shall present sink CC terminations; the battery input shall be non-reversible and its polarity marked.
- Transceiver, matching network, front end and launch shall reproduce the vendor reference layout as closely as the board allows; departures shall be recorded.
- RF routing shall sit over an uninterrupted adjacent reference plane, and other return currents shall not cross the RF ground region.

## Protection, test and bring-up

- USB-C pins and the exposed SMA centre conductor shall be ESD protected to a stated level without degrading the signals they sit on.
- The battery input shall survive reverse connection and shall not be back-driven from VBUS unless charging is deliberate.
- Rail test points, transceiver and front-end current measurement, and MCU debug access shall work on the assembled board from either supply.
- Firmware shall command continuous carrier, modulated transmit and continuous receive, so power, spectrum and sensitivity are measurable at the SMA port.

## Open choices

- MCU and packet radio transceiver, constrained to parts with a published vendor RF reference layout.
- Whether a PA/LNA or front-end is fitted, decided by whether the link budget justifies its current and cost.
- Battery chemistry, cell count, connector and declared voltage range, and whether the pack charges from VBUS.
- Whether USB-C carries data as well as power, and the regulatory regime and channel plan that fix the emission limits.
