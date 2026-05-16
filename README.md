# 🌡️ Analog Temperature-Based Automatic Fan Control System

An analog electronics project that automatically controls a DC fan speed based on ambient temperature using an op-amp comparator, NTC thermistor, and supporting passive components — no microcontroller required!

---

## 📌 Overview

This system senses temperature through a thermistor voltage divider and uses an op-amp to compare it against a reference threshold. When the temperature exceeds the set point, the fan is switched on intelligently. Perfect for passive cooling applications and analog electronics learning.

---

## ⚙️ How It Works

```
[Thermistor + Resistor Divider]
            │
            ▼
    [Op-Amp Comparator / Amplifier]
            │
            ▼
   [Transistor Switch / Driver]
            │
            ▼
        [DC Fan]
```

1. **Sensing:** An NTC thermistor forms a voltage divider with a fixed resistor. As temperature rises, thermistor resistance drops, increasing the voltage at the sensing node.
2. **Comparison:** An op-amp (e.g., LM358 or LM741) compares the thermistor voltage against a user-set reference voltage (via a potentiometer).
3. **Switching/Driving:** The op-amp output drives a transistor (e.g., BC547 / TIP31C) which switches the fan ON/OFF or varies its speed.
4. **Fan Control:** The DC fan runs when the temperature crosses the threshold and turns off when it cools down.

---

## 🧰 Components Used

| Component | Description |
|-----------|-------------|
| NTC Thermistor | Temperature-sensing element (e.g., 10kΩ at 25°C) |
| Op-Amp | LM358 / LM741 — comparator stage |
| Resistors | Voltage divider and biasing network |
| Potentiometer | Adjustable temperature threshold reference |
| Transistor | BC547 / TIP31C — fan driver |
| Diode | Flyback protection for the fan motor (e.g., 1N4007) |
| DC Fan | 5V or 12V brushless/brushed DC fan |
| Power Supply | 9V–12V DC |
| Capacitors | Noise decoupling (optional but recommended) |

---

## 📐 Circuit Schematic

The circuit schematic and project photos are available in the root directory:

```
analog-fan-control/
├── fan_control_schematic.png   ← Main circuit diagram
├── P1.jpeg                      ← Photo 1 of the assembled circuit
├── P2.jpeg                      ← Photo 2 of the assembled circuit
├── Demo.mp4                     ← Video demonstration of the system
├── README.md                    ← This file
├── BOM.md                       ← Bill of Materials
├── CALIBRATION.md               ← Calibration Guide
├── TROUBLESHOOTING.md           ← Troubleshooting Tips
└── LICENSE                      ← Project License
```

---

## 📊 Key Design Parameters

- **Supply Voltage:** 9V – 12V DC
- **Thermistor Type:** NTC (Negative Temperature Coefficient)
- **Temperature Threshold:** Adjustable via potentiometer (~30°C – 70°C range)
- **Op-Amp Configuration:** Open-loop comparator (bang-bang control)
- **Fan Voltage:** 5V or 12V (depending on fan spec)

---

## 🔬 Working Principle (Detailed)

The NTC thermistor and a fixed resistor form a **voltage divider**:

```
V_sense = Vcc × R_fixed / (R_thermistor + R_fixed)
```

As temperature increases → R_thermistor decreases → V_sense increases.

The op-amp compares V_sense (non-inverting input) to V_ref (inverting input, set by potentiometer):
- If `V_sense > V_ref` → Op-amp output goes HIGH → Transistor turns ON → Fan runs
- If `V_sense < V_ref` → Op-amp output goes LOW → Transistor turns OFF → Fan stops

---

## 🚀 Getting Started

1. **Clone this repository:**
   ```bash
   git clone https://github.com/Mmamoonn/analog-fan-control.git
   cd analog-fan-control
   ```

2. **Review the documentation:**
   - Open `fan_control_schematic.png` to see the circuit diagram
   - Check `BOM.md` for a complete list of components
   - Read `CALIBRATION.md` for setup instructions

3. **Assemble the circuit:**
   - Use a breadboard or PCB based on the schematic
   - Refer to `P1.jpeg` and `P2.jpeg` for assembly reference

4. **Power on and test:**
   - Connect a 9V–12V DC power supply
   - Adjust the potentiometer to set your desired temperature threshold
   - See `TROUBLESHOOTING.md` if you encounter any issues

5. **Watch the demo:**
   - View `Demo.mp4` to see the system in action

---

## 📖 Documentation

- **[BOM.md](BOM.md)** - Complete bill of materials with part numbers and suppliers
- **[CALIBRATION.md](CALIBRATION.md)** - Step-by-step calibration and setup guide
- **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - Common issues and solutions

---

## 📄 License

This project is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.
You are free to share and adapt this work as long as appropriate credit is given.

See the [LICENSE](LICENSE) file for full details.

---

## 👤 Author

**Mamoon**  
Robotics Engineering Student

---

## 🙏 Acknowledgements

- References: Analog Electronics textbooks and op-amp application notes
- Community feedback and contributions welcome!
