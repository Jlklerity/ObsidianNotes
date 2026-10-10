# Notes Gap Report — CSD2182 Lectures 1–4
*Generated 2026-09-08. Compares your Obsidian vault against the four lecture PDFs.*

## How to read this

Four verdicts are used:

- **Written** — you have a note with your own text explaining it.
- **Screenshot only** — a note exists but contains only a pasted slide image. The slide content is technically in your vault, but you have not restated it. For recall practice this counts as not yet learned.
- **Stub** — a note file exists but is empty (0 bytes) or is a heading with nothing under it.
- **Missing** — no note at all.

A structural point before the details: **26 of your 32 notes rely on pasted slide screenshots, and 8 of those contain no prose at all.** Screenshots are fine as a reference but they do not test recall. The gaps flagged as "Screenshot only" are the cheapest wins — the material is already in front of you, it just needs restating.

Also note: `OS_Services_and_Processes_Summary.md` in your week-2 folder is a slide transcription, not vault notes. It is not part of your Obsidian graph and nothing in it is linked. It duplicates the slides rather than compressing them.

---

## Lecture 1 — Introduction

### Written
| Topic | Note |
|---|---|
| Purpose / role of the OS as intermediary | `Purpose of the Operating System` |
| Bootstrap program, where it lives, what it must do | `Bootstrap Program` |
| Boot chain (Power-on → BIOS/POST → MBR → bootloader → kernel) | `Boot Sequence` |
| Storage hierarchy + locality principle | `Storage Hierarchy` |
| SPOOLing definition and purpose | `SPOOLing(...)` |

### Screenshot only
| Topic | Note | What you haven't written |
|---|---|---|
| Computer System Organization | `Computer System Organization` | CPUs and device controllers share a common bus to shared memory; CPU and devices execute **concurrently and compete for memory cycles** |
| Von Neumann Model | `Von Neumann Model` | Stored-program concept — instructions and data in the same memory |
| Fetch–Decode–Execute–Writeback | `Execution of CPU Instruction` | The role of PC, Instruction Register, instruction decoder, ALU at each of the 4 steps |
| ELF object file format | `ELF Object File Format` | Every section's meaning — see gap list below |

### Missing
**OS structure and definition**
- The four-layer computer system structure: hardware → OS → application programs → users.
- Formal OS definition: the kernel is *"the one program running at all times"*; everything else is a **system program** (ships with OS, not kernel) or an **application program**. Your `System Program` and `Application Program` notes are empty stubs — this is the definition they need.
- **Middleware** — software frameworks (databases, multimedia, graphics) provided by modern general-purpose and mobile OSes. Not mentioned anywhere in your vault.
- OS goals stated explicitly: execute user programs / make the system convenient / **use hardware efficiently**. *(The take-home quiz asks "in the context of OS goals, what does efficiency refer to?")*

**Storage structure** (distinct from the hierarchy note you have)
- Main memory: the only large storage the CPU can access **directly**; random access; **volatile**; typically DRAM.
- Secondary storage as a non-volatile extension of main memory.
- HDD internals: platters, **tracks subdivided into sectors**, the disk controller's role.
- NVM devices — faster than HDD, non-volatile, displacing disks as price drops.
- The "Characteristics of Various Types of Storage" table, and which level is managed by whom — **registers are managed by the compiler**, cache by hardware, main memory by the OS. *(Directly asked in the take-home quiz.)*
- **Caching as a general principle**: performed at many levels; check faster storage first; cache is smaller than what it caches; cache size and replacement policy are the design problems.
- Device driver as the **uniform interface between controller and kernel**.

