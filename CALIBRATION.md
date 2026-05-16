# 🔧 Calibration & Setup Guide

Step-by-step guide to properly assemble, calibrate, and fine-tune your Analog Fan Control System.

---

## ⚠️ Pre-Assembly Safety Checklist

Before you start, make sure you have:

- [ ] **Power supply disconnected** (or turned off)
- [ ] **Multimeter ready** (you'll need it for testing)
- [ ] **All components verified** against [BOM.md](BOM.md)
- [ ] **Schematic printed** or open on screen
- [ ] **Breadboard clean** (no old components left over)
- [ ] **Workspace clear** (adequate lighting, organized)
- [ ] **No food or drinks** near electronics
- [ ] **Static mat or wrist strap** (optional but recommended)

---

## 📐 Assembly Guide

### **Step 1: Layout Planning**

Arrange your breadboard sections:

```
Left Side:        Middle:           Right Side:
Thermistor        Op-Amp            Transistor & Fan
Divider           Comparator        Driver Circuit
Potentiometer     Buffer
```

### **Step 2: Install Power Rails**

1. **Connect positive rail (Vcc):**
   - Power supply red lead → top positive rail

2. **Connect ground rail (GND):**
   - Power supply black lead → top ground rail

3. **Add a "strip" of power across breadboard:**
   - Jump from positive rail to positive power strip
   - Jump from ground rail to ground strip
   - This ensures even power distribution

**Test with multimeter:**
```
Measure between any Vcc point and GND point
Should read 9–12V DC
```

---

### **Step 3: Install Op-Amp**

**LM358 8-pin DIP layout:**

```
Pin positions on breadboard:
┌────────────┐
│ 1  2  3  4 │ Row A
│ 8  7  6  5 │ Row B
└────────────┘

Position op-amp with notch facing LEFT
```

**Connections:**
- **Pin 1** (Trim): Leave unconnected
- **Pin 2** (Inv. In): Connect to threshold voltage (potentiometer)
- **Pin 3** (Non-Inv. In): Connect to thermistor divider
- **Pin 4** (GND): Connect to ground rail
- **Pin 5** (Trim): Leave unconnected
- **Pin 6** (Output): Connect to transistor base (via 10kΩ resistor)
- **Pin 7** (Vcc-): Connect to ground rail (for single supply) OR leave open
- **Pin 8** (Vcc+): Connect to Vcc rail (9–12V)

**Add bypass capacitors:**
- 100nF between pin 8 and pin 4 (noise decoupling)
- 100nF between pin 7 and pin 4 (if pin 7 not used)

---

### **Step 4: Install Thermistor Divider**

Create a voltage divider using thermistor and resistor:

```
           Vcc (9–12V)
              │
         ┌────┴────┐
         │          │
        ╱╲         10kΩ
      NTC │      Resistor
   Therm.╲         │
         └────┬────┘
              │
          To Op-Amp Pin 3
              │
             GND
```

**Assembly:**
1. Connect thermistor between Vcc and center node
2. Connect 10kΩ resistor between center node and GND
3. Tap center node → connect to op-amp pin 3 (non-inverting input)

**Test with multimeter (room temperature):**
```
Measure voltage at center node
Should read 3–6V (depends on thermistor type)
```

---

### **Step 5: Install Potentiometer (Threshold)**

The potentiometer sets the reference voltage for comparison:

```
          Vcc (9–12V)
             │
        ┌────┴────┐
        │ Pot    │
        │ 10kΩ   │
        │        │
    ┌───┴────┬───┴──┐
    │        │      │
  Pin 1    Pin 2   Pin 3
  (Sweep) (Wiper) (End)
           │
    To Op-Amp Pin 2
    (Inverting Input)
           │
           GND
```

**Connections (standard configuration):**
- **One end** → Vcc (9–12V)
- **Wiper (middle)** → Op-amp pin 2 (inverting input)
- **Other end** → GND (0V)

**Adjustment range:**
- Fully CCW (toward 0°): Pin 2 ≈ 0V (low threshold, fan on early)
- Fully CW (toward 9V): Pin 2 ≈ 9V (high threshold, fan on late)

---

### **Step 6: Install Transistor & Driver**

**BC547 NPN Transistor layout:**

```
Looking at flat side:
  ┌────┐
  │    │ (Flat side)
B─┤    ├─C (Collector)
  │    │
E─┤    ├─
  └────┘
(Emitter)
```

**Connections:**
- **Base (B)** → Op-amp pin 6 output (via 10kΩ resistor)
- **Collector (C)** → Fan positive terminal (through flyback diode)
- **Emitter (E)** → GND (0V)

**Install flyback diode:**
```
     Transistor Collector
              │
              │
        ──────┼──── Diode Anode
             /  \
            / 1N │ (Band marks cathode)
            \4007/
             \  /
              ─┼────── Diode Cathode
              │
             GND
              
        → Diode protects transistor from back-EMF
```

---

### **Step 7: Connect Fan**

**Fan connection:**

```
Diode Anode ─────→ Fan (+) (Red wire)
Diode Cathode ────→ Fan (-) & GND (Black wire)
```

**Test fan independently first:**
```
Connect fan directly to 12V power supply
If fan spins: Good
If fan doesn't spin: Check polarity or fan is broken
```

---

## 🔌 Full Circuit Diagram Reference

```
                    Vcc (9–12V)
                       │
        ┌──────────────┼──────────┐
        │              │          │
      ╱╲            10kΩ      Pot-End1
     NTC │Thermistor  │    10kΩ Pot
     Divider         │          │
        │            ├─Pin2(Op) ├─Pin-Mid(Op)
        │            │          │
    ┌───┴────┐  ┌────┴─┐        │
    │        │  │      │    ┌───┴────┐
    │ 10kΩ   │  │LM358 │    │  Pot   │
    │Resist. │  │  +   │    └───┬────┘
    │        ├──┤3(+)  │        │
    └────┬───┘  │      ├────────┴─ Pot-End2 (GND)
         │      │6(Out)│
        GND     └┬─────┘
                 │
              10kΩ Base
              Resistor
                 │
            ┌────┴────┐
            │  BC547  │B
            │Transistor│
         C──┤         │
            │    E────┴─── GND
            └────┬────┘
                 │
            Flyback Diode (1N4007)
            (Cathode to GND)
                 │
             ┌───┴────┐
             │   DC   │
             │  Fan   │
             └────┬───┘
                 GND
```

---

## 📊 Calibration Procedure

### **Phase 1: Visual Verification**

Before powering on:

1. **Check all connections match schematic**
   - Op-amp pins 2, 3, 6, 8, 4 verified
   - Thermistor in divider
   - Potentiometer connected
   - Transistor base from op-amp (with 10kΩ resistor)
   - Diode oriented correctly (band toward GND)

2. **Check for visible shorts**
   - No jumper wires touching unintended connections
   - No exposed leads touching power rails

3. **Verify component orientation**
   - Op-amp notch pointing correct direction
   - Transistor flat side correct way
   - Capacitor polarity correct (if electrolytic)

---

### **Phase 2: Power-On Test (No Fan)**

1. **Disconnect fan temporarily** (test op-amp alone first)

2. **Turn on power supply**
   ```
   Measure Vcc rail: Should read 9–12V ✓
   Measure op-amp pin 8: Should read 9–12V ✓
   Measure op-amp pin 4: Should read 0V (GND) ✓
   ```

3. **Check op-amp inputs**
   ```
   Measure pin 2 (from potentiometer):
     Start position: _____ V
     
   Measure pin 3 (from thermistor):
     Room temperature: _____ V
   ```

4. **Observe op-amp output (pin 6)**
   ```
   Should read either ~0V (LOW) or ~9V (HIGH)
   
   If 4–5V (in middle): Might be oscillating or unstable
   Solution: Add 100kΩ hysteresis resistor from pin 6 to pin 3
   ```

---

### **Phase 3: Potentiometer Calibration**

1. **Slowly adjust potentiometer**
   ```
   Turn potentiometer knob back and forth (full range)
   Measure pin 2 voltage:
     Fully CCW (0°): Should be ~0V
     Fully CW (360°): Should be ~9V
   ```

2. **Find threshold point**
   ```
   Set potentiometer to approximately middle
   Adjust until op-amp output (pin 6) switches
   
   This is your initial "threshold voltage"
   Record it: V_threshold = _____ V
   ```

3. **Lock the potentiometer** (optional)
   ```
   Once you find desired threshold, you can:
   - Tighten set-screw (if potentiometer has one)
   - Mark position on knob with tape
   - Use epoxy to lock shaft (permanent)
   ```

---

### **Phase 4: Temperature Calibration**

Now connect the thermistor and test temperature response:

#### **Cold Test (Ice Bath):**

1. **Prepare ice bath:**
   ```
   Fill cup with ice + water (0°C)
   Thermometer optional but helpful
   ```

2. **Immerse thermistor:**
   ```
   Hold thermistor in ice bath for 30 seconds
   Let thermal equilibrium settle (another 30 seconds)
   Measure op-amp input (pin 3): _____ V
   Observe op-amp output (pin 6): LOW (0V) or HIGH (9V) ?
   ```

3. **Expected behavior:**
   ```
   Ice bath (cold): V_pin3 drops → Op-amp should output LOW (0V)
   
   This should turn fan OFF
   ```

#### **Room Temperature Test:**

1. **Let thermistor return to room temperature:**
   ```
   Wait 2–3 minutes for thermal equilibrium
   Measure op-amp input (pin 3): _____ V
   Observe op-amp output (pin 6): LOW or HIGH ?
   ```

#### **Hot Test (Warm Water):**

1. **Prepare warm water:**
   ```
   Fill cup with warm (not boiling) water (~40–50°C)
   ```

2. **Immerse thermistor:**
   ```
   Hold thermistor in warm water for 30 seconds
   Measure op-amp input (pin 3): _____ V
   Observe op-amp output (pin 6): LOW (0V) or HIGH (9V) ?
   ```

3. **Expected behavior:**
   ```
   Warm water (hot): V_pin3 rises → Op-amp should output HIGH (9V)
   
   This should turn fan ON
   ```

---

### **Phase 5: Fan Connection & Full System Test**

1. **Power OFF the system**

2. **Connect fan to transistor:**
   ```
   Transistor collector → Fan positive (via diode)
   GND rail → Fan negative
   ```

3. **Power ON and test:**

   **Cold test:**
   ```
   Ice bath: Fan should be OFF
   ```

   **Room temperature:**
   ```
   At normal temperature: Fan OFF or ON ?
   Adjust potentiometer to set correct threshold
   ```

   **Hot test:**
   ```
   Warm water: Fan should be ON
   Listen for motor spin
   Feel for air movement
   ```

4. **Fine-tune threshold:**
   ```
   Adjust potentiometer slowly
   Find temperature where fan switches
   
   Record this as your working threshold: _____ °C
   ```

---

## 📈 Temperature Reference Table

Use this table to estimate your current temperature based on voltage reading at op-amp pin 3:

| Temperature | V_pin3 (est.) | Thermistor R | Notes |
|-------------|--------------|--------------|-------|
| -10°C | ~6.5V | 35kΩ | Very cold |
| 0°C (Ice) | ~5.8V | 25kΩ | **Cold test point** |
| 10°C | ~5.1V | 18kΩ | Winter indoors |
| 20°C | ~4.4V | 13kΩ | Cool room |
| 25°C | ~3.9V | 10kΩ | **Room temperature** |
| 30°C | ~3.4V | 7.5kΩ | Warm room |
| 40°C | ~2.6V | 5.0kΩ | **Hot test point** |
| 50°C | ~1.9V | 3.3kΩ | Very hot |
| 60°C | ~1.3V | 2.2kΩ | Extremely hot |
| 70°C | ~0.9V | 1.5kΩ | Critical heat |

**How to use this table:**
1. Measure voltage at op-amp pin 3 (in ice bath, room, warm water)
2. Find the matching row in table
3. This tells you approximate current temperature
4. Adjust potentiometer to switch fan at desired temperature

---

## 🎛️ Fine-Tuning Adjustments

### **If threshold is too low (fan turns on when too cold):**
- **Solution:** Turn potentiometer CW (toward Vcc)
- **Effect:** Increases reference voltage, requiring higher thermistor voltage to trigger
- **Result:** Fan will turn on at higher temperature

### **If threshold is too high (fan turns on when too hot):**
- **Solution:** Turn potentiometer CCW (toward GND)
- **Effect:** Decreases reference voltage, requiring lower thermistor voltage to trigger
- **Result:** Fan will turn on at lower temperature

### **If fan chatters or oscillates:**
- **Problem:** Threshold very close to room temperature
- **Solution 1:** Move potentiometer further from current temperature
- **Solution 2:** Add hysteresis resistor (100kΩ–1MΩ) from pin 6 to pin 3
- **Effect:** Creates dead zone (~1–2°C) to prevent rapid switching

### **If fan doesn't turn off when cooling down:**
- **Problem:** May need hysteresis to create "dead zone"
- **Solution:** Add 100kΩ hysteresis resistor between op-amp output (pin 6) and non-inverting input (pin 3)

---


## ✅ System Verification Checklist

Before declaring setup complete:

- [ ] Fan spins when transistor base is HIGH (9V)
- [ ] Fan stops when transistor base is LOW (0V)
- [ ] Thermistor causes op-amp output to change when temperature changes
- [ ] Potentiometer adjusts threshold smoothly (not stuck)
- [ ] No chattering or oscillation (or hysteresis resistor added to fix)
- [ ] System remains stable for 10+ minutes at room temperature
- [ ] Ice bath test: Fan OFF when cold
- [ ] Hot water test: Fan ON when warm
- [ ] No components getting hot or burning
- [ ] All multimeter readings make sense

**✅ System is calibrated and ready to use!**

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues.

---

## 🚀 Advanced Calibration (Optional)

### **Adding Hysteresis for Stability**

If fan chatters, add a 100kΩ–1MΩ resistor:
```
From op-amp output (pin 6) to non-inverting input (pin 3)

This creates a dead zone:
- Hysteresis = ~1–2°C (for 100kΩ resistor)
- Fan won't flicker on/off rapidly
```

### **Temperature-to-Celsius Conversion**

If you want accurate temperature readout:
1. Create reference points (ice + warm water)
2. Measure voltages at each point
3. Plot linear regression
4. Use formula: `T(°C) = m × V + b`

### **PWM Speed Control (Advanced)**

For variable fan speed (not just ON/OFF):
- Requires microcontroller (Arduino, PIC)
- Op-amp output drives PWM input
- Varies fan voltage smoothly (not in scope of analog-only design)

---

**Calibration complete! Your system is ready for use.** 🎉
