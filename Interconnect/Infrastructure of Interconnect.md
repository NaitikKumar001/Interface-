p1# Types of Interconnect.

An interconnect is the communication infrastructure that allows different hardware blocks inside a chip to communicate with each other.

There are different ways to design an interconnect. Three important types are:
```
1. Bus
2. Crossbar
3. NoC (Network-on-Chip)
```
---

# Bus

A bus can be thought of as a single shared communication path.
```
             CPU
              │
              ▼
════════════════════════════
          SHARED BUS
════════════════════════════
      │        │        │
      ▼        ▼        ▼
    Memory    GPIO     UART
```
All the connected hardware blocks share the same communication path.

For example, if the CPU wants to communicate with memory:
```
CPU ─────► BUS ─────► Memory
```
If the CPU wants to communicate with GPIO:
```
CPU ─────► BUS ─────► GPIO
```
The Problem with a Shared Bus

If multiple hardware blocks want to use the bus at the same time:
```
CPU ──┐
      ├──► BUS ───► Memory
GPU ──┘
```
Both devices are competing for the same shared path.

Therefore, an arbiter may be required to decide which requester gets access first.

Advantages of a Bus
```
- Simple architecture
- Relatively easy to design
- Suitable for small and simple systems
```
Disadvantage
```
As the number of devices increases, the shared bus can become a bottleneck, because many devices have to share the same communication path.
```
---

# Crossbar

A crossbar provides multiple possible communication paths between hardware blocks.

A simplified view is:
```
             Memory    GPIO    UART
                │        │       │
                │        │       │
CPU ────────────┼────────┼───────┤
GPU ────────────┼────────┼───────┤
DMA ────────────┼────────┼───────┤
                │        │       │
             CROSSBAR
```
Unlike a simple shared bus, a crossbar can allow different hardware blocks to communicate through independent paths.

For example:
```
CPU ─────────► Memory
GPU ─────────► UART
```
These transactions can potentially happen in parallel, provided that they do not compete for the same destination or resource.

Advantages
```
- Higher parallelism
- Higher potential performance
- Multiple transactions can occur simultaneously
```
Disadvantage
```
A crossbar can become complex and hardware-expensive as the number of connected devices increases.
```
---

# NoC — Network-on-Chip

NoC stands for Network-on-Chip.

When a chip becomes very large and contains many hardware blocks, a simple bus or large crossbar may not scale efficiently.

For example, a modern SoC may contain:
```
- CPU cores
- GPU
- Memory controllers
- DSP
- AI accelerators
- DMA controllers
- I/O controllers
- Other peripherals
```
Instead of connecting everything through one shared bus, we can create a network inside the chip.
```
       CPU
        │
      Router
        │
   ┌────┼────┐
   │    │    │
 Router Router Router
   │    │    │
 Memory GPU  DSP
```
A NoC contains communication links and routers.

The routers help move data from the source to the destination through the network.

The basic idea is similar to a communication network:

«Data travels through a network from a source to its destination.»

The internal implementation is much more specialized than the Internet, but the basic networking concept is useful for understanding it.

---

# Bus vs Crossbar vs NoC
```
Type| Basic Idea| Typical Use
Bus| One shared communication path| Small/simple systems
Crossbar| Multiple possible direct communication paths| Medium-sized, higher-performance systems
NoC| A network of links and routers| Large and complex SoCs
```
---

Road Network Analogy

The easiest way to visualize the three types is to imagine roads.

Bus — One Shared Road
```
CPU ─────── ROAD ─────── Memory
             │
             ├──────── GPIO
             └──────── UART
```
Everyone shares the same main road.

---

Crossbar — Multiple Direct Roads
```
CPU ───────── Memory
 │  ╲
 │   ╲──────── GPIO
 │
 └──────────── UART
```
There are multiple possible paths between different blocks.

---

NoC — A Complete Road Network
```
CPU ── Router ── Router ── Memory
        │          │
      Router ─── Router
        │
       GPU
```
There are multiple interconnected paths, and routers help direct communication toward the destination.

---
## Comparing Interconnect Types

| Feature | Shared Bus | Crossbar | Network-on-Chip (NoC) |
|---|---|---|---|
| **Scales to** | A few managers | ~16 × 16 | Hundreds of nodes |
| **Wiring cost** | Low | Grows as managers × subordinates | Grows approximately linearly |
| **Delay** | Low when quiet; high when busy | Low and steady | A few cycles per hop; predictable |
| **Transfers at once** | 1 transfer | Many, if there is no clash | Many flows |
| **Typical use** | Slow peripherals | Main backbone of most chips | Many-core CPUs, GPUs |
