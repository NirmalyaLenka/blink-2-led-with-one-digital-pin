# One Pin, Two LEDs

Control two LEDs with a single digital output pin on an Arduino Uno. The LEDs blink in alternating fashion: when one is on, the other is off. No extra ICs or shift registers are needed. The trick relies on wiring the two LEDs in opposite polarity on the same pin.

---

## How It Works

A digital output pin can be either HIGH (5V) or LOW (0V). By connecting one LED so that its anode faces the pin and the other so that its cathode faces the pin, the two LEDs respond in opposite ways to the same signal.

```
Pin 8 HIGH:
  LED1: anode at 5V, cathode at GND  ->  ON
  LED2: cathode at 5V, anode at 5V   ->  OFF  (no potential difference)

Pin 8 LOW:
  LED1: anode at 0V, cathode at GND  ->  OFF
  LED2: cathode at 0V, anode at 5V   ->  ON
```

A 1k ohm resistor in series with each LED limits the current to a safe level (approximately 4 mA per LED at 5V).

---

## Components

| Component        | Quantity | Notes                    |
|------------------|----------|--------------------------|
| Arduino Uno      | 1        |                          |
| LED (any color)  | 2        | Purple and cyan used here |
| Resistor, 1k ohm | 2        | 1/4 W or higher           |
| Breadboard       | 1        |                          |
| Jumper wires     | 4-5      |                          |

---

## Wiring

| Connection       | From        | To          |
|------------------|-------------|-------------|
| LED1 path        | Pin 8       | R1 (1k)     |
|                  | R1          | LED1 Anode  |
|                  | LED1 Cathode| GND         |
| LED2 path        | 5V          | R2 (1k)     |
|                  | R2          | LED2 Anode  |
|                  | LED2 Cathode| Pin 8       |

See `diagram/wiring_diagram.png` for a visual reference.

---

## Files

```
one_pin_2_leds/
├── src/
│   └── one_pin_2_leds.ino     # Arduino sketch
├── diagram/
│   └── wiring_diagram.png     # Circuit diagram
├── docs/
│   └── explanation.md         # Detailed circuit explanation
├── README.md
└── LICENSE
```

---

## Getting Started

1. Wire the circuit as described above (see the diagram).
2. Open `src/one_pin_2_leds.ino` in the Arduino IDE.
3. Select board: Tools > Board > Arduino Uno.
4. Select the correct COM port under Tools > Port.
5. Click Upload.
6. Both LEDs will start blinking alternately at one-second intervals.

---

## Customization

- Change the blink speed by adjusting the `delay(1000)` values (milliseconds).
- Use any color of LED. Forward voltage differences between colors will slightly affect brightness but will not prevent operation at 5V with a 1k resistor.
- Pin 8 can be changed to any digital output pin by updating the `ledPin` constant.

---

## Simulate Online

This project was originally built and simulated on Wokwi:  
https://wokwi.com/projects/465977896205616129

---

## License

MIT License. See `LICENSE` for details.
