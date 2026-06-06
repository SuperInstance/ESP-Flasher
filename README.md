# ESP-Flasher

**Browser-based firmware flasher for ESP32 — and the bridge between git-native AI agents and physical hardware.**

## What It Does

ESP-Flasher lets you flash `.bin` firmware files onto ESP32 boards and monitor their serial output, all from your web browser. No software installation. No drivers. Just open Chrome, connect, and flash.

## The Bigger Picture

This fork is part of the **[SuperInstance Oxide Stack](https://github.com/SuperInstance/cuda-oxide/blob/main/FLUX_TO_PTX.md)** — a distributed compute runtime where AI agents can program physical hardware through git-native skill swapping.

**Read the full architecture**: [AGENT_ARCHITECTURE.md](./AGENT_ARCHITECTURE.md)

```
User → AI Agent → ESP-Flasher (browser) → ESP32 workers
                ↓
        Git repos = skill library
        Each repo compiles to .bin firmware
        Agent hot-swaps skills based on task
```

### Use Cases

- **Smart Agriculture**: Agent monitors weather + soil → hotloads irrigation skill → verifies results
- **Home Automation**: "Movie night" → agent flashes dim/AV/blind skills to 3 ESP32s
- **Research Labs**: Hot-swap data collection → calibration → analysis skills between experiment runs
- **Industrial IoT**: Central agent assigns firmware to 50+ ESP32 workers based on production schedule
- **Education**: Students write code → agent compiles and flashes → iterate

### Why It Matters

The ESP-Flasher is the **cudaclaw of microcontrollers** — it persists and loads executable images to workers, except the "GPU" is an ESP32 and the "kernel" is bare-metal firmware. Combined with [ternary-esp32-firmware](https://github.com/SuperInstance/ternary-esp32-firmware) (Z₃ operations in 279 bytes, 8ns lookups), you get a complete system where AI agents physically interact with the world.

## Features

- 🌐 **Zero install** — runs entirely in the browser (Chrome/Edge)
- ⚡ **Real-time serial monitor** with search, auto-scroll, ASCII/HEX/BIN
- 🔌 **Multi-board support** — ESP32, S2, S3, C3, C6 + clones (CP2102, CH340, FTDI)
- 📦 **Drag-and-drop** firmware flashing
- 🤖 **Agent-ready** — Web Serial API enables programmatic control from AI agents

## Supported Boards

| Board | Connection | Notes |
|-------|-----------|-------|
| ESP32 | USB-UART | Original Espressif + clones |
| ESP32-S2 | Native USB | |
| ESP32-S3 | Native USB | |
| ESP32-C3 | USB-JTAG / Native USB | |
| ESP32-C6 | USB-JTAG | |

## Quick Start

```bash
# Serve locally
npx serve .

# Or just open index.html in Chrome
```

1. Click **Connect** → select your board's serial port
2. Drag a `.bin` file into the Flash Firmware section
3. Click **Flash**
4. Monitor output in real-time terminal

## Connection to the Oxide Stack

| Layer | ESP-Flasher Analog |
|-------|-------------------|
| **open-parallel** (async runtime) | Browser event loop + Web Serial |
| **pincher** (intent→compile) | Agent selects skill → compiles firmware |
| **flux-core** (bytecode VM) | ESP32 executes compiled firmware |
| **cuda-oxide** (compiler) | Cross-compiler: Rust/C → Xtensa .bin |
| **cudaclaw** (persistent kernels) | Firmware in git, cached locally |

## Related Projects

- [ternary-esp32-firmware](https://github.com/SuperInstance/ternary-esp32-firmware) — Bare-metal Z₃ operations (279 bytes)
- [ternary-hotswap-inference](https://github.com/SuperInstance/ternary-hotswap-inference) — Atomic model swapping
- [oxide-checkpoint](https://github.com/SuperInstance/oxide-checkpoint) — Kernel execution checkpointing
- [cuda-oxide](https://github.com/SuperInstance/cuda-oxide) — The full Flux→PTX compiler

## Open Questions

1. Can firmware swap time reach <1 second for real-time control?
2. Can multiple skills coexist on one ESP32 via FreeRTOS task swapping?
3. How does the ESP32 report structured results back to the agent?
4. Can ESP32s cache multiple firmware images and self-swap autonomously?

## Credits

Forked from [bharanidharanrangaraj/ESP-Flasher](https://github.com/bharanidharanrangaraj/ESP-Flasher).

## License

See upstream repository.
