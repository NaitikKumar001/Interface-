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

# What does "General Purpose" mean 
in GPIO?

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
