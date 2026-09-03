
| **Feature**              | **Interrupt Vector Table (IVT)**                                    | **Interrupt Descriptor Table (IDT)**                                                                  |
| ------------------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **CPU Mode**             | **Real Mode** (16-bit legacy)                                       | **Protected Mode** (32-bit) & **Long Mode** (64-bit)                                                  |
| **Memory Location**      | **Fixed / Hardcoded** at physical memory `0x0000` to `0x03FF`       | **Dynamic** anywhere in RAM; tracked by the **IDTR** register                                         |
| **Entry Contents**       | Raw **Function Pointers** (4 bytes: 16-bit segment + 16-bit offset) | **Gate Descriptors** (8 or 16 bytes: target offset, segment selector, privilege level/DPL, gate type) |
| **Security & Privilege** | None (direct real-mode addresses, no privilege checks)              | Enforces privilege checks (DPL/CPL) before transferring execution to the ISR                          |
| **Addressing Formula**   | $\text{Vector } N \times 4$                                         | $\text{Base Address} + (\text{Vector } N \times 8)$ _(or $\times 16$ in 64-bit)_                      |
