minimise cross talk (capacitive coupling)
Elec field = vol / dist

PCB reliability:
heat
stay below datasheet
# Schematic Design
Prototyping rules:
- Don't emphasize shape or size requirements
- Add test points
- Add diagnostic LEDs (3.3V, 5V, Ready, Status, Error)
- Use 805 package passives (Caps., Resistors)
- Add additional space around components
- Keep decoupling caps close
- Add silkscreen text (Component names, resistor/cap values, diode direction, component placement hints, +-)
- Silkscreen text should 2mm tall
- Add Isolation jumpers
- Breakout unused GPIOs
- Be unambigous about UART TX/RX (Or add Poka-yoke to switch)
- Add isolation jumpers to configure I2C addresses
- ordered labeled SMD resistors
- Always check footprints (Check measurements of footprint in EDA and manufacturer)

## Rules
- Place the project name at the top of the schematic page
- Include descriptions for each block in the schematic.
- Organize blocks logically (e.g., Arduino headers on the right, microcontroller in the middle, USB connector connected directly to the microcontroller).
- **Symbol Pin Organization:** (2:55) Place power pins at the top of a symbol, ground pins at the bottom, input pins on the left, and output pins on the right.
- **Decoupling Capacitors:** (5:27) Use one 100nF decoupling capacitor per power pin of a chip, placed close to the pin on the PCB.
- **Bulk Capacitors:** (5:52) Place one larger capacitor (e.g., 10µF) somewhere close to the microcontroller.
- **Component Type Minimization:** (6:30) Keep the number of different component types on the board to a minimum (e.g., use the same 100nF capacitor type throughout).
- **Capacitor Voltage Rating:** (6:09) Ensure capacitor voltage ratings are appropriate for the circuit's voltage.
- **Ferite Bead Selection:** (8:00) Be careful when selecting ferrite bits; check the maximum current they can handle.
- **Vcap Connection:** (9:21) Connect the Vcap pin with a 4.7µF capacitor, placing it close to the pin with the shortest possible trace.
- **Net Naming:** (10:04) Name important nets (e.g., Vcap, crystal nets) for clarity during PCB layout.
- **Regulator Capacitor Type:** (11:31) Be careful about the specific type of output capacitor used with regulators, as some are very specific.
- **Heat Dissipation (Regulators):** (14:12) For chips that get hot (e.g., regulators), design the PCB to cool them down, ideally by connecting the large thermal pad to a ground plane with vias for better heat spreading.
- **Wire Crossing Conventions:** (15:21) Avoid using wire crossings that require a junction dot to indicate connection; prefer crossings where wires are clearly connected or not.
- **Component Size Selection:** (17:18) Be aware of the size of components used, smaller capacitors might be better for compact boards.
- **Schematic Information:** (17:58) Add text boxes to the schematic with important information like maximum input voltage and maximum current for components like regulators.
- **Linear Regulator Heat:** (18:57) Be very careful with linear regulators as they can get very hot if input voltage is too high or current drawn is too large.
- **Jumper Symbol in BOM:** (19:39) Create a specific symbol for a jumper to ensure it's included in the Bill of Material (BOM).
- **Header Orientation:** (20:05) When a header is used as a jumper, consider rotating it by 90 degrees.
- **Consistent Power Symbols:** (20:13) Once a power symbol is used in the schematic, consistently use it for all similar power connections.
- **Net Names for Local Power:** (20:32) Only use net names for very local power connections, as they may not connect across multiple schematic pages depending on software settings.
- **Global Power Symbols:** (21:11) Power symbols are global and typically connect across all pages by default.
- **Power Net Naming Convention:** (21:28) Use a plus sign and voltage value (e.g., +3.3V) for all power nets.
- **Power LED Placement:** (22:27) Place the power LED on the last power rail to switch on (e.g., 3.3V if both 5V and 3.3V are present) to confirm all previous power rails are working.
- **LED Resistor Value:** (22:50) Use a 1kOhm resistor as an initial value for standard LEDs and adjust later based on brightness.
- **LED Resistor Necessity:** (23:16) Always place a resistor in series with an LED to limit current.
- **Boot Pin Information:** (24:41) Place a text box near the boot pin explaining its function (e.g., when boot 0 is high or low).
- **Reset Pin Circuitry:** (25:50) Avoid directly shorting capacitors with buttons (e.g., in reset circuits); consider adding a resistor to limit current.
- **Switch/Button Pin Connection:** (27:19) Be extremely careful to connect the pins of switches/buttons correctly, as incorrect rotation can lead to short circuits.
- **Crystal Capacitors:** (28:20) Be very careful about the correct capacitor values for crystal oscillators as they are sensitive.
- **Crystal Application Notes:** (29:54) Refer to application notes for specific equations and guidance on calculating crystal capacitor values.
- **USB-C Connector Selection:** (31:18) When selecting a USB-C connector, prefer one with a single row of pins as it's easier to solder.
- **USB-C Power Delivery:** (31:40) Use pull-down resistors on the CC pin of a USB-C connector to deliver 5V.
- **ESD Protection (USB):** (31:51) Consider adding ESD protection to USB data lines.
- **Decoupling Capacitor for USB Power:** (32:51) Add at least a 100nF decoupling capacitor close to the power pin of the USB connector.
- **USB Net Naming:** (33:43) Name important USB nets (e.g., D+, D-) for clarity during PCB layout.
- **User LED Connection (Software Compatibility):** (35:06) Be aware that connecting a user LED to a different GPIO pin than a reference design may impact software compatibility.
- **User LED Control:** (35:17) Consider controlling the cathode side of an LED (connecting the anode to power and the cathode to the microcontroller pin) for better power driving and compatibility with open-drain outputs.
- **Header Pinout Design:** (37:40) When designing header pinouts, consider what happens if someone connects the header incorrectly (e.g., reverse connection) to prevent damage.
- **UART Pin Selection:** (39:51) If a specific feature (like reprogramming flash memory) relies on specific UART pins, ensure the header is connected to those pins.
# PCL Layout
## Rules
Spread tracks to avoid cross talk
Don’t change default EDA component designators
Horizontal/Vertical routing on different layers
Add net colors (GND and Power, I2C, SPI)
Calculate track width (based on max current for power, an for digital based on impedance and stack up)
Don’t share power vias except for power regulator circuits, keep it on the same layer (to prevent inductance) and route to ground pour via multiple vias together in the same spot