**Program execution and loading** — this is your largest Lecture 1 blind spot
- The four stages: compile/interpret → **load** → execute → terminate (control returns to the OS).
- The open questions loading must answer: where in memory does the program go, which address holds the first instruction, how much memory to reserve, what about stack and heap.
- **The loader**: reads the executable format, copies text and data segments to the right addresses, allocates stack and heap, sets the PC to the entry point.
- The chicken-and-egg problem — who loads the loader — which is why the boot sequence matters.
- ELF sections in detail: `.text` (code), `.rodata` (read-only: jump tables), `.data` (initialised globals), **`.bss`** (uninitialised globals — "Block Started by Symbol" / "Better Save Space"; has a section header but **occupies no file space**), `.symtab`, `.rel.text`, `.rel.data`, `.debug`, plus the ELF header, segment header table and section header table.
- **Segments vs sections**: segments carry what is needed for *runtime execution*; sections carry data for *linking and relocation*. *(The quiz asks which component holds relocation info for instructions → `.rel.text`.)*
- The `readelf -h / -S / -l` and `objdump -D / -s -j .data / -x` demo commands, and the `week1demo` folder in your week-1 directory — you have the sample code but no note on it.

**Boot sequence details missing from your existing note**
- Bootstrap loader / BIOS is stored in **ROM or EEPROM**.
- Sometimes a **two-step** process: ROM loads a boot block at a fixed location, which loads the bootstrap loader from disk.
- **UEFI** replaces BIOS on modern systems.
- **GRUB** as a common bootstrap loader — selects kernel from multiple disks, versions, options.
- Boot states such as **single-user mode**.
- BIOS is memory-mapped at `FFFFFFF0h`; MBR is the **first sector, 512 bytes**; **chain-loading** (MBR loads further bootloaders).
- **Why BIOS is required**: hardware initialisation, bootstrap loading, system configuration, legacy support, system management.
- **System daemons** — services started by the kernel after it loads, running outside the kernel.

**The OS responsibility list — entirely absent from your vault (~12 slides)**
- Process Management: process = program in execution; program is **passive**, process is **active**. Activities: create/delete processes, suspend/resume, synchronisation, communication, deadlock handling.
- Memory Management: instructions and data must be in memory to execute; track what's in memory and by whom, decide what moves in/out, allocate and deallocate.
- File-system Management: uniform logical view, file as the logical storage unit, directories, access control, mapping files onto secondary storage, backup.
- Mass-storage Management: mounting/unmounting, free-space management, storage allocation, disk scheduling, partitioning, protection.
- I/O Subsystem: **buffering vs caching vs spooling** distinguished, general device-driver interface, device-specific drivers.
- Protection vs Security: protection = controlling access to resources; security = defence against internal/external attack. User IDs, group IDs, **privilege escalation**.
- Virtualization: **emulation** (different source/target CPU, slowest) vs **virtualization** (guest natively compiled); VMM; host vs native VMM.
- Portability, and the API/abstraction argument for why an OS exists.

**Multiprogramming background**
- Overlapped I/O — the card-reader/printer vs tape-drive timeline.
- Tapes vs disks: sequential vs random access.
- Spooling **leads to multiprogramming** (multiple programs on one CPU) — your SPOOLing note mentions multiprogramming but not this causal link.
- Print spooling specifics: the spooler process feeds the printer at its own rate while other processes carry on.

---

## Lecture 2 — Hardware Support for OS

This is your strongest lecture. Interrupts, IVT/IDT/IDTR, DMA, dual-mode and the timer are genuinely well covered.

### Written
`Interrupt` · `ISR(Interrupt Service Routine)` · `Interrupt Vector Table` · `Interrupt Descriptor Table(IDT)` · `Interrupt Descriptor Table Register(IDTR)` · `IDT vs IVT` (your best note) · `DMA(Direct Memory Access)` · `Cycle Stealing` · `Timer` · `Trap vs Abort` · `Dual-Mode Operation` · `CPU Privileged Modes` · `Status Register` · `Workings of an IO Operation`

### Screenshot only
| Topic | Note | What you haven't written |
|---|---|---|
| Interrupt handling flow + HW setup | `Interrupt Handling` | The **IF (Interrupt Flag)** and **IV (Interrupt Vector)** registers, and where the IF check sits in the fetch-decode-execute-writeback loop |
| The three interrupt categories | `3 Types of Interrupts` | Headings for Hardware / Software / Exceptions exist with **nothing under them** |
| Intel Pentium event-vector table | `Event-Vector Table` | Which vector numbers map to which exceptions |
| Synchronous vs asynchronous I/O | `Synchronous vs Asynchronous IO` | The behavioural difference, not just the diagram |
| Privileged instruction set | `CPU Privileged Modes` | Which instructions are privileged vs not — listed below |

