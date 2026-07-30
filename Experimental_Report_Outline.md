# EXPERIMENTAL MEASUREMENT REPORT: GEAR DRIVE SYSTEM

> **Experiment Objective:**
> To simultaneously collect multi-channel data from multiple sensor types (acceleration, proximity, torque, speed) for the diagnosis and condition monitoring of gear faults under various operating conditions (speed, load, fault type, gear material).

---

## PART 1: DRIVE SYSTEM

### 1.1. Prime Mover

#### a. Electric Motor — GIN RE ELECTRIC MOTOR GR-5IK90A-S

| Parameter | Value |
|:---|:---|
| Manufacturer | GIN RE ELECTRIC MOTOR |
| Model | GR-5IK90A-S |
| Rated Power | 90 W |
| Rated Current | 0.55 A |
| Rated Torque | 5.5 kg·cm (≈ 0.54 N·m) |
| Voltage | 220 V / 3-phase |
| Number of Pole Pairs ($p$) | 2 pole pairs (4 poles) |
| Maximum Speed | 1750 rpm |

The motor speed is controlled via the YASKAWA V1000 inverter. With $p = 2$ pole pairs, the synchronous shaft speed corresponding to the inverter output frequency is given by:

$$n = \frac{60 \times f}{p}$$

Motor shaft speed at each preset frequency:

| Inverter Frequency ($f$) | Synchronous Speed ($n$) |
|:---:|:---:|
| 10 Hz | 300 rpm |
| 20 Hz | 600 rpm |
| 30 Hz | 900 rpm |
| 40 Hz | 1200 rpm |
| 50 Hz | 1500 rpm |

> [!NOTE]
> The actual shaft speed will be slightly lower than the synchronous speed due to slip in the induction motor (typically 3–5%). The actual speed must be measured directly by the encoder mounted on the motor shaft to ensure accuracy in signal analysis.

---

#### b. Variable Frequency Drive — YASKAWA V1000 (CIMR-VU Series)

**Key Technical Specifications:**

| Parameter | Value |
|:---|:---|
| Manufacturer | Yaskawa Electric Corporation |
| Product Line | V1000 / CIMR-VU Series (CIMR-VUBA — Single-Phase 200V) |
| Input Voltage | Single-phase 200–240 VAC (+10%, -15%), 50/60 Hz (±5%) |
| Output Voltage | 3-phase 200–240 VAC (proportional to input voltage) |
| Output Frequency Range | 0.01 – 400 Hz |
| Control Method | Open-Loop Current Vector (OLV); V/f; PM OLV |
| Overload Capacity | Heavy Duty: **150%** for 60 s; Normal Duty: **120%** for 60 s |
| Communication | Built-in RS-485 (Memobus/Modbus RTU, up to 115.2 kbps); optional: PROFIBUS-DP, EtherCAT, EtherNet/IP, PROFINET, CANopen |
| Protection Class | IP20 (open chassis); optional NEMA Type 1 |
| Operating Temperature | -10°C to +50°C |

**Control Panel and Power-Up Procedure:**

The V1000 inverter is operated as follows:

1. **Power ON:** Push the NFB (No-Fuse Breaker) on the control panel to the ON position to supply 3-phase 220V to the inverter.
2. **Set Frequency:** Press the `LO/RE` key to switch to Local control mode. Use the `▲` / `▼` arrow keys to adjust the frequency. Press `ENTER` to save.
3. **Start Motor:** Press the `RUN` key — the indicator light will illuminate and the motor will start at the set frequency.
4. **Stop Motor:** Press the `STOP` key.

Preset frequencies used in this experiment: **10 Hz, 20 Hz, 30 Hz, 40 Hz, 50 Hz**.

---

### 1.2. Drive Train

#### a. Motor-to-Gearbox Coupling — Synchronous Belt Drive

**Belt:**

