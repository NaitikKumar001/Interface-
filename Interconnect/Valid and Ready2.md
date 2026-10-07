# VALID and READY.

VALID and READY are extremely important concepts in hardware communication and interconnect protocols.

Imagine that you are giving a parcel to someone.
```
Sender                         Receiver
  │                               │
  │       DATA / PARCEL           │
  └──────────────────────────────►│

The sender has a parcel ready to give.
```
The sender indicates:

```«VALID = 1»```

This means:

«"I have valid data or a valid request available."»

The receiver indicates:

```«READY = 1»```

This means:

«"I am ready to receive the data or request now."»

---

When Does the Transfer Happen?

A transfer takes place only when both VALID and READY are HIGH.

VALID = 1
READY = 1
     — TRANSFER happens 

So the basic rule is:

«Transfer = VALID AND READY»

In a synchronous hardware interface, the transfer is recognized on the rising edge of the clock when both signals are high.
```
Clock ↑
  │
  ├── VALID = 1
  ├── READY = 1
  │
  └── Data Transfer
```
---

# What If READY = 0?

Suppose:

VALID = 1
READY = 0

The sender has valid data, but the receiver is currently busy.
```
Sender                         Receiver
  │                               │
  │ DATA                          │
  │                               │
  └────────────── X ──────────────┤
                                  │
                              Not Ready
```
The transfer does not happen.

The sender must wait.

The sender keeps VALID asserted and keeps the data stable until the receiver becomes ready.
