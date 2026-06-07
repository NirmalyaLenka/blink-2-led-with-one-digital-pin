# Circuit Explanation

## The Problem

A standard digital output pin on an Arduino Uno can only drive one LED reliably. To drive two LEDs, the usual approach is to use two pins, a multiplexer IC, or a shift register. This project sidesteps all of that using a property that is already built into how LEDs work.

---

## The Core Idea

An LED is a diode. It only allows current to flow in one direction, from anode (+) to cathode (-). If the voltage across it is reversed, or if there is no potential difference, no current flows and the LED stays off.

This gives us a way to control two LEDs from one pin:

- Wire LED1 so its anode connects (through a resistor) to the pin and its cathode connects to GND.
- Wire LED2 so its anode connects (through a resistor) to the 5V rail and its cathode connects to the same pin.

Now the pin controls both, but in opposite directions.

---

## State Table

| Pin 8 State | LED1 (Anode on Pin 8) | LED2 (Cathode on Pin 8) |
|-------------|----------------------|------------------------|
| HIGH (5V)   | ON                   | OFF                    |
| LOW (0V)    | OFF                  | ON                     |

When the pin is HIGH, LED1 has 5V at its anode and 0V at its cathode, so it conducts. LED2 has 5V at its anode and 5V at its cathode, so there is no potential difference and it does not conduct.

When the pin is LOW, LED1 has 0V at its anode and 0V at its cathode, no potential difference, so it stays off. LED2 has 5V at its anode and 0V at its cathode, so it conducts.

---

## Current Limiting

Each LED has a 1k ohm resistor in series. At 5V, with a typical red or green LED forward voltage of around 2V, the current through each active LED is approximately:

```
I = (5V - 2V) / 1000 ohm = 3 mA
```

The Arduino Uno can safely source or sink up to 40 mA per pin. 3 mA is well within this limit. If you want brighter output, you can reduce the resistors to around 220 ohms, which brings the current to roughly 13 mA, still within the safe operating range.

---

## Limitations

- Both LEDs cannot be ON at the same time with this wiring. The alternating behavior is fixed by the circuit topology, not just the code.
- If you need independent control of each LED (both on, both off, or any combination), you need two separate pins.
- The brightness of LED2 depends on the 5V rail being stable. On USB power this is fine. On a battery-powered setup, verify that the supply voltage is sufficient.

---

## Why This Is Useful

This technique is practical when you have used most of your digital pins on a project and need a simple indicator pair, such as a pass/fail indicator, a direction indicator, or a heartbeat signal that alternates between two colors. It costs nothing in hardware and requires only one pin.