Add big copper area for heat dissipation + heat sinks to power components

Use 4 layer PCB boards
Add dedicated power layer, use stitching capacitors and stitching vias
Add thermal reliefs connections (for soldering purposes)
Add ESD
Control impedance
Dont route under components with Metal parts or Chassis
Stick to safe zones in manufacturer capabiilities
Keep oscilator track from reset track
Clock signals create a lot noise, dont route other signals close to clock tracks
Headers have J or CON designators
Add board padding around the circuitry
Clearances:
- distance between tracks (stick to manufacturer capabilities)


(From Gemini):
- **Arduino Compatibility** (2:14): For replacement boards, follow the exact shape, mounting hole positions, connectors, and pin-out of the original Arduino board.
- **Component Height** (4:49): Avoid using very tall components if not strictly necessary, as they can cause problems with additional boards or enclosures.
- **Board Size** (4:12): Aim to make the board as small and thin as possible to save costs and for practicality.
- **Text and Labels** (6:07):
    - Include information on how jumpers can be used directly on the PCB (6:07).
    - Align all text in only two directions (e.g., horizontal and vertical) to make it easy to read without excessive board rotation (7:03).
    - Use a readable text size; avoid very small text on large boards with ample space (7:46).
- **LED Placement** (8:06): Group LEDs together for a cleaner look, especially if an enclosure box is planned. Keep them slightly separated to prevent light bleeding (8:32).
- **Board Identification** (8:52): Always include the project name, board name, board version, and year of design on the PCB for identification and revision control.
- **Track Spacing (Cross-talk Prevention)** (10:16): Spread tracks as far apart as possible, especially when there's free space on the board, to minimize cross-talk and noise.
- **Reference Designators** (14:52): Never manually change reference designators in the PCB layout; any changes should be made in the schematic to ensure synchronization with the Bill of Materials (BOM) and pick-and-place files. Use text labels for custom component names instead.
- **Horizontal/Vertical Routing** (15:00): Route most signals on one layer (e.g., top) horizontally and most signals on another layer (e.g., bottom) vertically. This approach simplifies routing and minimizes vias.
- **Net Colors** (16:07): Assign colors to specific nets, especially ground, to easily identify pins that are simple to connect with a short track and a via, making the layout process easier.
- **Track Width Calculation** (18:10):
    - Calculate power track widths based on maximum current using online calculators (19:18).
    - Calculate digital signal track widths based on stackup and required impedance (usually 50 ohms) (19:41).
    - Use different track widths for power tracks and standard 50-ohm tracks to facilitate mass changes later (22:18).
