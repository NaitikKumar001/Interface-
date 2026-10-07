# What is AMBA?

AMBA = Advanced Microcontroller Bus Architecture

AMBA was developed by Arm.

Simplest Definition

AMBA is a family of communication protocols/specifications that defines the rules for communication between different hardware blocks inside an SoC.

Example

              CPU
               │
               │
        ┌──────▼──────┐
        │ Interconnect│
        └──────┬──────┘
          ┌────┼────┐
          ▼    ▼    ▼
       Memory UART GPIO

AMBA helps define the rules according to which these hardware blocks communicate with each other.

---

# Why is AMBA called a "Family"?

AMBA is not a single protocol.

It contains multiple communication protocols.

Just like a family has multiple members:
```
AMBA
 │
 ├── AXI
 ├── AHB
 ├── APB
 └── ACE
```
For our current interconnect topic, the main protocols to understand are:

- AXI
- AHB
- APB

---

# What is AXI?

AXI = Advanced eXtensible Interface

AXI is mainly used for high-performance communication between hardware blocks.

Example
```
CPU / DMA
    │
    │ AXI
    ▼
Memory / High-performance hardware
```
AXI provides advanced features such as:
```
- Multiple outstanding transactions
- Burst transfers
- Separate read and write channels
- VALID/READY handshake
```
| Channel | Short | Driven by | Carries |
|---|---|---|---|
| Write address | AW | Manager | Where to write, how many beats |
| Write data | W | Manager | The data, which bytes are valid, "last beat" |
| Write response | B | Subordinate | OK, or an error |
| Read address | AR | Manager | Where to read, how many beats |
| Read data | R | Subordinate | The data, status, "last beat" |

# What is APB?

APB = Advanced Peripheral Bus

APB is designed for simple and low-bandwidth peripherals.

Example
```
Interconnect
     │
     │ APB
     ▼
   UART
```
APB can be used to access the registers of simple peripherals.

Examples
```
- UART
- GPIO
- Timer
- Simple control registers
```
So, you can remember APB as a protocol commonly used for simple peripheral communication.

---

# What is AHB?

AHB = Advanced High-performance Bus

AHB is also a protocol in the AMBA family.

It was designed for relatively high-performance system communication.

Example
```
CPU
 │
 │ AHB
 ▼
Memory / Other hardware
```
AHB can be found especially in simpler AMBA-based systems and microcontroller-type designs.

---

# AXI, AHB and APB Together
```
                    AMBA
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
         AXI         AHB         APB
          │           │           │
       High          High       Simple /
    performance   performance   low-bandwidth
          │           │           │
      CPU/Memory    System      UART/GPIO/
                     bus         Timer
```
Simple Comparison

| Protocol | Main Idea | Typical Use |
|---|---|---|
| AXI | High-performance communication | CPU, Memory, DMA |
| AHB | High-performance system communication | Microcontrollers, system buses |
| APB | Simple, low-bandwidth communication | UART, GPIO, Timer |

Easy Memory Trick

AXI → High-performance communication

AHB → System-level communication

APB → Simple peripheral communication

The important point is that AXI, AHB, and APB are communication protocols within the AMBA family, while the interconnect is the hardware infrastructure that connects and routes communication between different blocks.
