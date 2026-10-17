# 💧 Smart Irrigation Simulator

An Arduino-based smart irrigation system that automatically waters plants when
the soil gets dry. A soil moisture sensor feeds readings to the Arduino, and
when moisture drops below a configurable threshold, the pump (simulated by a
red LED) switches ON — no manual watering needed.

**▶️ Try it live on Wokwi (no hardware required):** https://wokwi.com/projects/478056834107943937

## How It Works

Every 500 ms, the Arduino:

1. Reads the soil moisture sensor on analog pin **A0** (0–1023)
2. Prints the raw reading to the Serial Monitor (9600 baud)
3. Compares it against the dryness threshold (`threshold = 500`):
   - **Reading < 500** → soil is dry → pump (LED) turns ON
   - **Reading ≥ 500** → soil is moist → pump stays OFF

**Why lower = drier:** the sensor returns a higher voltage when soil is wet,
so a *low* analog reading means *dry* soil. In the Wokwi simulation, a
potentiometer stands in for the real moisture sensor — drag it to see the pump
trigger live.

The threshold lives in a single variable (`threshold`), so it's easy to retune
for different soil types or plants.

## Hardware

| Part | Role |
|---|---|
| Arduino UNO | Microcontroller board |
| Soil moisture sensor (potentiometer in sim) | Moisture reading on A0 |
| Red LED (pin 13) | Represents the water pump |
| 220Ω resistor | LED current limiting |

## Wiring

| Sensor / LED | Arduino UNO Pin |
|---|---|
| Sensor VCC | 5V |
| Sensor GND | GND |
| Sensor SIG | A0 |
| LED Anode (+) | D13 |
| LED Cathode (−) | GND |

The exact layout is defined in [`diagram.json`](diagram.json) — open the Wokwi
link above to see the wired circuit.

## Files

- `sketch.ino` — the Arduino program (moisture reading, threshold check, pump control)
- `diagram.json` — Wokwi circuit definition (board, parts, wiring)

## Sample Serial Output

```
720      ← moist soil, pump OFF
680
300      ← dry soil, pump turns ON
290
```

## How to Run

**Option 1 — Wokwi (easiest):** click the link above, press ▶️ Play, and open
the Serial Monitor. Drag the potentiometer *below* the middle of its range —
when the reading drops under 500, the red LED lights up as the "pump" starts.

**Option 2 — Real hardware:** wire the circuit as above, flash the sketch with
the Arduino IDE, open Serial Monitor at 9600 baud.

## Concepts Demonstrated

- Analog input (`analogRead`) and 10-bit ADC values (0–1023)
- Threshold-based decision logic (`if` / `else`)
- Digital output control (`digitalWrite`)
- Serial communication for live telemetry
- Sensor polling with a timing loop (`delay`)

## Planned Improvements

- [ ] Real soil moisture sensor (capacitive type recommended)
- [ ] Drive an actual relay + water pump
- [ ] LCD display of moisture percentage
- [ ] Add dryness *and* temperature conditions (see my [smart-irrigation-simulator-2.0](https://github.com/AkashBGBhat/smart-irrigation-simulator-2.0))
- [ ] Replace `delay()` with `millis()` for non-blocking reads
- [ ] Hysteresis band to prevent pump rapid-cycling near the threshold
- [ ] ESP32 + Wi-Fi version with automated watering schedules

## Built With

- Arduino UNO (C++ / Arduino framework)
- [Wokwi](https://wokwi.com) — browser-based simulation

## Author

**Akash Bhat** — [github.com/AkashBGBhat](https://github.com/AkashBGBhat)
