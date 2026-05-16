# 🌡️ Analog Temperature-Based Automatic Fan Control System

An analog electronics project that automatically controls a DC fan speed based on ambient temperature using an op-amp comparator, NTC thermistor, and supporting passive components — no microcontroller required.

---

## 📌 Overview

This system senses temperature through a thermistor voltage divider and uses an op-amp to compare it against a reference threshold. When the temperature exceeds the set point, the fan is switched on (or its speed is varied). The design is fully analog, making it simple, fast-responding, and power-efficient.

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

The circuit schematic is available in the `/schematic` folder.

```
/schematic
  └── fan_control_schematic.pdf   ← Main circuit diagram
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

## 📁 Repository Structure

```
analog-fan-control/
├── schematic/
│   └── fan_control_schematic.pdf
├── README.md
└── LICENSE
```

---

## 🚀 Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/analog-fan-control.git
   ```
2. Open the schematic PDF in the `/schematic` folder.
3. Assemble the circuit on a breadboard or PCB.
4. Power on with a 9V–12V DC supply.
5. Adjust the potentiometer to set your desired temperature threshold.

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

- Course Instructor: **Engr. Fazeel Abbas**
- References: Analog Electronics textbooks and op-amp application notes
