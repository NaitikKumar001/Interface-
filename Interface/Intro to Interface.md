# What is an Interface?

An interface is a defined method of communication between two systems or components.
It defines how two components exchange information.

In simple words:
An interface is the communication boundary and rules that allow two different systems to understand and interact with each other.
For example:
```
CPU  ←──────── Interface ────────→  Peripheral
```
The interface determines things such as:
```
How data is transferred
How data is received
Which signals are used
How timing is controlled
Who sends the data
Who receives the data
How devices are selected
How errors are handled
How the communication starts and ends
```
Basically Interface is just like a communication boundary between two Hardware. Which allows to communicate between Hardwares through control signals. 
Example:
```
        ┌──────────────┐
        │   CPU Core   │
        └──────┬───────┘
               │
            Interface
               │
        ┌──────▼───────┐
        │ Memory       │
        └──────────────┘
```
There is no way from witch CPU directly connect to memory so we use interfaces here.

# Why Do We Need Interfaces?
Different components operate in different ways.
A CPU internally works with:
```
Binary data
Registers
Addresses
Control signals
Clock cycles
Instructions
```
An external device may communicate using a different electrical and logical interface.
For example, a GPIO device uses:
```
GPIO Input → Reads the logic level from an external device
GPIO Output → Sends a logic level to an external device
GPIO Direction → Determines whether the pin works as input or output
```
Therefore, the CPU needs a GPIO Controller that manages these GPIO pins.
The basic architecture is:
```
                    CPU
                     │
                     │ Internal Bus
                     ↓
              ┌───────────────┐
              │ GPIO Controller│
              └───────┬───────┘
                      │
          ┌───────────┴───────────┐
          │                       │
     GPIO Input              GPIO Output
          │                       │
          ↓                       ↓
   External Device          External Device
```
# What does the GPIO Controller do?
The GPIO Controller acts as a bridge between the CPU and GPIO pins.
Example:

—Suppose the CPU wants to turn an LED ON.
```
CPU
 │
 │ "Set GPIO output = 1"
 ↓
GPIO Controller
 │
 │ Output register stores 1
 ↓
GPIO Pin
 │
 │ HIGH
 ↓
LED ON
```
—If the CPU wants to read a button:
```
Button
  │
  │ HIGH / LOW
  ↓
GPIO Pin
  │
  ↓
GPIO Controller
  │
  │ Input register
  ↓
CPU
```
# Interface vs Controller

These two terms are related but should not be confused.

```Interface```

An interface defines the communication rules and signals.
For example, I²C defines:
```
SDA
SCL
Addressing
Start condition
Stop condition
Data transfer rules
Acknowledgement
```

```Controller```

A controller is the hardware that implements those rules.
For example:
```
CPU
 │
 ↓
I²C Controller
 │
 ↓
I²C Bus
 │
 ↓
Sensor
```
The CPU tells the I²C controller what it wants to do.
The I²C controller then performs the required I²C operations.
So:
```
Interface = rules/protocol used for communication
Controller = hardware that implements those rules
```
# What is a Peripheral?

Peripheral = A hardware component that performs a specific task outside the CPU/Core's main computation and allows the CPU to interact with the external world or provides additional functionality.

Simple Definition

> The CPU performs calculations and makes decisions, while peripherals handle specific hardware-related tasks.
```
PERIPHERAL 
├── Communication Interfaces
│   ├── GPIO
│   ├── I²C
│   ├── SPI
│   └── UART
│
├── Timing
│   ├── Timer
│   └── Counter
│
├── Data Conversion
│   ├── ADC
│   └── DAC
│
├── Control
│   └── PWM
│
└── Other Hardware Functions
    ├── Watchdog Timer
    ├── Interrupt Controller
    └── etc.
```