### Missing
**CPU → I/O direction**
- **Special I/O instructions / port-mapped I/O**: separate address spaces for memory and I/O devices; Intel `IN`/`OUT` moving data between I/O ports and EAX/AX/AL; `INS`/`OUTS` block instructions moving blocks between ports and memory. Your canvas has a "Port-Mapped I/O" card but no note.
- **Memory-mapped I/O**: device data and command registers mapped into the processor address space; used especially for large address spaces such as graphics; accessed with ordinary `MOV`. *(Quiz question.)*
- **Polling** (`while (done_bit == 0);`): pro — fast response time for the waiting program; con — **low CPU utilisation**. *(Quiz asks the main disadvantage of software polling.)*

**Interrupts**
- **Maskable vs non-maskable** hardware interrupts ("maskable" = can be turned off).
- **Faults** as the third exception category — recoverable: page fault, division by zero, illegal instruction. Your `Trap vs Abort` note covers two of the three; fault is the one being tested against them.
- **Interrupt priority**: an interrupt handler can itself be interrupted by a higher-priority interrupt.
- Interrupt architecture must **save the address of the interrupted instruction**.
- "An operating system is **interrupt driven**" — stated as a principle.
- Multi-CPU systems can process interrupts concurrently if the OS is designed for it.

**DMA**
- The **DMA command block** the OS writes into memory: source and destination addresses, read/write mode, byte count; then the location of the command block is written to the DMA controller; the controller interrupts on completion.
- The motivating scenario (copying 1 KB from disk one byte at a time, one interrupt per byte) — the *why* behind DMA.
- DMA reduces the **number of interrupts** and allows CPU processing in parallel with device-to-memory transfer.

**I/O structure**
- The two methods stated formally: control returns to the user program only on I/O completion, vs control returns immediately.
- Blocking case: `wait` instruction idles the CPU until the next interrupt; wait loop causes memory-access contention; **at most one I/O request outstanding at a time**.
- Non-blocking case: system call to wait for completion; the **device-status table** — one entry per device holding type, address and state; the OS indexes into it to find status and record the interrupt. *(Quiz: "in an asynchronous I/O structure, what happens after a user program initiates an I/O request?")*

**Protection**
- Why a user program cannot touch a device directly: it goes through the device driver via `open()`, `read()`, `write()`; prevents access-control violations; erroneous direct use crashes the system.
- How the mode bit is protected: a **system call changes the mode to kernel, and returning from it resets the mode to user** — the user cannot set the bit itself. Your `Dual-Mode Operation` note states the mode bit exists but not this guarantee.
- The explicit privileged / non-privileged instruction split:
  - **Privileged**: change IDTR, I/O instructions, halt, turn off interrupts, set the timer, context switching, clear memory, remove a process from memory, modify device-status table entries.
  - **Not privileged**: add, sub, read processor status, read system time, generate a trap, send final printout to printer.

### Empty stub files to fill or delete
`Application Program` · `CPU to Memory` · `Local Buffer Storage` · `Special Purpose Registers` · `System Program`

`Local Buffer Storage` in particular is load-bearing for Lecture 2: each device controller has a **local buffer**; I/O goes device → controller's local buffer; the CPU moves data between main memory and that buffer; the controller signals completion by raising an interrupt.

---

## Lecture 3 — OS Services

**Nothing in the vault.** `OS Services & Processes.canvas` is an empty file. Full inventory of what to note:

