# Accuracy Audit — Lectures 1 & 2
*Generated 2026-09-08. Companion to `_Notes Gap Report (Lectures 1-4).md`, which covers completeness. This one checks whether what you already wrote is **correct**.*

Verdict up front: **most of your prose is accurate.** `Cycle Stealing`, `Timer`, `ISR`, `Interrupt`, `Status Register`, `Workings of an IO Operation` and `IDT vs IVT` are all sound. Seven items need attention — five are genuine errors or misleading phrasings, one is an omission that changes meaning, and one is a case where **your note is right and the slide is wrong**.

Corrections are stated, then followed by a check question. Answer the check question from memory before you edit the note — if you can't, the correction hasn't landed yet.

---

## A. Genuine errors

### A1. `CPU Privileged Modes` — the model is backwards
> Your note: *"Depending on which mode is being used (User/Kernel), each mode has their own privilege instructions"*

This describes two parallel sets of privileged instructions, one per mode. That isn't the architecture.

There is **one** instruction set supported by the CPU, partitioned into two groups:
- **Privileged instructions** — executable **only** in kernel mode. Attempting one in user mode raises an exception.
- **Other instructions** — executable in **both** modes.

Kernel mode doesn't have "its own" privileged instructions; it has *access to* the privileged subset. User mode has no privileged instructions of any kind. Look again at the slide diagram — the box labelled "Set of instructions supported by the CPU" contains both groups, and the mode determines which group you may reach, not which set exists.

This matters because the whole protection argument depends on it: if each mode had its own set, there would be nothing to protect.

> **Check:** `HLT` halts the processor. Which group is it in, and what happens if a user program executes it? Then: reading the system time — which group, and why is that group's membership decided on *safety* grounds rather than *difficulty* grounds?

---

### A2. `Storage Hierarchy` — locality is the wrong cause
> Your note: *"Based on Locality Principle, the closer the source of memory is to the CPU, the faster it's access time"*

Two separate ideas are fused here, and the causal arrow points the wrong way.

