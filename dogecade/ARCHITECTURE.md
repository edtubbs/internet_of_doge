# Dogecade Architecture
## Table of Contents
- [Doge Arcade System Overview](#doge-arcade-system-overview)
  - [Concept Overview](#concept-overview)
  - [System Architecture](#system-architecture)
- [Hardware](#hardware)
- [Software](#software)

## Doge Arcade System Overview
### Concept Overview
**Brainstorm a Doge Arcade**
Discusses a novel Dogecoin-based payment system for arcades. It involves replacing traditional coin slots with cryptocurrency transactions. Key components include software for address generation, transaction monitoring, user interaction through QR codes or mobile apps, and hardware adaptations for electronic activation in arcade machines. Administrative tools for operational management are also highlighted. For more details, visit the following links:
  - [Blog Post](https://blog.ifdogethenwow.com/posts/brainstorm-a-doge-arcade/)
  - [GitHub Repository](https://github.com/chromatic/internet_of_doge/tree/main/dogecade)
  - [Forum Discussion](https://forum.dogecoin.org/d/17-arcadevending-machine-payment-processing/2)


### System Architecture
The Doge Arcade System architecture is designed to be integrated with existing arcade systems. It features networked arcade machines with electronic activation, connected to central servers and payment terminals, managed via administrative tools and a user-friendly mobile app.

The architecture is divided into two subsystems: Gaming and Operations. The Gaming subsystem is responsible for user interaction and transaction processing. The Operations subsystem is responsible for administrative management and security. The two subsystems are connected via a network of arcade machines, servers, and payment terminals. The following diagram illustrates the Doge Arcade System architecture:
```
+----------------------------------------------------------------+
|                      Doge Arcade System                        |
+----------------------------------------------------------------+
| +----------------------------+  +----------------------------+ |
| | Subsystem: Gaming          |  | Subsystem: Operations      | |
| +----------------------------+  +----------------------------+ |
| | User Account Mgmt. (SW)    |  | Database (SW)              | |
| | QR Codes (SW)              |  | Security Systems (SW)      | |
| | Mobile App (SW)            |  |                            | |
| +----------------------------+  +----------------------------+ |
|            |                                |                  |
| +----------------------------+  +----------------------------+ |
| | Arcade Machines (HW)       |  | Networking (HW)            | |
| | - Game Consoles (HW)       |  | - Switches (HW)            | |
| | - Display Screens (HW)     |  | - Routers (HW)             | |
| | - Control Panels (HW)      |  | - Dogecoin Nodes (HW)      | |
| +----------------------------+  +----------------------------+ |
|            |                                |                  |
| +----------------------------+  +----------------------------+ |
| | Activation Mechanisms (HW) |  | Servers (HW)               | |
| | - Coin Acceptors (HW)      |  | - Data Storage (HW)        | |
| | - Electronic Triggers (HW) |  | - Security Modules (HW)    | |
| | - Blockchain Nodes (HW)    |  |                            | |
| +----------------------------+  +----------------------------+ |
|            |                                |                  |
| +----------------------------+  +----------------------------+ |
| | libdogecoin (SW)           |  | Administrative Tools (SW)  | |
| | - such (SW)                |  | - Mobile App (SW)          | |
| | - sendtx (SW)              |  |                            | |
| | - spvnode (SW)             |  |                            | |
| +----------------------------+  +----------------------------+ |
|            |                                |                  |
| +----------------------------+  +----------------------------+ |
| | Kiosk or Admin Terminal    |  | Admin Terminal (HW)        | |
| | Terminal (HW)              |  | - Monitoring Displays (HW) | |
| | - Monitoring Displays (HW) |  | - Control Interfaces (HW)  | |
| | - Control Interfaces (HW)  |  |                            | |
| +----------------------------+  +----------------------------+ |
+----------------------------------------------------------------+
```

## Hardware

**Arcade Machines & Activation Mechanisms**: Adapted for electronic activation.

**Networking Equipment & Servers**: Networked arcade machines and central servers.

**Payment Terminals (Optional)**: User interaction and transaction processors.

**Kiosk or Administrative Terminal**: Hub for arcade management.

## Software

**Mobile App**: User account management and transaction processing.

**Dogecoin Transaction System, libdogecoin & SPV Node**: Transaction processing, address generation, and scanning.

**Database Systems & Security Software**: User account management and security.

**Administrative Tools**: Suite for arcade management, including the mobile app and admin terminal.

## Dogecade Transaction Flow

The following diagram illustrates the flow of a Dogecoin transaction in the Doge Arcade System:
```
+----------------------+           +-----------------------+           +-----------------------+            +----------------------+
|    User's Wallet     |           |    Arcade Machine     |           |     Dogecoin Core     |            |       Dogecoin       |
|      (External)      |           |      (Gaming HW)      |           |    (Operations HW)    |            |      (External)      |
+----------------------+           +-----------------------+           +-----------------------+            +----------------------+
           |                                   |                                   |                                   |
           | 1. User initiates game            |                                   |                                   |
           |    transaction from wallet.       |                                   |                                   |
           |---------------------------------->|                                   |                                   |
           |                                   |                                   |                                   |
           | 2. libdogecoin on Arcade          |                                   |                                   |
           |    Machine generates a unique     |                                   |                                   |
           |    receiving Dogecoin address     |                                   |                                   |
           |    for the game transaction.      |                                   |                                   |
           |<----------------------------------|                                   |                                   |
           |                                   |                                   |                                   |
           | 3. User's wallet sends the        |                                   |                                   |
           |    game transaction to the        |                                   |                                   |
           |    generated Dogecoin address     |                                   |                                   |
           |    (QR code or manual input).     |                                   |                                   |
           |---------------------------------------------------------------------------------------------------------->|
           |                                   |                                   |                                   |
           |                                   |                                   | 4.0 Dogecoin Core on the          |
           |                                   | 4.1 spvnode on Arcade Machine     |     Operations side monitors      |
           |                                   |     scans the blockchain for      |     and processes incoming        |
           |                                   |     incoming transactions         |     transactions for all          |
           |                                   |     to the generated address      |     arcade machines.              |
           |                                   |     (address scanning).           |<----------------------------------|
           |                                   |<----------------------------------------------------------------------|
           | 5.0 Arcade Machine receives       |                                   |                                   |
           |     the confirmed transaction     |                                   | 5.1 Dogecoin Core confirms        |
           |     and activates the game.       |                                   |     the game transaction          |
           |<----------------------------------|                                   |     and updates the wallet        |
           |                                   |                                   |     balance for the arcade        |
           |                                   |                                   |     machine.                      |
           |                                   |                                   |---------------------------------->|
           |                                   |                                   |                                   |
           |                                   |                                   |                                   |
```
***Assumptions***:

Operations runs a full Dogecoin node.

Gaming runs SPV node for monitoring transactions.

The Arcade Machine on Gaming receives transactions from the user's wallet.

Full node on Operations side confirms them.

***Contraints***:

There is no direct connection between Gaming and Operations.

The Arcade Machine is only connected to the Dogecoin network via the SPV node.

No private keys are stored on the Arcade Machine.