1. **A view of OS services** — the layered diagram: user/system programs → user interfaces (GUI, touchscreen, CLI) → system calls → services (program execution, I/O, file systems, communication, resource allocation, accounting, error detection, protection & security) → OS → hardware.
2. **CLI / shell** — direct command entry; kernel-resident or a system program; multiple shells; built-in commands vs names of programs, and why the latter means new features don't require modifying the shell.
3. **GUI** — desktop metaphor, icons, invented at Xerox PARC; Windows = GUI + CLI shell, macOS = Aqua over a UNIX kernel, Linux = CLI + optional CDE/KDE/GNOME.
4. **Touchscreen interfaces** — gestures, virtual keyboard, voice.
5. **System calls** — the programming interface to OS services; usually reached via an **API** rather than directly; Win32 / POSIX / Java as the three common APIs.
6. **System call implementation** — each call has a **number**; the system-call interface keeps a table indexed by number; the caller needs to know only the API, not the implementation; the run-time support library bridges them.
7. **Parameter passing — three methods**: registers (limited count); a **block/table in memory** with its address passed in a register (Linux, Solaris); pushed on the **stack**. Block and stack methods don't limit parameter count or length.
8. **Invoking OS services mechanically** — `int 0x80` software interrupt (`80h` = the system-call vector), `iret` to return; `sysenter`/`sysexit`; `syscall`.
9. **The x86 assembly `write()` example** — `eax` = call number, `ebx` = file descriptor, `ecx` = buffer pointer, `edx` = length, `int 0x80` triggers the user→kernel transition; then `eax = 1` for `sys_exit`.
10. **The six types of system call** — process control, file management, device management, information maintenance, communications, protection. Learn representative calls in each.
11. **Windows vs UNIX system call comparison** table.
12. **Standard C library example** — `printf()` calling `write()`.
13. **System services / system programs** — file manipulation, status information (including the **registry**), file modification, programming-language support, program loading and execution, communications, **background services (daemons — launch at boot, run in user context not kernel context)**, application programs. Key idea: most users' view of the OS is defined by system programs, not system calls.
14. **Linkers and loaders** — the compile → object file → link → executable → load pipeline; **relocatable** object files; relocation assigns final addresses; **dynamically linked libraries (DLLs)** loaded as needed and shared. This directly extends the Lecture 1 loader material you're also missing.
15. **Why applications are OS-specific** — different system calls and file formats; three routes to multi-OS (interpreted language, VM/Java, recompile standard C); **ABI** as the binary-level equivalent of an API.
16. **OS structure — the five designs**, which is the stated exam objective for this lecture:
    - **Simple / MS-DOS** — single-tasking, single memory space, shell reloaded on program exit.
    - **Monolithic / original UNIX** — system programs + kernel; kernel is everything below the system-call interface and above the hardware.
    - **Layered** — layer 0 = hardware, layer N = user interface; each layer uses only lower layers.
    - **Microkernel (Mach)** — minimal kernel, message passing between user modules. Benefits: extensible, portable, more reliable, more secure. Detriment: **user↔kernel communication overhead**.
    - **Modules (LKMs)** — object-oriented, loadable as needed, more flexible than layers.
    - **Hybrid** — Linux/Solaris monolithic + modular; Windows monolithic + microkernel subsystems; macOS Mach + BSD + I/O Kit + kernel extensions.

---

## Lecture 4 — Processes

**Nothing in the vault.** Full inventory:

