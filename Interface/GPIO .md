# What is GPIO?

GPIO = General-Purpose Input/Output
GPIO is a configurable set of digital
pins/interface used to connect a system 
with external devices through
simple digital electrical signals.

In simple words:
GPIO is an interface between the CPU/MCU
and external hardware that allows the 
system to exchange simple ON/OFF (0/1) 
type digital signals.

Example:
```
 CPU/MCU
   │
   │
GPIO
   │
   ├──── LED
   ├──── Button
   ├──── Relay
   ├──── Motion Sensor
   └──── Other digital device
```

             

---

# What does "General Purpose" mean in GPIO?

General Purpose means that, depending on
the hardware,a GPIO pin can be configured 
for different simple purposes.

A GPIO pin can generally be configured as
either:

- Input
- Output

---

```Input```

In input mode, an external device sends a
digital signal to the system.

Example: Button
```
Button
   │
   ↓
GPIO INPUT
   │
   ↓
  CPU
```

The CPU can read the state of the GPIO pin:
```
0 → LOW
1 → HIGH
```
For example:
```
- Button not pressed → GPIO may read "0"
- Button pressed → GPIO may read "1"
```
(The exact HIGH/LOW behavior depends on
the circuit configuration.)

---

```Output```

In output mode, the CPU/MCU sends a digital
signal through the GPIO pin to an external 
device.
```
CPU
 │
 ↓
GPIO OUTPUT
 │
 ↓
LED
```
The CPU can set the GPIO output to:
```
0 → LOW
1 → HIGH
```
For example:
```
CPU sets GPIO = 1
        ↓
     GPIO HIGH
        ↓
       LED
        ↓
       ON
```
So, a GPIO allows the CPU/MCU to read
simple digital signals from external
hardware and send simple digital control
signals to external hardware.

# What is a GPIO Controller?
A GPIO Controller is a hardware block or peripheral that allows the CPU/MCU to control and read GPIO pins.

Simple Architecture

             CPU / RISC-V Core
                    │
                    │
             Bus / Interconnect
                    │
                    ▼
            ┌─────────────────┐
            │ GPIO Controller │
            │                 │
            │  Control Logic  │
            │  Registers      │
            │  Input Logic    │
            │  Output Logic   │
            └────────┬────────┘
                     │
                  GPIO Pins
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        LED        Button      Sensor
        
—Important point

The CPU generally does not directly control the electrical GPIO pin.
Instead:
```
CPU → reads/writes GPIO Controller registers → GPIO Controller controls the GPIO pins
```
The GPIO Controller acts as the hardware interface between the CPU and the physical GPIO pins.

# Why is a GPIO Controller needed?

A CPU contains components such as:
```
Registers
ALU
Control Unit
Program Counter
Instruction-related hardware
```
The CPU is not directly designed to manage the electrical behavior of an external LED, button, sensor, or other device.

Therefore, a GPIO Controller peripheral is used in a SoC or MCU.

Basic flow
```
CPU
 │
 │ Commands / Data
 ▼
GPIO Controller
 │
 │ Digital Electrical Signals
 ▼
GPIO Pin
 │
 ▼
External Device
```
The CPU sends commands by accessing the GPIO Controller's registers.
The GPIO Controller then uses those settings to control the GPIO hardware.

For example:
```
CPU
 │
 │ Set GPIO = HIGH
 ▼
GPIO Controller
 │
 │ HIGH signal
 ▼
GPIO Pin
 │
 ▼
LED → ON
```
So, the GPIO Controller connects the software-controlled CPU side to the physical hardware side.


# What is inside a GPIO Controller?

The exact design can be different from one chip to another. However, a typical GPIO Controller may contain the following components:
```
                 GPIO Controller
        ┌────────────────────────────┐
CPU ───►│ Bus Interface          │
        │                         │
        │ Control Registers       │
        │       │                 │
        │       ▼                 │
        │ Direction Control       │
        │       │                 │
        │       ▼                 │
        │ Output Data Register     │
        │       │                  │
        │       ▼                  │
        │ Output Logic ──────────────┼──► GPIO Pin
        │                           │
        │ GPIO Input ────────────────┼──► Input Data Register
        │                           │
        └────────────────────────────┘
```
