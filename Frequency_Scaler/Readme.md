# Frequency Divider (50 MHz to 1 MHz)

This Verilog module implements a **frequency divider** that converts a 50 MHz input clock into a 1 MHz output clock signal. It uses a simple counter-based method to toggle the output signal every 25 clock cycles of the input.

---

## ⚙️ Module: `freq`

### 🔧 Ports

| Signal       | Direction | Width | Description                        |
|--------------|-----------|-------|------------------------------------|
| `clk_50MHz`  | Input     | 1-bit | System input clock (50 MHz)        |
| `clk_1MHz`   | Output    | 1-bit | Derived output clock (1 MHz)       |

---

## 📐 Functionality

- The module uses a 26-bit counter to count up to 50 million cycles of the 50 MHz clock.
- For the **first 25 million** cycles, `clk_1MHz` is held HIGH.
- For the **next 25 million** cycles, `clk_1MHz` is held LOW.
- This generates a square wave with a period of 50 µs (1 MHz frequency).

### ⏱ Timing

- Input clock frequency: 50 MHz (20 ns period)
- Counter max value: 49,999,999
- Output clock toggles every 25,000,000 cycles → 1 MHz (500 ns high, 500 ns low)

---

## 🧠 Implementation Notes

- Uses a 26-bit counter to count up to 50 million.
- `clk_1MHz` is initially set to `1` in an `initial` block.
- Output is updated on every rising edge of the input clock.
- The output is a **50% duty cycle** square wave.

---

## 🔁 Example Waveform

| Time (ns) | `clk_50MHz` | `counter` | `clk_1MHz` |
|-----------|-------------|-----------|------------|
| 0         | ↑           | 0         | 1          |
| ...       | ...         | ...       | ...        |
| 500,000   | ↑           | 25M       | 0          |
| 1,000,000 | ↑           | 50M       | 1 (reset)  |

---