1. **Process concept** — a program in execution, progressing **sequentially** (no parallel execution within a single process). Its parts: **text** (code), current activity (PC + registers), **stack** (parameters, return addresses, locals), **data** (globals), **heap** (dynamic allocation).
2. **Program vs process** — program is a passive file on disk; process is active; a program becomes a process when loaded into memory; **one program can be several processes**.
3. **Process in memory / memory layout of a C program** — the low→high arrangement of text, data, heap, stack. This connects directly to the ELF material in Lecture 1.
4. **Snapshot view** — what a running process is actually using: CPU registers (PC, SP, GPRs, FPRs, status flags) and memory.
5. **Context of a process** — **registers only**. The reasoning matters: ALU and control unit are treated as black boxes, registers are their inputs, so restoring the same register values guarantees the same behaviour; memory is handled by memory management.
6. **HW context saving** — automatic, no instructions involved; hardware must save at least PC and SP (it is too late for the ISR to do it); saved to the stack via SP; restoring is the reverse.
7. **SW context saving** — usually the first thing an ISR does, because hardware doesn't save everything. x86-64 hardware saves only RIP/EIP, CS, RFLAGS, SS and RSP (SS/RSP only on a privilege-level change). SW saving is **selective** (e.g. FPRs saved only if used) whereas HW saving is unconditional.
8. **The full system-call/interrupt timeline** — HW save → SW save → servicing → SW restore → HW restore, with the user/kernel mode band, and the point that **the process resumed may not be the one that was interrupted**.
9. **The five process states** — New, Running, Waiting, Ready, Terminated.
10. **State transitions and their causes** — New→Ready (PCB initialised, memory allocated); Ready→Running (scheduler picks from the ready queue); Running→Ready (interrupt or fault); Running→Waiting (system call, especially I/O or synchronisation); Waiting→Ready (I/O event or signal arrives); Running→Terminated (info kept for a while afterwards — worth answering *why*).
11. **PCB** — per-process data structure, maintained by the OS, **not directly accessible**, usually a linked list. Contents: process state, program counter, CPU registers, scheduling information, memory-management information, accounting information, I/O status information.
12. **Linux `task_struct`** — `pid`, `state`, `time_slice`, `parent`, `children`, `files`, `mm`.
13. **Threads** — multiple program counters per process; PCB must store per-thread detail.
14. **Context switch** — save old state, load new state via the PCB; **pure overhead**, no useful work done; the more complex the OS and PCB, the longer the switch; some hardware provides multiple register sets to speed it up.
15. **Process scheduling** — goal is maximising CPU use; **ready queue** vs **wait queues**; processes migrate between them.
16. **Non-preemptive vs preemptive** — non-preemptive: a running process keeps the CPU until it finishes or blocks, even if a higher-priority process arrives. Preemptive: time slices and timer interrupts let the OS take the CPU back. (Links to your `Timer` note.)
17. **Scheduling opportunities** — the five transition points, and which of them only create an opportunity under **preemptive** scheduling (Waiting→Ready and New→Ready).
18. **Round-robin** — fixed time quantum, circular order, preempt and requeue at the back if the burst exceeds the quantum, immediate switch if it finishes early.
19. **Process creation** — parent/child tree, **pid**; resource-sharing options (all / subset / none); execution options (concurrent, or parent waits); address-space options (child is a duplicate, or a new program is loaded).
20. **`fork()`** — creates an exact replica (same memory contents, files) with a **different pid and different return value**; the memory diagrams showing two PCBs and two identical address spaces.
21. **`exec()`** — replaces the process image with a new program *in the same process*; the `execve` front ends and the **suffix conventions**: `l` = argument list, `v` = argument vector, `p` = search `$PATH`, `e` = custom environment. By convention the first argument is the filename.
22. **Windows creation** — `CreateProcess()` does both creation and program loading in one API (contrast with fork+exec); `WaitForSingleObject()` / `WaitForMultipleObjects()`.
23. **Process termination** — `exit()` returns status to the parent via `wait()`; the OS deallocates resources; `abort()` for a parent killing a child, and the three reasons; **cascading termination**; **zombie** (no parent waiting) vs **orphan** (parent terminated without waiting).
24. **Foreground vs background processes.**

---

## Cross-check against the take-home quiz

The quiz draws only on Lectures 1–2. Of its 15 questions, these hit topics you currently have **no written note** for:

- ELF component holding relocation info for instructions → `.rel.text`
- Storage hierarchy level managed by the **compiler** → registers
- What **efficiency** means among the OS goals
- How the CPU communicates with a controller under **memory-mapped I/O**
- Main disadvantage of **software polling**

The other ten map onto notes you already have (spooling, boot sequence, status register done/error bit, timer, cycle stealing, IVT vs IDT location, ISR address lookup, trap vs abort, mode bit, asynchronous I/O).

---

## Suggested order of work

1. Fill the five empty stubs — cheapest, and `Local Buffer Storage` is quiz-adjacent.
2. Convert the "screenshot only" notes to prose, especially `3 Types of Interrupts` (add maskable/non-maskable and **faults**) and `Execution of CPU Instruction`.
3. Close the five quiz-relevant Lecture 1–2 gaps listed above.
4. Write the Lecture 1 OS-responsibilities set (process/memory/file-system/mass-storage/caching/I-O/protection/virtualization) — the largest single block missing.
5. Write the loader and ELF-section material, then start Lecture 3, since linkers and loaders continue that thread.
6. Lecture 4 last — it depends on the interrupt and context material you already know well.