| Parameter | Value |
|:---|:---|
| Manufacturer / Part No. | Gates PowerGrip **339-GT3** |
| Belt Type | Synchronous (Timing) Belt |
| Material | Synthetic rubber (EPDM or Neoprene) with fiberglass tension cords |
| Belt Circumference | 339 mm |
| Tooth Pitch | 3 mm (GT3 = Gates Tooth 3mm pitch) |
| Number of Teeth | 113 |
| Belt Width | 6.4 mm |

**Pulleys:**

| Parameter | Value |
|:---|:---|
| Number of Teeth | 34T (same for both driving and driven pulleys — belt ratio 1:1) |
| Tip Diameter | ≈ 31.68 mm |
| Tooth Width | 7.04 mm |
| Material | Unknown (likely steel or aluminum) |
| Tooth Profile | Rounded (GT3 profile) |

> [!NOTE]
> Since both pulleys have the same number of teeth (34T), the belt drive ratio is **1:1** — meaning the gearbox input speed equals the motor shaft output speed.

---

#### b. Gear Drive System — 2-Stage Reduction Gearbox

**Drive Configuration:**

The gearbox uses a **2-stage series reduction** layout with 3 shafts and 4 gears:

```
Input shaft
    └─ Stage 1 driving gear: Z₁ = 25 teeth
            ↓ mesh
        Stage 1 driven gear: Z₂ = 50 teeth  (on Intermediate shaft)
        Stage 2 driving gear: Z₃ = 25 teeth (also on Intermediate shaft)
            ↓ mesh
        Stage 2 driven gear: Z₄ = 50 teeth  (on Output shaft)
```

**Overall Gear Ratio:**

$$i_{total} = i_1 \times i_2 = \frac{Z_2}{Z_1} \times \frac{Z_4}{Z_3} = \frac{50}{25} \times \frac{50}{25} = 2 \times 2 = \mathbf{4:1}$$

Output shaft speed:

$$n_{out} = \frac{n_{motor}}{i_{total}} = \frac{n_{motor}}{4}$$

**Gear Specifications:**

| Parameter | Small Gears (Z₁, Z₃) | Large Gears (Z₂, Z₄) |
|:---|:---:|:---:|
| Type | Spur Gear | Spur Gear |
| Number of Teeth ($Z$) | 25 | 50 |
| Module ($m$) | 2 | 2 |
| Pressure Angle ($\alpha$) | 20° | 20° |
| Tip Diameter ($D_a$) | 54 mm | 104 mm |

**Gear Mesh Frequency (GMF):**

Stage 1: $f_{GMF1} = Z_1 \times f_{shaft,in} = 25 \times f_{motor}$

Stage 2: $f_{GMF2} = Z_3 \times f_{shaft,intermediate} = 25 \times \frac{f_{motor}}{2}$

---

**Available Gear Test Sets:**

| Set | Description | Material | Surface Treatment |
|:---:|:---|:---|:---|
| **Set 1** | 2 pairs — 4 gears. **All gears are healthy (no faults).** | Steel S45C | Electroless nickel plating |
| **Set 2** | 3 small gears (25T) with **tooth root crack** faults at 3 different severity levels | Steel S45C | None |
| **Set 3** | 3 small gears (25T) with **tooth root crack** faults at 3 different severity levels | Aluminum (Al) | Unknown |
| **Set 4** | 2 pairs — 4 gears: 2 large gears (50T) healthy; 1 small gear with **chipped tooth**, 1 small gear with **missing tooth** | Unknown | Unknown |

---

**Rolling Bearings — NACHI 6201ZE:**

| Parameter | Value |
|:---|:---|
| Model | NACHI 6201ZE |
| Type | Single-Row Deep Groove Ball Bearing |
| Bore Diameter ($d$) | 12 mm |
| Outer Diameter ($D$) | 32 mm |
| Width ($B$) | 10 mm |
| Mass | ≈ 0.037 kg |
| Dynamic Load Rating ($C_r$) | 6,800 N |
| Static Load Rating ($C_{or}$) | 3,050 N |
| Max Speed (grease lubrication) | 22,000 rpm |
| Max Speed (oil lubrication) | 28,000 rpm |

Bearing fault characteristic frequencies (BPFO, BPFI, BSF, FTF) can be derived from the bearing geometry and number of rolling elements to support signal analysis.

