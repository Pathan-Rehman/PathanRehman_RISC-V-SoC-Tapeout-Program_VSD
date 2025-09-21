## Summary

This session introduces **logic synthesis** using the Yosys synthesizer tool. It explains the overall flow from RTL (Register Transfer Level) design to generating a netlist in terms of standard cells using a .lib (library) file. The process, verification methodology, and rationale behind standard cell library variations are discussed, along with detailed steps and concepts pertinent to both theoretical and practical aspects of logic synthesis.

## Core Concepts

### 1. **RTL Design**
- **RTL (Register Transfer Level)** describes digital circuits behaviorally, typically using Hardware Description Languages (HDL) like Verilog.
- RTL represents the functionality and intended operation without specifying gate-level hardware.

### 2. **Netlist**
- A **netlist** is a structural representation of the design mapped to gates and cells, expressed using standard cells from a library.
- The synthesis process converts RTL to this netlist format.

### 3. **.lib Library File**
- **.lib** is a standard cell library file describing logical cells like AND, OR, NOT, and variants (e.g., 2-input, 3-input, fast, slow gates).
- Libraries contain multiple flavors of each cell to meet differing performance and timing constraints.

### 4. **Synthesis Flow**
- The steps include:
  - Reading the Verilog RTL source.
  - Reading the .lib standard cell library.
  - Applying synthesis constraints (e.g., timing requirements).
  - Generating the netlist by mapping RTL to standard cells.

### 5. **Timing Concepts**
- **Setup Time:** The minimum period before a clock edge that data must be stable for a flip-flop to correctly register it.
- **Hold Time:** The minimum period after a clock edge during which data must remain stable.
- **Propagation Delay:** Time taken for changes at input of a gate or flip-flop to affect its output.

### 6. **Need for Cell Variants**
- Fast cells reduce delay but increase area and power; slow cells increase delay but save area and power.
- A mix of cells is needed—fast for meeting setup time (maximum frequency), slow for preventing hold violations.

### 7. **Constraints**
- Synthesis tools use constraints to balance speed, area, power, and timing (setup and hold) in cell selection.

### 8. **Verification**
- Synthesis verification involves functionally simulating the netlist with the **same testbench** used for the RTL.
- The outputs from netlist simulation (using tools like IVerilog) must match RTL simulation outputs, viewable using waveform viewers such as GTKWave.

## Lab Steps

### 1. Prepare Your Design

- Have your RTL code written in Verilog (e.g., `design.v`).
- Ensure you have access to the relevant standard cell library (`cells.lib`).

### 2. Launch USYS Synthesizer

1. **Read the RTL Design File**
   
   ```tcl
   read_verilog design.v
   ```
   ![PLACEHOLDER: Terminal reading RTL Verilog file]

2. **Read the .lib Standard Cell Library**
   
   ```tcl
   read_liberty cells.lib
   ```
   ![PLACEHOLDER: Terminal reading .lib standard cell library]

3. **Apply Synthesis (if needed, specify top module and constraints)**
   
   ```tcl
   # Optionally, set top module and timing constraints
   synth -top <module_name> -constr constraints.sdc
   ```
   ![PLACEHOLDER: Synthesizer interface before synthesis]

4. **Write Out the Netlist**
   
   ```tcl
   write_verilog synthesized_netlist.v
   ```
   ![PLACEHOLDER: Synthesis completed, netlist generated]

### 3. Verify Synthesis

1. **Simulate the Synthesized Netlist**
   
   - Use **the same testbench as for RTL**, for example (`testbench.v`):
   
   ```shell
   iverilog -o sim_out testbench.v synthesized_netlist.v
   ./sim_out
   ```
   ![PLACEHOLDER: IVerilog simulation terminal output]

2. **View Waveforms for Output Comparison**
   
   - Generate a **VCD** (Value Change Dump) file with IVerilog.
   - Open the VCD in **GTKWave** for analysis:
   
   ```shell
   gtkwave dump.vcd
   ```
   ![PLACEHOLDER: GTKWave waveform viewer with simulation output]

3. **Compare Results**
   
   - Confirm that the **outputs and stimulus from synthesized netlist simulation match those from original RTL simulation**.
   - Any mismatches may indicate synthesis errors or issues.
   ![PLACEHOLDER: Side-by-side waveform comparison]

### 4. Detailed Flow Illustration

- **RTL Design → Synthesis Tool (USYS) + .lib Library → Gate-Level Netlist**  
  ![PLACEHOLDER: Schematic flow from RTL to netlist using standard cells]

- In the netlist, **primary inputs and outputs remain identical to RTL design**, maintaining testbench compatibility.

### 5. Additional Notes

- **Area and Power Trade-Offs:**
  - Fast cells use wider transistors (low delay, high area/power).
  - Slow cells use narrower transistors (higher delay, low area/power).
- **Guidance to Synthesizer:**
  - Use synthesis constraints to fine-tune which cell flavors are chosen based on desired trade-offs (timing, area, power).
- **Cell Selection & Optimization:**
  - The tool automatically selects a mix of cells to satisfy constraints while optimizing design performance.

---

This documentation outlines the theory, rationale, and practical steps to perform logic synthesis using a synthesizer like USYS, including how to verify correctness with simulation outputs.
