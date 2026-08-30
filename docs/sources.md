# Sources — Sub-GHz Telemetry Radio

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Sub-GHz transceiver datasheet | RF port impedance, TX power and RX sensitivity figures, supply current per state, reference clock requirements, and control interface timing — the numbers the whole link budget and current budget rest on. |
| Vendor RF reference design and reference layout package | The brief explicitly requires following vendor RF reference layouts, so the specific reference design, its revision, its matching topology and its stackup must be cited and any deviation justified. |
| Front-end module or discrete PA/LNA datasheet | Gain, output power, P1dB, noise figure, bias and TX/RX switching timing, and thermal resistance for the added front end the brief permits if justified. |
| MCU datasheet and reference manual | Peripheral capability against the radio interface, package pinout, supply rails, sleep and active current for the average-power figure. |
| Regulatory rules for the 902–928 MHz ISM band | The brief names the band, so emission limits, spurious requirements and channel/duty-cycle behaviour must be checked against a named rule set rather than assumed. |
| SMA connector datasheet and mechanical drawing | Footprint and launch geometry, frequency rating, gender and body style, and mating torque and retention for the mechanical interface. |
| Passive component datasheets and S-parameter models | Tolerance, Q, and self-resonant frequency of the matching and filter components, which determine whether the computed match survives real parts at 900 MHz. |
| PCB fabricator capability and stackup documentation | Dielectric constant and layer thicknesses for the impedance calculation, plus minimum trace and space limits for whatever layer count and stackup the design adopts — the metadata calls 4 layers likely, not required. |
| Regulator, charger and battery datasheets | Transient response and current capability against the transmit pulse, input voltage range, and — if charging is placed on this board — charge current and thermal limits for the battery input. |
| USB Type-C connector and configuration references | Connector footprint and mechanical retention plus CC termination and current advertisement for whatever role USB-C is given. |
| ESD and circuit-protection device datasheets | Clamping performance and, critically, junction capacitance where protection sits on the RF path or on USB data lines. |
| Simulation and measurement evidence generated for this board | Impedance and return-loss results, link-budget arithmetic, and rail-droop analysis — the documented matching network and power-current assumptions the brief requires as deliverables. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
