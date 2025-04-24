#  SRAM in Caravel

##  Overview

Caravel includes two primary SRAM memory blocks to support embedded system operations:
1. **Management Area SRAM**
2. **Storage Area SRAM**

These SRAM modules are integral to enabling both the **management SoC** and **user project** areas to perform memory-based tasks efficiently.

---

##  1. Management Area SRAM

- **Size**: 256 words × 32 bits  
- **Base Address**: `0x0000_0000`
- **Purpose**:  
  Acts as the primary local memory for the management core (a small embedded RISC-V SoC inside Caravel). It is used to store critical configuration, runtime variables, or temporary code during system operation.

---

## 🗃️ 2. Storage Area SRAM

- **Purpose**: Serves as auxiliary memory available to both:
  - The **management SoC**
  - The **user project area**
- **Access Method**: Through the **Wishbone bus interface**
- **Power Domain**: Connected to **User Area 2** power supply
- **Implication**: Considered part of the **user project area** but is shared and accessible by the management SoC as needed.
- **Use Case**: This SRAM is typically used for:
  - Large temporary data buffering
  - Shared memory for inter-module communication
  - Project-specific variables or runtime data

---

##  Technical Integration

- The Wishbone interface acts as the main communication bridge for reading and writing to storage SRAM.
- Users can customize SRAM usage depending on the requirements of their project.
- The design assumes the developer might map additional SRAM or memory peripherals in future Caravel derivatives.

---

##  Source Code References

The SRAM modules and Wishbone interfaces can be explored in the [Caravel GitHub repository](https://github.com/efabless/caravel):

- SRAM control logic: `verilog/dv/caravel/mgmt_soc/sram_ro`
- Wishbone interface: `verilog/dv/wb_utests`
- Management SoC memory mapping: `verilog/gl`

---

##  To-Do (for Custom SCL180 SRAM)

If you're planning to integrate a **custom SRAM in SCL180 technology**:
- Create a compatible **Verilog model** or macro for simulation.
- Ensure it connects to the existing Wishbone bus or your custom interface.
- Power domain compatibility with **User Area 2** must be ensured.
- Perform proper DRC/LVS checks using the SCL180 PDK.

---

##  Credits

- Based on official documentation from [efabless/caravel](https://github.com/efabless/caravel)