**Bearing Housing:** Dimensions and shape to be reported later. Material unknown (likely gray cast iron FC200 per common industrial practice).

**Jaw Coupling:** Used at shaft connection points to compensate for misalignment and dampen shock loads transmitted between shafts.

---

#### c. Output Load — Magnetic Powder Brake

| Parameter | Value |
|:---|:---|
| Load Device | Magnetic Powder Brake |
| Model | Unknown |
| Operating Principle | Braking torque is controlled by varying the exciting voltage applied to the brake coil, which adjusts the magnetic flux density and the frictional force of the magnetic powder |
| Exciting Voltage Range | 0 – 25 V (continuously adjustable) |
| Adjustment Method | Rotary resistor 0 – 5.37 kΩ |
| Brake Controller | Ji-Xiang (https://www.ji-xiang.com/product) |
| Controller Power Supply | Mean Well RS-25-5 (5 VDC, 5 A) |

---

## PART 2: MEASUREMENT SYSTEM

### General Sensor Principles

A sensor is a transducer that converts a physical quantity (acceleration, force, speed, displacement, etc.) into an electrical signal (voltage, current, or digital pulses) that can be processed by a data acquisition system. The fundamental conversion mechanism relies on the following principle: when the physical quantity being measured changes, it alters an electrical or mechanical property of the sensor's sensitive element (resistance, capacitance, inductance, piezoelectricity, etc.), which produces a corresponding change in the output current or voltage.

---

### 2.1. Sensors

#### a. Motor Encoder — Integrated Optical Incremental Encoder

**Purpose:** Measures the instantaneous rotational speed and angular position of the motor shaft.

**Structure and Location:**
The encoder is integrated directly onto the rear (tail end) of the motor and is co-axial with the motor shaft.

**Power Supply:** Mean Well RS-25-5 (5 VDC).

**Specifications:**

| Parameter | Value |
|:---|:---|
| Pulses Per Revolution (PPR) | 1024 |
| Output Type | Two-channel square wave (Quadrature Encoder) — channels A and B |
| Supply Voltage | 5 VDC |

**Operating Principle (Optical Encoder):**
An optical encoder consists of a code disc with alternating transparent slots and opaque segments, positioned between an infrared LED source and a photodetector. As the shaft rotates, the slots alternately pass and block the light, generating a sequence of square pulses.

**Reading Quadrature Signals (Channels A and B):**
Channels A and B are offset by 90° (quarter-cycle phase shift). This enables:
- **Direction detection:** If channel A leads B → clockwise rotation; if B leads A → counter-clockwise.
- **4× resolution (x4 decoding):** Counting all four rising and falling edges of both channels A and B → with PPR = 1024, the effective resolution becomes **4096 counts/revolution**.
- **Speed calculation:** $n = \frac{\text{pulse count} \times 60}{PPR \times \Delta t}$ (rpm).

In this experiment, channels A and B are read into the NI USB-6210 module via the Counter/Timer inputs (PFI0, PFI1).

---

#### b. Vibration Sensor — PCB Piezotronics 356A32/NC

> [!NOTE]
> **Model Clarification:** A search of the PCB Piezotronics database confirms the correct model number is **356A32/NC** (not 365A32). This is a triaxial ICP® accelerometer by PCB Piezotronics.

**Purpose:** Measures vibration acceleration along 3 axes (X, Y, Z) at the rolling bearing housing nearest to the faulty gear.

**Sensor Type:** IEPE (Integrated Electronics Piezo-Electric).

**IEPE Operating Principle:**
IEPE sensors (also known as ICP® — Integrated Circuit Piezoelectric) operate on the piezoelectric effect: when a piezoelectric crystal (typically PZT — Lead Zirconate Titanate, or quartz) is subjected to mechanical stress caused by acceleration, it generates an electric charge on its surface. This charge is amplified by a built-in preamplifier integrated within the sensor body, and the output is delivered as a low-impedance voltage signal over a single coaxial cable. The DAQ module supplies a constant DC current (typically 2–20 mA) through the coaxial cable to power the amplifier, and reads the AC signal superimposed on that DC bias.

**Advantage of IEPE:** Low-impedance voltage output allows transmission over long cables without signal degradation and with immunity to electromagnetic interference (EMI).

**Technical Specifications — PCB 356A32/NC:**

| Parameter | Value |
|:---|:---|
| Model | **356A32/NC** (PCB Piezotronics) |
| Type | Triaxial ICP® Accelerometer |
| Sensing Principle | Piezoelectric IEPE (ICP®) |
| Sensitivity | **100 mV/g** (10.2 mV/(m/s²)) ±10% |
| Measurement Range | ±50 g peak (±491 m/s² peak) |
| Frequency Range (±5%) | **1.0 – 4,000 Hz** |
| Frequency Range (±10%) | 0.7 – 5,000 Hz |
| Resonant Frequency | ≥ 25 kHz |
| Resolution (Noise Floor) | 0.0003 g rms (0.003 m/s² rms) |
| IEPE Excitation Current | 2 – 20 mA |
| Output Bias Voltage | 7 – 16 VDC (Excitation: 24–30 VDC) |
| Mass | 5.4 g (0.19 oz) |
| Connector | 8-36 4-pin receptacle (side exit) |

**Mounting Location:** The sensor is mounted directly on the rolling bearing housing at the position closest to the faulty gear under investigation, to capture the highest-energy vibration signal before it attenuates through the test rig structure.

---

#### c. Proximity Sensor — Bently Nevada 3300 XL NSv Proximity Transducer System

**Purpose:** Measures shaft phase — determines the instantaneous angular position of the gear during each revolution, enabling Order Tracking analysis and angle-domain data synchronization.

**Equipment Source:** Borrowed from a rotor dynamics test kit provided by Bently Nevada.

**Operating Principle:**
The eddy-current proximity probe operates on the eddy-current principle: the probe coil generates a high-frequency alternating magnetic field. When a conductive surface (gear face or metal shaft) approaches the probe, the magnetic field induces eddy currents in the conductive material, which attenuates the field amplitude and changes the coil impedance. This change is linearly proportional to the gap between the probe tip and the metal surface, and is converted to a DC voltage output by the proximitor signal conditioner.

**Phase Measurement Application:**
As the gear rotates, the gap between the probe and the surface varies continuously following the gear tooth profile — tooth tips produce a smaller gap (lower voltage), tooth roots produce a larger gap (higher voltage). From this waveform, the following can be extracted:
- **Instantaneous shaft rotational speed** (from the repetition frequency of the signal pattern).
- **Angular phase position** of each tooth at each time instant.
- This information is used for signal filter design and Order Tracking analysis.

**Power and Signal Chain:**

```
RK4 Rotor Kit Motor Speed Controller
    └─> RK4 Proximitor Assembly (provides DC power to probe + amplification + filtering)
            └─> Proximity Probe (sensing tip)
            └─> Output (filtered DC voltage signal) → NI USB-9234 (AI3)
```

**Technical Specifications — Bently Nevada 3300 XL NSv:**

| Parameter | Value |
|:---|:---|
| System | Bently Nevada 3300 XL NSv Proximity Transducer |
| Probe Model | Unknown (borrowed from Bently Nevada Rotor Kit) |
| Sensing Principle | Eddy-Current |
| Supply Voltage | **-17.5 VDC to -26 VDC** (nominal -24 VDC), max 12 mA |
| Scale Factor | **7.87 V/mm (200 mV/mil)** nominal (calibrated for AISI 4140 steel targets) |
| Linear Range | **1.5 mm (60 mils)** — from 0.25 mm to 1.75 mm (10 to 70 mils) |
| Output Voltage at Center Gap | -10.0 VDC (recommended gap: ~0.75 mm / 30 mils) |
| Frequency Response | **0 Hz – 10 kHz** (+0, -3 dB) |
| Operating Temperature (Probe) | -51°C to +177°C |
| Operating Temperature (Proximitor) | -51°C to +100°C |

**Mounting Location:** Positioned above the gear, with the probe axis directed radially toward the gear center.

---

#### d. Torque Sensor — JIHSENSE Rotary Torque Sensor RT-2.5 Nm

**Purpose:** Measures the braking torque applied by the magnetic powder brake to the gearbox output shaft.

**Operating Principle — Wheatstone Bridge Strain Gauge:**
This rotary torque sensor operates on the mechanical strain gauge (loadcell) principle: thin-film resistive strain gauges are bonded to a torsion-elastic shaft at 45° to the shaft axis (the orientation that maximizes sensitivity to shear stress from torsion). When the shaft is subjected to torque, shear stress causes elastic deformation, which changes the resistance of the strain gauges. Four gauges are connected in a Wheatstone bridge — the bridge imbalance is linearly proportional to the applied torque. The bridge signal is transmitted externally via carbon brushes contacting slip rings on the rotating shaft.

**Technical Specifications — RT-2.5 Nm:**

| Parameter | Value |
|:---|:---|
| Manufacturer | JIHSENSE Industrial |
| Model | RT-2.5 Nm (Rotary Torque Sensor) |
| Measurement Range | 0 – 2.5 N·m |
| Rated Output | 1.0 mV/V |
| Total Error | ±0.3% R.O. |
| Repeatability | ±0.2% R.O. |
| Creep | 0.1%/20 min |
| Input Resistance | 430 Ω or 385 Ω or 350 Ω |
| Output Resistance | 350 Ω |
| Max Excitation Voltage | 20 V |
| Recommended Excitation | 10 V |
| Safe Overload | 150% of rated load |
| Operating Temperature | -10°C to +50°C |
| Temp. Effect on Zero | 0.05% R.O./10°C |
| Temp. Effect on Span | 0.03% Load/10°C |
| Cable Length | 3 m |
| Wiring | Red(+) Exci, Black(-) Exci / Green(+) Sign, White(-) Sign |
| Maximum Speed | 200 rpm (for RT-1 to RT-10 Nm range) |

**Signal Amplifier — JS-100 Load Cell Amplifier (JIHSENSE):**
The millivolt-level signal from the torque sensor Wheatstone bridge is too small to be read directly by a DAQ module. The JS-100 amplifier performs the following:
- Supplies the excitation voltage to the Wheatstone bridge.
- Amplifies the differential bridge signal to a usable voltage level.
- Applies active second-order noise filtering.
- Output: ±5 V, ±10 V, or 4–20 mA (configurable).

**Torque Calculation from Amplifier Output Signal:**

For a 4–20 mA output configuration with load resistance $R_L$ (Ω):

$$U_{out} = I_{out} \times R_L \quad \text{(V)}$$

$$T = \frac{U_{out} - U_{min}}{U_{max} - U_{min}} \times T_{rated} \quad \text{(N·m)}$$

Where $T_{rated} = 2.5$ N·m, and $U_{min}$, $U_{max}$ are the voltages corresponding to 4 mA and 20 mA respectively.

**Mounting Location:** Installed between the magnetic powder brake and the gearbox output shaft, connected to both shafts via jaw couplings on each end.

---

#### e. Data Acquisition Module — NI USB-9234 (via Prowave PW700 Converter)

> [!NOTE]
> This module is the **NI USB-9234**, connected to the PC via a **Prowave PW700 Series** RS-232-to-USB converter. The combined unit is sometimes referred to as "NI PW9234A" in local documentation.

**Introduction:**
The NI USB-9234 is a dynamic signal acquisition (DSA) module from National Instruments, designed specifically for sound and vibration measurements. It features software-selectable per-channel IEPE excitation and AC/DC coupling.

**Technical Specifications — NI USB-9234:**

| Parameter | Value |
|:---|:---|
| Manufacturer | National Instruments (NI) |
| Analog Input Channels | 4 channels (AI0 – AI3), simultaneous sampling |
| Maximum Sample Rate | 51.2 kS/s per channel |
| ADC Resolution | 24 bit |
| Input Voltage Range | ±5 V |
| IEPE Support | Yes — software-selectable per channel |
| IEPE Excitation Current | 2 mA (typical) |
| Coupling | AC or DC — software-selectable per channel |
| Physical Connector | BNC (one BNC per channel) |
| PC Interface | USB (via Prowave PW700 RS-232→USB converter) |
| Anti-Aliasing Filter | Built-in automatic anti-aliasing filter |

**Channel Wiring:**

| Sensor | DAQ Channel |
|:---|:---:|
| Accelerometer X-axis | AI0 |
| Accelerometer Y-axis | AI1 |
| Accelerometer Z-axis | AI2 |
| Proximity Sensor | AI3 |

---

#### f. Data Acquisition Module — NI USB-6210

**Introduction:**
The NI USB-6210 is a general-purpose M-Series DAQ device from National Instruments supporting both analog voltage input and digital/counter input. It connects via screw-terminal blocks, making it suitable for reading the torque amplifier analog output and the encoder quadrature pulse signals.

**Technical Specifications — NI USB-6210:**

| Parameter | Value |
|:---|:---|
| Manufacturer | National Instruments (NI) |
| Analog Input Channels | 16 single-ended (RSE/NRSE) or 8 differential (DIFF) |
| Maximum Sample Rate | 250 kS/s |
| ADC Resolution | 16 bit |
| Input Voltage Range | Software-selectable: ±0.2 V, ±1 V, ±5 V, ±10 V |
| Digital I/O | 8 lines (4 DI + 4 DO), 5V TTL/CMOS |
| Counter/Timer | 2 × 32-bit counters, 80 MHz max source frequency |
| PFI Pins | 8 Programmable Function Interface pins (usable as counter inputs) |
| Physical Connector | 68-pin connector or screw terminal block |
| PC Interface | USB |

**Channel Wiring:**

| Signal | NI USB-6210 Terminal |
|:---|:---:|
| Encoder Channel A | PFI0 |
| Encoder Channel B | PFI1 |
| Encoder GND | DGND |
| Torque Amplifier Output (+) | AI0+ |
| Torque Amplifier Output (–) | AI0– |

---

## PART 3: LABVIEW PROGRAMMING

### 3.1. Introduction to LabVIEW

LabVIEW (Laboratory Virtual Instrument Engineering Workbench) is a graphical programming environment (G language) developed by National Instruments, specifically designed for data acquisition, instrument control, and signal processing in laboratory and industrial settings. Each LabVIEW program is called a **Virtual Instrument (VI)** and consists of two components:
- **Front Panel:** The user interface (control knobs, graphs, indicators, buttons, etc.).
- **Block Diagram:** The graphical programming canvas where nodes and functions are connected by data wires (dataflow programming paradigm).

---

### 3.2. DAQ Assistant vs. DAQmx API

LabVIEW provides two approaches for interfacing with DAQ hardware:

| Criterion | DAQ Assistant | DAQmx API |
|:---|:---|:---|
| Creation Method | Drag-and-drop with graphical configuration wizard | Manual programming with DAQmx function library |
| Configurability | Limited — does not allow deep configuration | Full control over clock, trigger, buffer, and per-channel settings |
| Multi-device Support | Limited | Full — supports synchronization across multiple modules |
| Best For | Quick prototyping and testing | Rigorous experiments with multi-channel, multi-device setups |

**Why DAQmx API is Preferred in This Experiment:**
This measurement system uses 2 different DAQ modules (NI USB-9234 and NI USB-6210) and 4 different signal types (IEPE acceleration, proximity DC voltage, torque analog, encoder quadrature pulses). DAQ Assistant does not fully support hardware clock/trigger synchronization across devices, nor does it allow fine-grained per-channel IEPE on/off, AC/DC coupling, or high-resolution quadrature counter decoding. The DAQmx API provides all of these capabilities through its complete programming interface.

---

### 3.3. DAQmx Task Creation Workflow

Standard steps for building a DAQmx data acquisition loop in LabVIEW:

```
1. DAQmx Create Task           → Create a new task
2. DAQmx Create Virtual Channel → Define virtual channel(s) (Analog Input, Counter, Digital)
                                   Configure: device name, measurement range, coupling, IEPE on/off
3. DAQmx Timing (Sample Clock)  → Configure the sample clock
                                   Set: sample rate, samples per read,
                                   mode: Continuous Samples or Finite Samples (N Samples)
4. DAQmx Trigger (optional)     → Configure a Start Trigger
                                   Can use a trigger from another channel for synchronization
5. DAQmx Start Task             → Begin data acquisition
6. DAQmx Read (in a loop)       → Read data from hardware buffer periodically
7. Write / Display Data         → Write to Measurement File, or push to Queue/FIFO
8. DAQmx Stop Task              → Stop acquisition
9. DAQmx Clear Task             → Release hardware resources
```

---

### 3.4. Producer–Consumer Loop with Queue

To efficiently read and write data without dropping samples, the LabVIEW program uses a **Producer–Consumer Loop** architecture with a **Queue**:

```
┌──────────────────────────────┐      Queue      ┌───────────────────────────────┐
│       PRODUCER LOOP          │  ───────────►   │       CONSUMER LOOP           │
│  (runs at acquisition rate)  │                 │  (runs at file-write rate)    │
│                              │                 │                               │
│  DAQmx Read → Enqueue Data   │                 │  Dequeue Data → Write File    │
│                              │                 │  (or update waveform chart)   │
└──────────────────────────────┘                 └───────────────────────────────┘
```

**Advantages:**
- The **Producer** loop (data read from DAQ) runs at high speed, ensuring no samples are missed.
- The **Consumer** loop (file writing or display) runs independently, processing data from the Queue as capacity allows, without blocking or delaying the acquisition loop.
- The **Queue** acts as a FIFO buffer between the two loops, preventing data loss when the file-write rate is slower than the acquisition rate.

---

## PART 4: RESULTS, LIMITATIONS, AND FUTURE WORK

### 4.1. Results Achieved

- Full assembly and configuration of the measurement system has been completed, including 4 sensor types (triaxial accelerometer, proximity transducer, torque sensor, speed encoder) and 2 DAQ modules (NI USB-9234, NI USB-6210).
- A LabVIEW program has been developed to simultaneously acquire data from all sensor channels.
- Raw measurement data can be recorded to file for post-processing and analysis.

---

### 4.2. Current Limitations and Challenges

| # | Issue | Details |
|:---:|:---|:---|
| 1 | **Missing material specifications** | The materials of the bearing housings, shafts, pulleys, and gear set 4 have not been fully identified, which complicates structural modeling and stress analysis. |
| 2 | **System alignment not performed** | The geometric alignment of shafts and components, as well as bearing preload conditions, have not been reliably established or verified. |
| 3 | **Manual brake load control** | The brake load is currently adjusted manually via a rotary resistor. This approach lacks precision and repeatability, making it difficult to establish controlled and reproducible loading conditions for systematic experiments. |
| 4 | **Data sources not synchronized** | Data from the NI USB-9234 and NI USB-6210 are not yet time-synchronized — the actual sampling timestamps do not consistently match the configured timer target, causing misalignment in multi-channel signal analysis. |

---

### 4.3. Future Work

1. **Synchronize sampling across all signal sources:** Research and implement a hardware synchronization mechanism (shared hardware clock or start trigger) or a software-based alignment method between the NI USB-9234 and NI USB-6210 to ensure temporal consistency across all measurement channels.

2. **Automate brake load control:** Investigate replacing the manual rotary resistor with an electronic controller (DAC output or PWM signal) to precisely and repeatably set the brake exciting voltage via software. This will enable systematic experimental designs with controlled loading profiles (constant load, ramp load, step load, etc.).

3. **Align and calibrate the entire test rig:** Perform shaft alignment across all coupled components, and verify and zero the torque sensor and accelerometer offsets before each measurement session.

4. **Systematic data collection and signal analysis:** Once the above steps are completed, acquire data for all 4 gear test sets across multiple speeds (10, 20, 30, 40, 50 Hz) and load levels, then perform spectral analysis of the vibration signals to identify and classify the gear fault signatures.