- **PCB Layers** (24:09): For beginners, use at least a four-layer PCB instead of two-layer, as it's easier to maintain high-quality signals, and the price difference for small boards is minimal.
- **Via Dimensions** (25:22): Use appropriate via dimensions (e.g., 24/12 mil); smaller vias can increase PCB cost.
- **Component Placement** (26:10):
    - Place components in the PCB based on their proximity in the schematic (26:21).
    - Place components of critical circuits (e.g., regulators) very close to each other (27:04).
    - Place decoupling capacitors close to each power pin (27:22).
- **Vias for Power/Ground Pins** (27:55): Use at least one via per power or ground pin; avoid sharing vias between power pins, especially with large ground planes.
- **Regulator Connections** (30:47):
    - The connection between the output of a regulator and its output capacitor should be as good as possible, ideally on the same layer to minimize inductance (31:51).
    - Use multiple vias for power outputs, even if the current is not very high, as a good habit (32:50).
    - Ensure a large copper area (heat sink area) for regulators to dissipate heat effectively, especially if high input voltage and current are expected (33:33). If not possible, use multiple vias to spread heat to internal planes (34:51).
- **Stitching Capacitors and Vias (Advanced)** (35:40): For advanced designs, place stitching capacitors or stitching vias where signals change layers to control fields and return currents.
- **Through-hole Pins and Thermal Relief** (38:09):
    - Do not connect through-hole ground/power pins through additional vias if there's a solid ground/power plane inside the PCB (38:29).
    - Ensure thermal relief connections are appropriately sized; wider connections are often better for soldering (39:40).
- **USB Routing** (41:30):
    - USB signals (D+/D-) should be routed as 90-ohm differential pairs, with track width and spacing calculated based on PCB stackup and impedance (41:44).
    - Keep USB tracks as short as possible, especially if impedance cannot be controlled (42:50).
    - Place ESD protection components as close as possible to the connector, with direct connections (43:52).
    - Be cautious when routing under components with metal chassis, though solder mask provides some isolation (44:30).
- **Clearance** (45:37): Set appropriate clearance values (distances between objects), considering the PCB manufacturer's minimum capabilities. Avoid using values at the edge of their capabilities to prevent increased costs (47:00).
- **Critical Signals (Clocks)** (50:36):
    - Route critical signals like clocks with smoother, rounded corners rather than sharp 90-degree bends, primarily for aesthetic reasons, though electrically 90-degree bends are often fine for non-high-speed signals (52:37).
    - Keep other signals spaced further away from clock tracks to prevent noise pickup (53:50).
- **Aesthetics** (54:15): Strive to make the PCB layout look nice and organized, especially on visible layers like the bottom layer (54:15).
- **DRC Checks** (57:11): Always run Design Rule Check (DRC) for both schematic and PCB before sending the board to production, and ensure there are no errors (59:16).

## Questions
What is differential pairs in PCB Design and why is it relevant to USB D+ D-
What does transient response mean?