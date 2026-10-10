

Notes built from a Q&A revision session, checked against the Lecture 2 and Lecture 3 PDFs. Each section says which slide it's from, and flags anything that's my synthesis rather than a direct slide statement — check those against your own notes or the instructor before quoting them as "from lecture."

---

## 1. Dual-mode operation

**Source: Lecture 2, "Dual-mode Operation" / "CPU privilege modes."**

- Dual-mode operation exists so the OS can protect itself and other system components from user programs — not to let the OS and CPU "communicate" in general.
- A hardware **mode bit** tracks which mode the CPU is in: `user` while user code runs, `kernel` while kernel code runs.
- User code can never set the mode bit to kernel directly. The only path from user → kernel mode is a **system call**; returning from the call resets the bit to user.
- The full instruction set is split into two groups:
  - **Privileged instructions** — kernel mode only. Examples from the slide: change the IDTR value, I/O instructions, `Halt`, turn off all interrupts, set the timer, context switching, clear memory, remove a process from memory, modify device-status table entries.
  - **Other instructions** — either mode. Examples: `add`, `sub`, reading processor status, reading system time, generating a trap instruction, sending output to the printer.

**Why "turn off all interrupts" specifically must be privileged:** the timer interrupt is how the OS preempts a running process (see §2). If user code could disable interrupts, it could mask the timer interrupt and the OS would never regain control — the process (or the whole system) hangs. Restricting the instruction to kernel mode is what prevents that. This is not physical hardware damage — it's loss of scheduling control.

**Timer, specifically:**
- OS sets the timer counter (a privileged instruction) before scheduling a process.
- Counter decrements with the physical clock; hitting zero generates an interrupt.
- Purpose: prevent infinite loops or one process hogging the CPU past its allotted slice — this runs for *every* scheduled process, not just "if something goes wrong."

---

## 2. Where the checks sit in the instruction cycle

**Source: Lecture 2, "Interrupt Handling" diagram, combined with §1 and §3 below.**
**⚠ Synthesis — the deck doesn't draw this as one figure.** The base cycle (Fetch/Decode/Execute/Writeback/Check-IF-flag) is a direct slide diagram; layering the privilege check into "execute" specifically, and tying it to an illegal-instruction fault, is my inference from architecture fundamentals, not a quoted slide.

- **Fetch → Decode → Execute → Writeback → Check IF flag**, then loop.
- **Synchronous path (privilege fault):** during **execute**, if the decoded instruction is privileged and the mode bit reads `user`, the CPU refuses to run it and raises a fault instead — checked once, tied to that one instruction.
- **Asynchronous path (device/timer interrupt):** at the **IF-flag check**, once per completed instruction, regardless of what that instruction was. If `IF = 1`, control transfers to the ISR via the interrupt vector; the ISR services the device and returns, and — per the slide — *"CPU resumes running interrupted program."*
- Full reference diagram + comparison table: [Instruction Cycle Trap Flow](https://claude.ai/code/artifact/ac01c3d4-ac33-453e-a298-5bbfc53ad8ff)

---

## 3. Exceptions: Faults / Traps / Aborts

**Source: Lecture 2, "Interrupts (Cont.)."**

| Category | Meaning | Examples |
|---|---|---|
| **Faults** | Recoverable | page fault, division by zero, **illegal instruction** |
| **Traps** | Intentional | breakpoints in debugging |
| **Aborts** | Severe, unrecoverable | double fault, hardware failure |

**Terminology trap (literally):** the deck uses the word "trap" at two different levels — don't conflate them on an assessment.

1. **General mechanism (verb):** *"A trap or exception is a software-generated interrupt caused either by an error or a user request."* This covers system calls **and** exceptions alike — anything triggered by the CPU's own execution rather than an external device.
2. **Narrow category (noun, this table only):** "Trap" here means specifically an *intentional* exception like a breakpoint — a different box from Faults.

So: a privileged-instruction violation is a **Fault** (illegal instruction) in this table's terms, even though the general mechanism that delivers it is correctly described as "trapping into the kernel." Elsewhere the same deck labels system calls as **"Trap Interrupts"** under Software Interrupts — using "trap" in the general sense again. The deck itself is inconsistent about this; know both senses.

---

## 4. System calls

**Source: Lecture 2 ("Interrupts (Cont.)," "Dual-mode Operation") + Lecture 3 ("OS Services").**

A system call is a request for a kernel-provided service (file I/O, process control, device access) — **not** a check on whether the CPU is able to run something.

**Mechanism:**
1. User program executes a trap instruction (e.g. the `INT` instruction) — a deliberate, self-triggered software interrupt.
2. The trap flips the mode bit to kernel and transfers control to the OS's system-call handler.
3. Handler performs the requested service using privileged instructions as needed.
4. Control returns to the user program; mode bit resets to user.

*(Lecture 2: "System call executes via trap to trigger kernel to execute request." / "System call changes mode to kernel, return from call resets it to user.")*

**System call implementation (Lecture 3):**
- Each system call has a number; the **system-call interface** keeps a table indexed by that number, invokes the right kernel routine, and returns status/results.
- The caller doesn't need to know how it's implemented — just the API contract.

---

## 5. API vs. library vs. system call — the layering

**Source: Lecture 3, "OS Services."**

These are related but **not** the same thing:

- **API** (POSIX, Win32, Java API) — what the programmer codes against. Most programs use the API rather than issuing system calls directly.
- **Run-time support library** — implements the API; "a set of functions built into libraries included with compiler." Hides most OS-interface detail from the programmer.
- **System call** — specifically, the operation that traps into the kernel.

Not every API function is a system call. The slide's own example: **`printf()` is a C library/API call that itself calls `write()`, the actual system call.** `printf()` formats and buffers; it never touches the kernel directly. `write()` is what traps.

**Caveat on naming, direct from the slide:** *"the system-call names used throughout this text are generic"* — the course often uses a function's name (`open()`, `read()`, `write()`, `fork()`) as shorthand for "the system call," without always separating the API layer from the underlying trap. Assume the loose usage unless a question is specifically testing the `printf`/`write` distinction.

---

## Self-check (don't read the notes above while answering)

1. Why must "turn off all interrupts" be a privileged instruction — what specifically breaks if it isn't?
2. A user-mode program tries to execute a privileged instruction. Walk the sequence from mode-bit check to what the OS does about it.
3. Is an illegal-instruction violation classified as a Fault or a Trap in the Lecture 2 taxonomy — and why might someone reasonably call it "trapping into the kernel" anyway?
4. What's the difference between what `printf()` does and what `write()` does?

---
*Built from a Q&A session — cross-check the flagged synthesis points against the Lecture 2 / Lecture 3 PDFs before treating them as quotable slide content.*
