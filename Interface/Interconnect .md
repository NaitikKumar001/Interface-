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
