# ESP32 OLED Frame Animation

Plays a 294-frame animation on a 128x64 SSD1306 OLED driven by an ESP32-C3.
The frames are stored as bitmaps in flash (`PROGMEM`) and drawn one after
another at a fixed frame rate.

Author: Jhon Lee Quint

**Run it online:** [Wokwi simulation](https://wokwi.com/projects/452093329805054977)

## Hardware

| Part | Connection |
|---|---|
| ESP32-C3-DevKitM-1 | — |
| SSD1306 128x64 OLED (I2C, address `0x3C`) | SDA 8, SCL 9, 3V3, GND |

The full wiring is in [`diagram.json`](diagram.json).

## How it works

- Each frame is 128x64 pixels at 1 bit per pixel, i.e. 1024 bytes. The
  294 frames take about 294 KB of flash.
- `FRAME_COUNT` is derived from the array size, so frames can be added or
  removed without touching the loop.
- `FRAME_DELAY` sets the time per frame (70 ms by default, about 14 fps).
- Frame bitmaps were generated with [image2cpp](https://javl.github.io/image2cpp/)
  (horizontal, 1 bit per pixel).

## Replacing the animation

1. Export the animation as 128x64 frames.
2. Convert them in image2cpp to an Arduino byte array, one array per frame.
3. Replace the contents of `frames[]` in `sketch.ino`.

## Project layout

| File | Responsibility |
|---|---|
| `sketch.ino` | Frame data, display setup and playback loop |
| `diagram.json` | Wokwi circuit |
| `libraries.txt` | Wokwi library list |

## Building locally

Install the ESP32 board package and the **Adafruit SSD1306** and
**Adafruit GFX** libraries, then select *ESP32C3 Dev Module*.
