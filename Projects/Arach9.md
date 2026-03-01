---
image: Pasted image 20260118110024.png
status: Ongoing
---
![[Pasted image 20260118110024.png]]
![[Hexapod 2026-01-13 09.22.37.excalidraw]]


## Controller Board
The Hex9 controller board will be a PCB that contains all of the IMU sensors as well as the motor drivers. The power for the motors and the MCU will be routed separately on the board. I will be using the STM32F401RE Chip, it will need:
- a 3.3 V regulator: buck converter if powering from 7–24 V or have high total current, LDO if input is already near 3.3–5 V and current is modest
- decoupling capacitors: 0.1 µF at every VDD pin, 1–4.7 µF bulk near the MCU
- layout: solid ground plane, short & wide power traces, Keep switching regulator loops tight (if using buck)
- Motors inject noise; keep **motor power** and **logic power** well-separated with star returns and bulk capacitance near drivers.


You need your MCU to reliably boot every time.

**Minimum:**

- **NRST pin**:
    - Add an optional reset button to ground
    - Add a pull-up if needed (often internal is fine, but an external pull-up is common)

- **BOOT0 pin**:
    - Add a pull-down resistor (typ. ~10 kΩ) so it boots from Flash by default
    - Optionally add a jumper/test pad to pull BOOT0 high for ROM bootloader mode

This prevents the common “board boots into weird mode” issue.

---

### 3) Clocking: internal HSI vs external crystal

The F401 can run from internal oscillator (HSI) for many applications.

**Options:**

- **Use internal HSI (simpler)**:
    
    - Good enough for many control applications
        
    - Less BOM, easier routing
        
- **Add an external crystal (more accurate timing)**:
    
    - Recommended if you need:
        
        - Very accurate timebase
            
        - USB (not typical for F401RE usage, depends on part)
            
        - Higher precision comms (often still fine on HSI)
            

If you are doing lots of serial comms and timing-critical PWM, HSI is often acceptable. If you want maximum robustness, add an **8–16 MHz crystal** with proper load capacitors.

---

### 4) Programming and debugging (how you will flash it)

You should design for **SWD programming**. This is the standard, reliable method.

**Include on your PCB:**

- **SWDIO**
    
- **SWCLK**
    
- **GND**
    
- **3.3 V (VTref)**
    

Optionally:

- **NRST** (strongly recommended)
    
- **SWO** (optional, for trace/printf-style debugging)
    

**Connector choice:**

- Easiest: a **2×5 1.27 mm “ARM SWD” header** (Cortex debug header)
    
- Or a compact 4–6 pin header/test pads
    

**How to use the Nucleo as programmer**  
You can use the Nucleo’s onboard ST-LINK to program your custom board:

- Disconnect Nucleo’s MCU from ST-LINK (many Nucleos have jumpers/solder bridges)
    
- Wire ST-LINK SWD pins to your board’s SWD header
    

This is a very common workflow.

---

### 5) Bring-up and debugging aids (strongly recommended)

These cost almost nothing and save days:

- A **power LED** on 3.3 V
    
- A **user LED** on a GPIO
    
- A **UART header** (TX/RX/GND) for logging
    
- Test points for:
    
    - 3.3 V
        
    - GND
        
    - NRST
        
    - BOOT0
        
    - SWDIO/SWCLK
        

UART logging is especially helpful when you have 20 motors and lots of moving parts.

---

### 6) Protection and signal integrity considerations (important for your system)

Because you are controlling motors and reading encoders/IMU:

- Add **ESD protection** on external connectors
    
- Add **series resistors** (22–100 Ω) on fast digital lines leaving the board (optional but often helpful)
    
- Use proper **pull-ups** for I²C (to 3.3 V)
    
- Keep IMU away from high-current motor traces and magnets
    
- Plan your ground returns carefully
    

---

## Practical recommendation for your exact project

Given you are aiming at:

- Many motors
    
- Encoder feedback
    
- PWM expansion possibly via I²C devices
    
- A streamlined integrated controller
    

I recommend:

1. **Start firmware on Nucleo** to validate timing, comms, and control loops.
    
2. In parallel, design a custom board using the **STM32F401 MCU directly**.
    
3. On the custom board, include:
    
    - SWD connector (with NRST and VTref)
        
    - BOOT0 strap/jumper
        
    - UART header for logs
        
    - Clean 3.3 V power and proper decoupling
# Roadmap
- [ ] Remove callback pattern in uart parser (Make it private variable in main.c)
- [ ] Write code for PID Joint Position Control
- [ ] Clean up as5600.c
- [ ] Clean up tb6612fng.c
- [ ] Clean up main.c
- [ ] Add endstops to joint

Controller Circuit Diagram
![[Hexapod 2026-01-24 23.48.25.excalidraw]]

![[Hexapod 2026-01-25 10.30.21.excalidraw]]


**Design**
- **Power Rail Filtering:** The Nucleo uses an extensive array of **100nF decoupling capacitors** (one for every VDD pin) plus a single **4.7µF bulk capacitor**.
    
- **VCAP Pin:** For the F401RE, **Pin 31 (VCAP_1)** must be connected to a **2.2µF capacitor** tied to GND. This is for the internal voltage regulator; without it, the MCU will not start.
    
- **Clocking (HSE):** The Nucleo connects an 8MHz clock from the ST-LINK bypass or a crystal to **PH0 and PH1**.
    
- **Reset (NRST):** The reset line (Pin 7) includes a **100nF capacitor** to GND and a push button, with a pull-up provided internally by the MCU or an external **10kΩ resistor**.
    
- **SWD Interface:** For programming your custom board, you need a header connecting to **PA13 (SWDIO)**, **PA14 (SWCLK)**, **NRST**, and **GND**.