The hierarchy is organised by **speed, cost and volatility** (that is the slide's own list). Registers and cache are fast because they are small, physically close, and expensive per byte — that is physics and economics, not locality. Locality is not why they are fast.

**Locality of reference** is a property of how *programs* access memory: a program tends to reuse recently-touched addresses (temporal locality) and addresses near them (spatial locality). Locality is what makes the hierarchy *worth building* — it is the reason a small fast cache achieves a high hit rate instead of being useless. It explains why caching **works**, not why closer memory is **faster**.

Correct framing: *the hierarchy exists because of speed/cost/volatility trade-offs; caching across that hierarchy is effective because programs exhibit locality.*

> **Check:** if a program accessed memory addresses uniformly at random across a 100 GB working set, would the storage hierarchy still be organised the same way? Would caching still help? Your two answers should differ — explain why.

---

### A3. `Interrupt Vector Table` — the IDTR does not point to the IVT
> Your note: *"IDTR is the Hardware pointer inside the CPU whereas, Interrupt Vector Table (or IDT) is the actual data structure stored in system memory."*

The register/memory distinction you're drawing is exactly right, and it's a good distinction to have made. The problem is the parenthetical **"(or IDT)"**, which treats IVT and IDT as interchangeable — and this sentence sits inside your *Interrupt Vector Table* note, so it reads as "the IDTR locates the IVT."

It doesn't:
- **Real mode → IVT.** Base is **hardcoded at 0x0000**, limit 0x03FF. Nothing points to it; the address is fixed by the architecture. There is no lookup register in play.
- **Protected / long mode → IDT.** Base is **anywhere in RAM**, and the **IDTR** holds base + limit.

The IDTR is the answer to "how does the hardware find the table *when the table can be anywhere*." In real mode that question doesn't arise, which is precisely why no register is needed. Your own `IDT vs IVT` table states this correctly — the contradiction is between two of your notes, so fix this one to match that one.

> **Check:** the take-home quiz asks how the IVT's location is determined in protected mode *compared to* real mode. State both mechanisms in one sentence each, then say which of the two allows the OS to relocate the table at runtime and why that's useful.

---

### A4. `Trap vs Abort` — a taxonomy collapsed into one level
> Your note heads the file with *"Software-generated/CPU-generated interrupts (exceptions)"* and gives *"a system call"* as an example of a **trap**.

The slide uses a **two-level** taxonomy, and your note flattens it:

```
Interrupts
├── Hardware Interrupts        — from I/O devices; maskable or non-maskable
├── Software Interrupts        — a CPU instruction inside a program
│   └── system calls, INT instruction
└── Exceptions (CPU-generated)
    ├── Faults    — recoverable   (page fault, divide by zero, illegal instruction)
    ├── Traps     — intentional   (debugger breakpoints)
    └── Aborts    — severe, unrecoverable (double fault, hardware failure)
```

Three consequences for your note:
1. **"Software-generated" and "CPU-generated" are not synonyms.** Software interrupts come from an instruction the program deliberately executed; exceptions are raised by the CPU in reaction to a condition. Your heading equates them.
2. **A system call is a software interrupt, not a trap**, in this taxonomy. Your note lists it as a trap example. (Be aware: the textbook uses "trap" loosely to include system calls, and the Lecture 2 slide itself says "System Calls (Trap Interrupts)". So both usages appear in your own materials. Note *both*, and know which taxonomy a question is asking about — but keep the three-way Fault/Trap/Abort split clean, because that is the split being examined.)
3. **Faults are missing entirely.** You have two of the three exception types. Fault is the most important one in practice — page faults are how demand paging works, and you will meet them again in the memory-management lectures.

> **Check:** classify each of these into exactly one leaf of the tree above — a divide-by-zero; pressing a key; `int 0x80`; a debugger breakpoint; a double fault. Then: which one is recoverable *by design* such that the faulting instruction is re-executed after handling?

---

### A5. `System Call(Monitor Call)` — circular definition
> Your note: *"Software that triggers an interrupt by executing a special operation called System Call"*

This defines "system call" using the term "system call". It also mislabels the *what*: a system call isn't software, it's a **request**.

A usable definition separates the three layers:
- **What it is** — the programming interface through which a user program requests a service from the OS kernel.
- **Why it's needed** — the requested service requires privileged operations the user program cannot perform itself (see A1).
- **How it's implemented** — by deliberately raising a software interrupt (`int 0x80`), or via dedicated fast instructions (`sysenter`/`syscall`), which switches the mode bit to kernel, runs the handler, and returns to user mode.

"Monitor call" is just the historical name — "monitor" was the early term for the resident kernel. Worth a parenthesis, not a heading.

> **Check:** why can't a user program simply `call` the kernel function directly and skip the interrupt? Your answer should mention both the mode bit and the fact that the user program doesn't know the kernel's addresses.

---

## B. Omissions that change the meaning

### B1. `Bootstrap Program` — "Stored in the ROM"
The slide says **ROM *or EEPROM***. The distinction is not pedantry: EEPROM is electrically erasable, which is what makes firmware **updatable**. A BIOS/UEFI that could never be reflashed would be a genuine design problem. One word, but it's the word that explains why firmware updates exist.

### B2. `Boot Sequence` — chain-loading is optional
Your chain reads *"MBR loads → bootloader loads → OS kernel runs"* as a fixed sequence. The slide says the MBR **may** load boot loaders (chain-loading). The MBR is only 512 bytes — the first sector — which is too small for a full bootloader, so it typically loads a larger one, but a minimal system can be booted from the MBR stage directly.

Also missing from the chain, and quiz-relevant since the quiz asks for the **correct sequence**: BIOS runs **POST** before searching storage for a bootable drive. You have POST in your note; make sure your ordering puts it before the drive search, not after.

---

## C. Where your note is right and the slide is wrong

### C1. `IDT vs IVT` — the entry-size multiplier

Your table gives the IDT addressing formula as **Base + (N × 8)**, and **× 16 in 64-bit**.

The Lecture 2 slide ("How does CPU transfer control to ISR?") gives:
- `Base Address + 8 * N` for 64-bit
- `Base Address + 4 * N` for 32-bit

**You are correct and the slide is wrong**, in both halves. Per the Intel SDM and confirmed against OSDev:
- 32-bit protected mode → IDT gate descriptors are **8 bytes** → `Base + N × 8`
- 64-bit long mode → descriptors are **16 bytes** → `Base + N × 16`

The slide's figures are each half the true value. `4 × N` is the *real-mode IVT* spacing (4-byte far pointers), so the slide looks like it shifted the IVT number up into the IDT row.

Two practical notes:
1. Don't "correct" your note to match the slide. It's right.
2. The quiz question on this topic asks about **how the location is determined** (hardcoded vs IDTR), not the multiplier, so the exam risk is low. If a multiplier question does appear, this is worth raising with the instructor rather than guessing which answer is being marked.

One genuine imprecision in the neighbouring `Interrupt Descriptor Table Register(IDTR)` note: you describe the limit field as specifying *"the size/length of the IDT in bytes"*. It holds the size **minus one** — the offset of the last addressable byte. For a full 256-entry 32-bit IDT that's 2048 bytes, so the limit is **2047**. Same convention as the GDTR.

---

## D. Accurate as written — no action needed

`Cycle Stealing` · `Timer` · `Interrupt` · `ISR(Interrupt Service Routine)` · `Status Register` · `Workings of an IO Operation` · `Interrupt Descriptor Table(IDT)` · `SPOOLing(...)` · `Dual-Mode Operation` · `DMA(Direct Memory Access)` · `Purpose of the Operating System`

`Cycle Stealing` and `Timer` are the two best notes in the vault — both explain a mechanism *and* why it exists. Use them as the template for the notes you rewrite.

Two of these are accurate but thin in a way that costs you marks rather than correctness:
- **`DMA`** — the slide's phrasing is "used to avoid programmed I/O (one byte at a time) **for large data movement**". Your note drops the qualifier. DMA isn't better than programmed I/O unconditionally; it's better for bulk transfer, and has setup overhead that makes it a poor choice for single bytes.
- **`Purpose of the Operating System`** — you list convenience, resource allocation, memory management, protection and security, but not **efficiency** as one of the three stated OS goals. The quiz asks specifically what "efficiency" means in the context of OS goals.

---

## E. Self-test — answer without opening your notes

Cover the vault and write answers out. Anything you can't answer in two sentences is not yet learned, regardless of whether a note exists for it.

**Lecture 1**
1. State the three OS goals from the slides. What specifically does *efficiency* refer to?
2. Distinguish kernel / system program / application program / middleware. Which one is "the one program running at all times"?
3. Why can the CPU access main memory directly but not secondary storage?
4. In the storage hierarchy, which level is managed by the **compiler**? Which by hardware? Which by the OS?
5. Name the four stages of program execution. Which one answers "where in memory does this go?"
6. Which ELF section holds relocation info for **instructions**? Which holds uninitialised globals, and why does it occupy no file space?
7. Segments vs sections — which is for runtime, which is for linking?
8. List four things a loader must do.
9. Give the boot sequence from power-on to kernel, including POST, MBR and chain-loading. How large is the MBR and where does it live?
10. What replaced BIOS on modern systems, and what does GRUB add?
11. Why does spooling lead to multiprogramming?
12. Distinguish buffering, caching and spooling in the I/O subsystem.
13. Distinguish protection from security. What is privilege escalation?
14. Emulation vs virtualization — which is slower and why?

**Lecture 2**
15. Two ways the CPU sends data *to* a device; two ways a device gets attention *from* the CPU.
16. In memory-mapped I/O, what instruction does the CPU use to talk to a controller?
17. Give one advantage and one disadvantage of polling. Which is the exam answer for its main drawback?
18. Maskable vs non-maskable interrupts.
19. Draw the interrupt taxonomy tree from A4 above, from memory.
20. A page fault, a breakpoint and a double fault — classify each and say which are recoverable.
21. What does the interrupt architecture have to save, and why is it too late for the ISR to save the PC itself?
22. Can an ISR be interrupted? Under what condition?
23. List the four fields the OS writes into a DMA command block.
24. Why does DMA reduce the *number of interrupts* rather than eliminating them?
25. What is the device-status table and what does each entry hold?
26. In asynchronous I/O, what happens immediately after the user program initiates the request?
27. How does the system guarantee a user program cannot set the mode bit to kernel?
28. Give three privileged instructions and three non-privileged ones.
29. Walk through what the timer does, from the OS setting it to the OS regaining control.
30. Why is a device controller's local buffer necessary — why not transfer straight to main memory?

Question 30 has no note behind it at all; `Local Buffer Storage` is empty. Start there.
