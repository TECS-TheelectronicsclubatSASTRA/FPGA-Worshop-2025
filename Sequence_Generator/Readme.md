# 🔁 D Flip-Flop Based Binary Logic (Verilog)

This project showcases a digital logic circuit constructed from interconnected **D Flip-Flops (DFFs)** to generate a unique binary output pattern based on custom feedback logic. It's an excellent demonstration of **sequential logic design** using Verilog.

---

## 📦 Project Structure

### 🔧 Modules

#### ✅ `DFF` – D Flip-Flop with Asynchronous Reset

A basic positive-edge triggered D Flip-Flop.

| Port | Direction | Width | Description                     |
|------|-----------|-------|---------------------------------|
| `D`  | Input     | 1-bit | Data input                      |
| `clk`| Input     | 1-bit | Clock signal                    |
| `rst`| Input     | 1-bit | Asynchronous reset (active-high)|
| `Q`  | Output    | 1-bit | Output                          |

---

#### ✅ `bday` – Binary Sequence Generator

A 4-bit binary output module composed of 4 D Flip-Flops with custom input logic and feedback paths.

| Port | Direction | Width | Description            |
|------|-----------|-------|------------------------|
| `clk`| Input     | 1-bit | System clock           |
| `rst`| Input     | 1-bit | Asynchronous reset     |
| `o`  | Output    | 4-bit | Binary output          |

**Logic Design:**

- Four flip-flops (`qa`, `qb`, `qc`, `qd`)
- Feedback logic:
  - `DFF1` input = constant `0`
  - `DFF2` input = `~qd`
  - `DFF3` input = constant `1`
  - `DFF4` input = `qb`
- Combined output: `{qa, qb, qc, qd}`

---

## 🧪 Testbench: `tb_bday`

Simulates the behavior of the `bday` module.

### 🕒 Clock & Reset

- Clock toggles every 10 ns (period = 20 ns)
- Reset (`rst`) is asserted for the first 20 ns, then released
- Simulation runs for 200 ns to observe output pattern

---

## 🖥 Example Usage

```verilog
bday uut (
    .clk(clk),
    .rst(rst),
    .o(o)
);
