# 📋 Bill of Materials (BOM)

Complete component list for building the Analog Temperature-Based Automatic Fan Control System.

---

## 🛒 Quick Overview

| Category | Quantity | Estimated Cost |
|----------|----------|-----------------|
| **Semiconductors** | 2 | $2–5 |
| **Resistors** | 4–5 | $0.50–1 |
| **Capacitors** | 2–3 | $0.50–1 |
| **Thermistor** | 1 | $1–3 |
| **Potentiometer** | 1 | $1–2 |
| **Passive Components** | 2–3 | $0.50–1 |
| **Breadboard & Wires** | 1 | $5–10 |
| **Power Supply** | 1 | $5–15 |
| **Fan** | 1 | $3–8 |
| **Miscellaneous** | - | $1–2 |
| **TOTAL** | - | **$19–48** |

---

## 📦 Detailed Component List

### **1. SEMICONDUCTORS**

#### Op-Amp (Operational Amplifier)

| Part | Value | Qty | Unit Price | Supplier Links |
|------|-------|-----|------------|-----------------|
| **LM358** | General purpose, dual op-amp | 1 | $0.50–1 | [Digi-Key](https://www.digikey.com/en/products/detail/texas-instruments/LM358N/LM358N-ND) |
| **LM741** | Classic op-amp (alternative) | 1 | $0.80–1.50 | [Mouser](https://www.mouser.com/ProductDetail/Texas-Instruments/LM741CN) |
| **TL072** | Low-noise (premium option) | 1 | $1–2 | [Amazon](https://www.amazon.com/TL072-Operational-Amplifier-Audio-DIY/dp) |

**Recommended:** LM358 (widely available, cheap, good for this application)

**Pin Configuration (8-pin DIP):**
```
     ┌──┐
  1-─┤  ├─ 8 (Vcc+)
  2-─┤  ├─ 7 (Vcc-)
  3-─┤  ├─ 6 (Output)
  4-─┤  ├─ 5
     └──┘
(Notch indicates pin 1)
```

**Datasheet:** [LM358 PDF](https://www.ti.com/lit/ds/symlink/lm358.pdf)

---

#### Transistor (NPN BJT)

| Part | Value | Qty | Unit Price | Supplier Links |
|------|-------|-----|------------|-----------------|
| **BC547** | NPN, 100mA, 45V | 1 | $0.10–0.30 | [eBay](https://www.ebay.com/sch/i.html?_nkw=BC547+transistor) |
| **2N2222** | NPN, 800mA, 30V (alternative) | 1 | $0.20–0.50 | [Digi-Key](https://www.digikey.com/en/products/detail/on-semiconductor/2N2222G/1557-1-ND) |
| **TIP31C** | NPN, 3A, 40V (high current) | 1 | $0.50–1 | [Mouser](https://www.mouser.com/ProductDetail/ON-Semiconductor/TIP31C) |

**Recommended:** BC547 (sufficient for most DC fans, cheap, easy to find)

**Pin Configuration (TO-92):**
```
Looking at flat side:
  ┌────┐
  │    │
B─┤    ├─ C (Collector)
  │    │
E─┤    ├─
  └────┘
(Emitter)
```

**Datasheet:** [BC547 PDF](https://www.onsemi.com/pub/Collateral/BC546-D.PDF)

---

### **2. RESISTORS (Carbon Film, 1/4W)**

| Value | Qty | Purpose | Tolerance | Unit Price | Notes |
|-------|-----|---------|-----------|------------|-------|
| **10kΩ** | 2 | Thermistor divider + Op-amp base | 5% | $0.05 | Standard resistor |
| **10kΩ** | 1 | Hysteresis (optional) | 5% | $0.05 | Add if fan chatters |
| **1kΩ** | 1 | Current limiting (optional) | 5% | $0.05 | For high-current transistor |

**Total Resistors:** $0.20–0.50

**Where to buy:**
- Individual: [eBay](https://www.ebay.com/sch/i.html?_nkw=10k+resistor+100+pack)
- Assorted pack: [Amazon - 600 piece kit](https://www.amazon.com/MCIGICM-Resistor-Assortment-Tolerance-Certified/dp/B07QH5D9F7)

---

### **3. CAPACITORS**

#### Ceramic Capacitors (Noise Decoupling)

| Value | Qty | Voltage | Purpose | Unit Price | Supplier |
|-------|-----|---------|---------|------------|----------|
| **100nF (0.1µF)** | 2 | 25V | Bypass filtering on op-amp pins 4 & 8 | $0.05 | [Digi-Key](https://www.digikey.com/en/products/detail/kyocera-avx/SR223C104KAA/2011012) |

#### Electrolytic Capacitors (Optional - Smoothing)

| Value | Qty | Voltage | Purpose | Unit Price | Supplier |
|-------|-----|---------|---------|------------|----------|
| **10µF** | 1 | 25V | Output smoothing (reduces chattering) | $0.10 | [Mouser](https://www.mouser.com/ProductDetail/Panasonic/ECA1HHG100B) |

**⚠️ Polarity Warning:** Long lead = positive, short lead = negative

**Total Capacitors:** $0.15–0.30

---

### **4. THERMISTOR (Temperature Sensor)**

| Part | Value | Qty | B-value | Unit Price | Supplier Links |
|------|-------|-----|---------|------------|-----------------|
| **NTC Thermistor** | 10kΩ @ 25°C | 1 | 3950K | $1–2 | [eBay - NTC 10k](https://www.ebay.com/sch/i.html?_nkw=NTC+10k+thermistor) |
| **NTC Thermistor** | 4.7kΩ @ 25°C | 1 | 3950K | $0.80–1.50 | [Amazon](https://www.amazon.com/Gaoxin-NTC-Thermistor-Resistor-3950/dp) |
| **Precision NTC** | 10kΩ @ 25°C | 1 | 3950K | $1.50–3 | [Digi-Key - Vishay](https://www.digikey.com/en/products/detail/vishay-bc-components/NTC-22D-15/1037997) |

**Recommended:** Generic NTC 10kΩ @ 25°C (works well, cheap)

**Temperature Range:** -40°C to +125°C (typical)

**Package Options:**
- Through-hole (easier for breadboard)
- Surface mount (smaller, requires soldering)

**How to identify:** Small ceramic bead with 2 leads, often marked with resistance value

**Datasheet:** Search "NTC 10k 3950 thermistor" for generic datasheets

---

### **5. POTENTIOMETER (Variable Resistor)**

| Part | Value | Qty | Type | Unit Price | Supplier Links |
|------|-------|-----|------|------------|-----------------|
| **Linear Potentiometer** | 10kΩ | 1 | 3-pin | $0.50–1 | [eBay](https://www.ebay.com/sch/i.html?_nkw=10k+potentiometer+linear+3pin) |
| **Precision Potentiometer** | 10kΩ | 1 | Trimmer | $1–2 | [Mouser](https://www.mouser.com/ProductDetail/Bourns/3362P-1-103LF) |
| **Rotary Potentiometer** | 10kΩ | 1 | With knob | $1–2 | [Amazon](https://www.amazon.com/EDGELEC-potentiometer-resistor-assorted-Potentiometer/dp) |

**Recommended:** 10kΩ linear (breadboard-friendly, knob adjustable)

**Pin Configuration (3-pin linear):**
```
Pin 1 (End) ───── Vcc or GND
Pin 2 (Wiper) ─── To op-amp pin 2
Pin 3 (End) ───── GND or Vcc
```

---

### **6. DIODE (Flyback Protection)**

| Part | Value | Qty | Voltage | Current | Unit Price | Supplier |
|------|-------|-----|---------|---------|------------|----------|
| **1N4007** | 1000V rectifier | 1 | 1000V | 1A | $0.05 | [eBay](https://www.ebay.com/sch/i.html?_nkw=1N4007+diode+100+pack) |
| **1N4148** | Fast switching | 1 | 100V | 200mA | $0.05 | [Digi-Key](https://www.digikey.com/en/products/detail/on-semiconductor/1N4148/458603) |
| **1N4001** | 50V rectifier | 1 | 50V | 1A | $0.05 | [Mouser](https://www.mouser.com/ProductDetail/ON-Semiconductor/1N4001GP) |

**Recommended:** 1N4007 (standard, widely available, works fine)

**Purpose:** Protects transistor from back-EMF when fan motor is switching off

**Polarity:** 
- Anode (no band) → To transistor collector
- Cathode (banded end) → To ground/fan negative

---

### **7. DC FAN**

| Type | Voltage | Size | Current | Speed | Unit Price | Supplier |
|------|---------|------|---------|-------|------------|----------|
| **Brushless 12V** | 12V DC | 40mm | 0.1–0.3A | 2000–4000 RPM | $3–5 | [Amazon](https://www.amazon.com/s?k=12v+40mm+brushless+fan) |
| **Brushless 5V** | 5V DC | 40mm | 0.1–0.2A | 2500–5000 RPM | $2–4 | [eBay](https://www.ebay.com/sch/i.html?_nkw=5v+40mm+fan) |
| **Brushed 12V** | 12V DC | Varies | 0.2–0.5A | 2000–3000 RPM | $2–3 | [Alibaba](https://www.alibaba.com/trade/search) |

**Recommended:** 12V brushless 40mm (cheap, quiet, reliable)

**Connection:**
- Red wire → Power (through transistor collector)
- Black wire → Ground (through diode)

**Note:** Choose voltage to match your power supply (9V → use 12V fan, 5V → use 5V fan)

---

### **8. POWER SUPPLY**

| Type | Voltage | Current | Cost | Supplier |
|------|---------|---------|------|----------|
| **9V Battery** | 9V DC | 500mA | $2–3 | Any convenience store |
| **12V Wall Adapter** | 12V DC | 1A | $5–10 | [Amazon](https://www.amazon.com/s?k=12v+1a+wall+adapter) |
| **USB Power Bank** | 5V DC | 1–2A | $5–15 | [Amazon](https://www.amazon.com/s?k=power+bank) |
| **Regulated Bench Supply** | Variable | 1–5A | $30–100 | [Amazon - Bench supplies](https://www.amazon.com/s?k=regulated+power+supply) |

**Recommended:** 12V 1A wall adapter (stable, affordable, reusable)

**Requirements:**
- Minimum 500mA current capability
- Regulated (stable voltage)
- Proper connector for breadboard

---

### **9. BREADBOARD & JUMPER WIRES**

| Item | Qty | Size | Pins | Cost | Supplier |
|------|-----|------|------|------|----------|
| **Breadboard** | 1 | 830 tie-point | 2 rows of 415 | $2–4 | [Amazon](https://www.amazon.com/Breadboard-Solderless-Prototype-Distribution-Connecting/dp/B07DL13RZH) |
| **Jumper Wire Kit** | 1 | Mix 65–75pcs | Multiple | $3–5 | [eBay](https://www.ebay.com/sch/i.html?_nkw=breadboard+jumper+wire+kit) |
| **Individual Wires** | - | 22AWG | Bare | $0.01 each | [Digi-Key](https://www.digikey.com/en/products/filter/wire/123?s=N4IgjCBcoDQBwFYGcB2AHAZgKbQOQ3swBGArlAKgDIgOgO4+hBi2OAzgGZOhBi2OARlADsdgUAXlAA) |

**Total:** $5–9

---

## 🔧 TOOLS & EQUIPMENT (Not included in BOM)

**Required:**
- [ ] Multimeter (analog or digital, $5–50)
- [ ] Screwdriver set (if potentiometer has screw)
- [ ] Needle-nose pliers (for bending wire leads)
- [ ] Wire strippers (for stripping jumper wires)

**Optional:**
- [ ] Soldering iron (not needed for breadboard)
- [ ] Anti-static mat and wrist strap ($5–10)
- [ ] Thermometer (for calibration)

---

## 📊 COST BREAKDOWN

### **Budget Option ($18–25)**
- Generic LM358 op-amp ($0.50)
- BC547 transistor ($0.15)
- 10kΩ resistors 5-pack ($0.25)
- 100nF capacitors 2-pack ($0.10)
- Generic NTC 10kΩ thermistor ($1)
- Linear 10kΩ potentiometer ($0.75)
- 1N4007 diode 100-pack ($0.50)
- 12V 40mm brushless fan ($3)
- Breadboard + jumper wires kit ($8)
- 12V 1A wall adapter ($5)
- **Total: ~$20**

### **Mid-Range Option ($30–40)**
- TL072 op-amp ($1.50)
- 2N2222 transistor ($0.35)
- Precision resistor assortment ($1)
- 100nF capacitors + 10µF capacitor ($0.50)
- Precision NTC thermistor ($2)
- Premium potentiometer with knob ($1.50)
- Mixed diode assortment ($1)
- 12V 50mm brushless fan ($5)
- Large breadboard (2 x) + premium jumpers ($12)
- Adjustable bench power supply ($15)
- **Total: ~$40**

### **Premium Option ($50+)**
- Matched op-amp pair ($3)
- TIP31C high-current transistor ($1)
- Precision resistor kit ($2)
- Quality capacitor assortment ($2)
- Industrial-grade thermistor ($5)
- Multi-turn precision potentiometer ($3)
- Schottky diode ($0.50)
- Multiple fans for testing ($10)
- Professional breadboard kit ($20)
- Regulated bench supply with digital display ($30)
- **Total: ~$75**

---

## ✅ COMPONENT CHECKLIST

Before assembly, verify you have all parts:

### **Semiconductors**
- [ ] 1x Op-Amp (LM358 or LM741)
- [ ] 1x NPN Transistor (BC547 or equivalent)
- [ ] 1x Diode (1N4007)

### **Resistors (1/4W, 5% tolerance)**
- [ ] 2x 10kΩ (thermistor divider + base resistor)
- [ ] 1x 10kΩ (hysteresis - optional)
- [ ] 1x 1kΩ (optional, for current limiting)

### **Capacitors**
- [ ] 2x 100nF ceramic (bypass)
- [ ] 1x 10µF electrolytic (optional, smoothing)

### **Sensors & Control**
- [ ] 1x NTC Thermistor (10kΩ @ 25°C)
- [ ] 1x 10kΩ Linear Potentiometer (3-pin)

### **Power & Interface**
- [ ] 1x 12V 1A Power Supply (or 9V battery)
- [ ] 1x 12V DC Fan (or 5V depending on supply)
- [ ] 1x Breadboard (830 tie-point recommended)
- [ ] 1x Jumper Wire Kit (65+ pieces)

### **Tools**
- [ ] 1x Multimeter
- [ ] 1x Needle-nose pliers
- [ ] 1x Wire stripper

---

## 🌍 WHERE TO BUY

### **Electronics Retailers**
1. **Digi-Key** (https://www.digikey.com) - Fast shipping, large inventory
2. **Mouser** (https://www.mouser.com) - Worldwide shipping
3. **SparkFun** (https://www.sparkfun.com) - Educational focus, good tutorials
4. **Adafruit** (https://www.adafruit.com) - Great for beginners

### **Budget Options**
1. **eBay** (https://www.ebay.com) - Cheap bulk parts, slower shipping
2. **Amazon** (https://www.amazon.com) - Fast Prime shipping, assorted kits
3. **AliExpress** (https://www.aliexpress.com) - Cheapest, very slow shipping
4. **Alibaba** (https://www.alibaba.com) - Bulk orders, industrial suppliers

### **Local Options**
1. **Radio Shack** - If still open in your area
2. **Local electronics shops** - Support local business
3. **Universities** - Sometimes have surplus stores
4. **Maker spaces** - Borrow or buy from community labs

---

## 📝 ASSEMBLY TIPS

1. **Check component orientation before placing on breadboard**
   - Op-amp notch must point correct direction
   - Diode band must face ground side
   - Capacitor polarity if electrolytic (+/-)

2. **Test components individually first**
   - Verify resistor values with multimeter
   - Check diode continuity
   - Measure thermistor resistance at room temp

3. **Use quality breadboard connections**
   - Ensure jumper wires push firmly into slots
   - No loose connections = 90% of problems solved

4. **Keep power supply disconnected during assembly**
   - Only power on when circuit is complete
   - Double-check all connections before powering

5. **Label your components**
   - Use tape to mark component values
   - Helps when troubleshooting later

---

## 🔗 USEFUL REFERENCES

- **Op-Amp Basics:** https://learn.sparkfun.com/tutorials/operational-amplifiers
- **Transistor Circuits:** https://en.wikipedia.org/wiki/Transistor_circuits
- **Thermistor Guide:** https://learn.adafruit.com/thermistor
- **Breadboard Guide:** https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard
- **Component Datasheets:** https://www.alldatasheet.com/

---

**Ready to build? See [CALIBRATION.md](CALIBRATION.md) for assembly instructions!** ✓
