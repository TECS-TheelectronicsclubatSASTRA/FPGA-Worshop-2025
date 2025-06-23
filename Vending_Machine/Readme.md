# Vending Machine (Verilog)

This project implements a simple FSM (Finite State Machine) based **vending machine** using Verilog HDL. The vending machine accepts specific denominations and dispenses products based on total inserted amount and a selection input.

---

## 💡 Features

- Accepts money in denominations:
  - `00`: ₹5
  - `01`: ₹10
  - `10`: ₹20
- Offers 4 product choices:
  - `00`: Product A (₹20)
  - `01`: Product B (₹30)
  - `10`: Product C (₹35)
  - `11`: Product D (₹40)
- Displays product codes using four 7-segment outputs (`m1`, `m2`, `m3`, `m4`)
- Handles reset (`rst`) and deactivation (`de`) inputs

---

## 🔌 Inputs

| Signal | Width | Description                          |
|--------|-------|--------------------------------------|
| `clk`  | 1-bit | Clock signal                         |
| `rst`  | 1-bit | Active-low reset                     |
| `de`   | 1-bit | Deactivation input                   |
| `amt`  | 2-bit | Amount inserted (₹5/₹10/₹20)         |
| `cho`  | 2-bit | Product selection (00 to 11)         |

---

## 💡 Outputs

| Signal | Width | Description                           |
|--------|-------|---------------------------------------|
| `m1`   | 7-bit | 7-segment output for digit 1          |
| `m2`   | 7-bit | 7-segment output for digit 2          |
| `m3`   | 7-bit | 7-segment output for digit 3          |
| `m4`   | 7-bit | 7-segment output for digit 4          |

---

## 🔄 FSM States

| State  | Description | Total Amount |
|--------|-------------|--------------|
| `ideal` | Idle       | ₹0           |
| `r5`    | Step 1     | ₹5           |
| `r10`   | Step 2     | ₹10          |
| `r15`   | Step 3     | ₹15          |
| `r20`   | Step 4     | ₹20          |
| `r25`   | Step 5     | ₹25          |
| `r30`   | Step 6     | ₹30          |
| `r35`   | Step 7     | ₹35          |
| `r40`   | Step 8     | ₹40          |

---

## 📟 Product Display Encoding (7-segment)

| Product | Price | `cho` | Display (`m1` to `m4`)                         |
|---------|--------|-------|------------------------------------------------|
| A       | ₹20    | `00`  | `0001000`, `1000000`, `0010010`, `0000110`     |
| B       | ₹30    | `01`  | `1001111`, `1000110`, `0000100`, `1111111`     |
| C       | ₹35    | `10`  | `1000000`, `0001000`, `0000010`, `1000000`     |
| D       | ₹40    | `11`  | `0000111`, `0000110`, `0001000`, `1111111`     |

> ⚠️ Default output when idle/reset: `1111111` (all segments off)

---

## 🧪 Usage Example

1. Insert ₹10 (`amt = 01`)
2. Insert another ₹10 (`amt = 01`) → total = ₹20
3. Select Product A (`cho = 00`)
4. Product is displayed
5. Apply reset (`rst = 0`) → returns to idle

---



