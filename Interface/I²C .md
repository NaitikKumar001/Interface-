# What is I²C?

I²C = Inter-Integrated Circuit

I²C is a serial communication
protocol/interface that allows one
controller to communicate with multiple
electronic devices.

Simple:
```
             CPU / MCU
                │
                │ I²C
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
 Temperature  Accelerometer  EEPROM
    Sensor
                │
                ├──── RTC
                │
                └──── Other ICs
```
—>The main purpose of I²C is:

«To exchange digital data between a
controller and one or more peripheral
devices using only two main signal lines.»

---

# Where is I²C Used?

I²C is commonly used for short-distance
communication between chips/ICs, 
especially when multiple low-speed or 
moderate-speed peripherals need to 
communicate with a controller.

Examples:
```
- 🌡️ Temperature sensors
- 🧭 Accelerometers
- 🌀 Gyroscopes
- 💾 EEPROM
- ⏰ Real-Time Clock (RTC)
- 🔋 Battery and power-management ICs
- 🖥️ Display controllers
- 🔧 GPIO expanders
- 🔊 Some audio and control ICs
```
Example:
```
             MCU
              │
           I²C Bus
              │
      ┌───────┼────────┬────────┐
      ▼       ▼        ▼        ▼
    Temp     RTC     EEPROM     IMU
   Sensor
```
One important feature of I²C is that 
multiple devices can share the same bus.

---

# How Many Wires Does I²C Use?

A basic I²C bus uses two main signal lines:

```SDA```

SDA = Serial Data

The SDA line carries the actual data bits 
being exchanged between the controller and
devices.

```SCL```

SCL = Serial Clock

The SCL line carries the clock signal,
which helps coordinate the timing of
communication.

              I²C BUS

        SDA ─────────────────────
             Serial Data

        SCL ─────────────────────
             Serial Clock

Therefore:

SDA = Data
SCL = Clock

These two lines allow multiple I²C devices
to communicate over the same bus.

# Some important terms. 
1] CONTROLLER:- Controller is device which 
control communication between CPU and target 

2] TARGET:- TARGET is device from which 
controller connects with. means an external 
device

3] REQUEST:- It is a instruction given to 
target through controller. 

4] RESPONSE:- When target process request and
give data that Is response.

# 4. What does "Two Open-Drain Wires" mean?

The slide says:

«I²C shares just two wires among all
devices: SDA and SCL, plus ground.»

This means:
```
- SDA → Data
- SCL → Clock
- GND → Common electrical reference
```
However, SDA and SCL are not normal push-pull wires.

They use:
```
Open-drain outputs + pull-up resistors
```
---

# Understanding Open-Drain

Let's connect this with the concept of an open-drain driver.

             SDA
              │
              ●
              │
       Open-Drain Driver
              │
             GND

The open-drain driver can do one important thing:

```Driver ON```

When the driver is ON, it connects the SDA line to GND.
```
SDA
 │
 ↓
GND
```

Therefore:
```
SDA = 0 (LOW)

Driver OFF
```
When the driver is OFF, it does not drive SDA HIGH.
Instead, the driver simply disconnects from the line.

```Driver = OFF```

Now the pull-up resistor can bring the SDA line to HIGH.
```
VCC
 │
Pull-up Resistor
 │
SDA
```
Therefore:
```
Driver OFF → Pull-up resistor → HIGH
Driver ON  → GND             → LOW
```
This is the fundamental electrical concept behind I²C.

---

# Why is a Pull-Up Resistor Needed?

This is very important.

An open-drain driver cannot actively drive the line HIGH.

So the question is:

Q—>How does SDA become HIGH?

—>The answer is:

«The pull-up resistor.»

The basic arrangement is:
```
             VCC
              │
        Pull-Up Resistor
              │
              ●──────── SDA
              │
       Open-Drain
         Driver
              │
             GND
```
When no device pulls SDA LOW:

Driver = OFF
      ↓
Pull-up resistor
      ↓
SDA = HIGH

When a device pulls SDA LOW:

Driver = ON
      ↓
SDA connected to GND
      ↓
SDA = LOW

So the basic rule is:
```
Driver OFF → SDA becomes HIGH through the pull-up resistor
Driver ON  → SDA becomes LOW by connecting it to GND
```
# Why is this useful in I²C?

Because multiple devices share the same SDA and SCL lines. The open-drain design allows different devices to safely pull the shared line LOW without one device actively fighting another device that is trying to drive it HIGH.

In short:

«I²C uses open-drain outputs so devices can pull the shared bus LOW, while pull-up resistors bring the bus back HIGH when no device is pulling it LOW.»
