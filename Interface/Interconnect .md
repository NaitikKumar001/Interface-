# What is an Interconnect?

Imagine a college campus with several buildings:
```
- Computer Lab
- Library
- Administrative Office
- Canteen
- Student areas
```
If someone needs to travel from the Computer Lab to the Library, they need a road or path.

Now imagine creating a separate road between every pair of buildings:
```
        Computer Lab
          │      │
          │      │
      ────┼──────┼──── Library
          │      │
          ├── Office
          │
          └── Canteen
```
As the number of buildings increases, the number of connections and roads would increase significantly.

Instead, we can create a common road network:
```
                  Computer Lab
                       │
                       │
Library ──────── ROAD NETWORK ──────── Office
                       │
                       │
                    Canteen
```
The same basic idea is used inside a chip.

A chip or SoC contains many hardware blocks, such as:
```
              ┌─────────────┐
              │ CPU / Core  │
              └──────┬──────┘
                     │
                     │
        ┌────────────▼────────────┐
        │       INTERCONNECT      │
        └────────────┬────────────┘
              ┌──────┼──────┐
              │      │      │
              ▼      ▼      ▼
           Memory   UART    GPIO
```
The interconnect provides the communication paths that allow these hardware blocks to exchange information.

Simple Definition

«Interconnect is the communication infrastructure that connects different hardware blocks inside a chip and allows them to exchange data, addresses, and control information.»

You can think of an interconnect as the road network of a chip.

---

# What Does "On-Chip" Mean?

Let's break the term into two parts:

```On + Chip```

- On → inside or within
- Chip → an integrated circuit (IC), such as an SoC

Therefore:

«On-chip means something that exists or operates within the chip.»

So:

«On-chip interconnect means the communication system inside a chip that connects different hardware blocks and allows them to communicate with each other.»

For example:
```
              ┌─────────────┐
              │ CPU / Core  │
              └──────┬──────┘
                     │
                     ▼
              ┌─────────────┐
              │ Interconnect│
              └──────┬──────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Memory       UART       GPIO
```
Here, the interconnect acts as the communication infrastructure between the CPU, memory, and peripherals.

Key Idea
```
Chip
 │
 ├── CPU / Core
 ├── Memory
 ├── UART
 ├── GPIO
 └── Interconnect
        │
        └── Connects and enables communication
            between these hardware blocks
```
In short:

«Interconnect = communication infrastructure

On-chip interconnect = communication infrastructure inside the chip»

# Jobs of Interconnect.
There are three major jobs of Interconnect 
```
Address decoding
Arbitration
Bridging
```
# 12. What is Address Decoding?

Let's break the term into two parts:

Address + Decoding

Meaning

Address decoding means looking at a memory address and determining which hardware device should receive the request.

For example:
```
CPU
 │
 │ Address = 0x10010000
 ▼
Interconnect
 │
 │ "Which address range does this belong to?"
 ▼
Memory Map
 │
 │ UART address range
 ▼
UART
```
The interconnect examines the address and compares it with the address ranges assigned to different devices.

If the address falls within the UART range, the request is sent to the UART.

Simple Definition

«Address decoding = Determining the destination by examining the address.»

---

—> The Problem: What if Two CPUs Want the Same Memory?

Consider this situation:
```
CPU 1 ─────┐
           │
           ▼
        MEMORY
           ▲
           │
CPU 2 ─────┘
```
Suppose both CPUs send requests to the same memory at the same time.

The memory may not be able to handle both requests simultaneously in the same cycle.

—> So a question arises:

"«Who gets access first?»"

This is where arbitration is needed.

---

#  What is Arbitration?

Arbitration is the process of deciding which competing request gets access to a shared resource.

For example:
```
CPU 1 ──┐
        │
CPU 2 ──┼──► ARBITER ───► Memory
        │
GPU   ──┘
```
The arbiter receives multiple requests and selects one of them to proceed.

For example:
```
CPU 1 → GO
CPU 2 → WAIT
GPU   → WAIT
```
During a later cycle, another request may be selected:
```
CPU 1 → WAIT
CPU 2 → GO
GPU   → WAIT
```
The exact selection depends on the arbitration policy.

Common Arbitration Methods

1. TURN-BASED

Requests get access in a rotating or predetermined order.
```
CPU 1 → CPU 2 → GPU → CPU 1 → ...
```
This helps provide fairness.

2. PRIORITY-BASED

Some requests are given higher priority than others.
```
High Priority   → CPU 1
Medium Priority → CPU 2
Low Priority    → GPU
```
The highest-priority request gets access first.

3. WEIGHTED

Each requester is given a certain weight, which influences how often it gets access.

For example:
```
CPU 1 → Weight 3
CPU 2 → Weight 2
GPU   → Weight 1
```
A higher weight can give a requester more opportunities to access the shared resource.

Simple Definition

«Arbitration = Deciding which requester gets access when multiple hardware blocks compete for the same shared resource.»

