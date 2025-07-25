# Pulse Width Modulation (PWM) using Verilog

This Verilog module generates a **1 Hz clock signal** and a **PWM (Pulse Width Modulation) signal** from a 50 MHz input clock. It demonstrates basic digital control of output signal duty cycle using a fixed pulse width parameter.

---

## 🔧 Module: `pwm`

### 📥 Inputs

| Signal       | Width | Description                      |
|--------------|-------|----------------------------------|
| `clk_50MHz`  | 1-bit | System input clock (50 MHz)      |

### 📤 Outputs

| Signal       | Width | Description                                 |
|--------------|-------|---------------------------------------------|
| `clk_1Hz`    | 1-bit | Clock output signal at 1 Hz                 |
| `pwm_signal` | 1-bit | PWM signal with adjustable duty cycle       |

---

## ⚙️ Functionality

- A **1 Hz clock** is generated by dividing the 50 MHz input.
  - HIGH for 25 million cycles (0.5s)
  - LOW for 25 million cycles (0.5s)
- A **PWM signal** is also generated by comparing a duty counter to a set value derived from `pulse_width`.

---

## 🔢 Parameters

- `pulse_width` (internal, default = `4'd1`) determines the **duty cycle** of the PWM signal.
- Formula:  
  `duty_cycle = pulse_width × 2,500,000`  
  (i.e. each unit of `pulse_width` = 5% duty in a 1 Hz period)

### Duty Cycle Table

| `pulse_width` | Duty Cycle (%) |
|---------------|----------------|
| 1             | 5%             |
| 2             | 10%            |
| 5             | 25%            |
| 10            | 50%            |
| 15            | 75%            |

---

## 📈 Timing

- The `counter` counts from 0 to 49,999,999 (1 second at 50 MHz).
- The `clk_1Hz` signal is HIGH for the first 25M cycles and LOW for the next 25M.
- The `pwm_signal` is HIGH while `counter < duty_cycle`, otherwise LOW.

---

## 🧪 Example Behavior

If `pulse_width = 4'd10`, then:

- `duty_cycle = 10 × 2,500,000 = 25,000,000`
- `pwm_signal` is HIGH for the first half of the 1 Hz period (50% duty)

---

## 📝 Notes

- `pulse_width` is currently **hardcoded** to 1. To make it configurable, uncomment the input line and remove the hardcoded assignment.
- No asynchronous reset is used. If required, it can be added to ensure safe startup.

---


