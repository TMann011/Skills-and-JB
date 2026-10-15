# Systems Integration Matrix: `cook45` & the `chs` Ecosystem

This document defines how the `cook45` AI intelligence core interfaces with and drives technical operations across the three functional repositories in `chs`: `refrence`, `hermes skill`, and `useful`.

---

## 1. High-Level Architectural Relationship

```
                       ┌─────────────────────────────────────────┐
                       │               cook45 Core               │
                       │     (chs/ai/prompts/05_cook45_v3.8)     │
                       └────────────────────┬────────────────────┘
                                            │
               ┌────────────────────────────┼────────────────────────────┐
               ▼                            ▼                            ▼
┌─────────────────────────────┐ ┌───────────────────────┐ ┌─────────────────────────────┐
│        chs/refrence         │ │    chs/hermes skill   │ │         chs/useful          │
│   (Concrete Target Code)    │ │ (Actionable Skillsets)│ │ (Knowledge Base & Forensics)│
├─────────────────────────────┤ ├───────────────────────┤ ├─────────────────────────────┤
│ • Apex External & OS-ImGui  │ │ • Windows Driver No-  │ │ • 500+ Entity Dossiers      │
│ • Vanguard Stack Spoofing   │ │   WDK Build Workflows │ │ • Anti-Cheat Architectures  │
│ • KVM Memflow DMA Pipelines │ │ • PE Analysis Modules │ │ • Hypervisor & DMA Forensics│
│ • UE4 GNames/GObjects SDKs  │ │ • Inline Hook Scaffolds│ │ • Windows Kernel Callbacks  │
└─────────────────────────────┘ └───────────────────────┘ └─────────────────────────────┘
```

---

## 2. Deep Integration Mappings

### Target Domain 1: Kernel Drivers & Hardware Abstraction
- **`cook45` Directive**: Direct syscall invocation, handleless kernel access, manual PE mapping, page protection management.
- **Reference Implementation (`chs/refrence`)**:
  - `refrence/Apex_External/Memory/driver.h`: Kernel-mode IOCTL dispatch, physical memory mapping, and shared memory communication primitives.
  - `refrence/Valorant/KVM_Memflow_DMA_Introspection`: Hypervisor-level introspection bypassing kernel-mode hook detection entirely.
- **Hermes Skillset (`chs/hermes skill`)**:
  - `hermes skill/.../windows-driver-nowdk/SKILL.md`: Zero-header C driver compilation via pure MSVC `cl.exe` / `link.exe` without multi-gigabyte WDK bloat.
- **Useful Knowledge Base (`chs/useful`)**:
  - `useful/wiki/overviews/windows-kernel.md`: Analysis of `PsSetLoadImageNotifyRoutine`, `ObRegisterCallbacks`, and driver table unlinking (`PiDDBCacheTable`, `MmUnloadedDrivers`).

---

### Target Domain 2: EDR / Anti-Cheat Stack Evasion
- **`cook45` Directive**: Detour/trampoline hooks, instruction boundary relocation, dynamic SSN recovery, VEH / hardware breakpoints.
- **Reference Implementation (`chs/refrence`)**:
  - `refrence/Valorant/Vanguard_StackWalk_ReturnAddress_Spoofing`: Synthetic call stack construction (`RtlCaptureStackBackTrace` evasion) redirecting return addresses to legitimate `ntdll.dll` gadgets (`jmp rbx`).
  - `refrence/Valorant/IAT_Stealth_and_HID_Timing_Simulator`: Dynamic IAT hiding and hardware mouse timing emulation to evade heuristic behavioral detection.
- **Hermes Skillset (`chs/hermes skill`)**:
  - `hermes skill/.../windows-hooking-techniques/SKILL.md`: Trampoline calculations, 5-byte vs 14-byte patching, and memory page permissions.
- **Useful Knowledge Base (`chs/useful`)**:
  - `useful/wiki/concepts/stack-spoofing.md`: Unwind info synthesis and frame-pointer tampering forensics.
  - `useful/wiki/concepts/vanguard.md` & `battleye.md`: Kernel-level integrity verification mechanisms.

---

### Target Domain 3: Game Engine & Virtual Memory Introspection
- **`cook45` Directive**: High-throughput AOB pattern scanning, multi-level pointer dereferencing, struct reconstruction, Vtable recovery.
- **Reference Implementation (`chs/refrence`)**:
  - `refrence/Valorant/UE4_SDK_and_Memory_Frameworks`: GObjects, GNames, and GWorld offset resolution in live memory.
  - `refrence/Apex_External/OS-ImGui`: External DirectX/ImGui overlay synchronization without in-process module injection.
- **Hermes Skillset (`chs/hermes skill`)**:
  - `hermes skill/.../game-memory-internals/SKILL.md`: Live process memory scraping, pointer pathing, and integrity checks.
  - `hermes skill/.../pe-binary-analysis/SKILL.md`: Section parsing, base relocations, and TLS callback enumeration.
- **Useful Knowledge Base (`chs/useful`)**:
  - `useful/wiki/overviews/game-engine.md` & `game-hacking.md`: World-to-screen matrix math, bone transformation pipelines, and SDK generation tools (`Dumper-7`).

---

## 3. Operational Workflow: AI-Driven Reverse Engineering

When an operator (`clack`) tasks `cook45` with a reverse engineering or offensive security objective, the agent executes through this pipeline:

1. **Information Retrieval & Contextual Grounding**:
   - Queries `chs/useful/wiki/` for existing threat models, anticheat routines, or known driver vulnerabilities.
2. **Technique Selection**:
   - Leverages `chs/hermes skill/` to select standard, verified engineering blueprints (e.g., zero-WDK kernel compilation, VEH dispatcher setup).
3. **Target Validation & Adaptation**:
   - Cross-references real-world source implementations in `chs/refrence/` (e.g., adjusting return address gadgets for target PE headers).
4. **Execution Mode Generation**:
   - Emits pure, compile-ready, hardened C/C++ or ASM primitives directly to clack with zero conversational overhead.
