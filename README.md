# LOMcard
#### A "Lights Out Managment" Card that provides said capability to any [PC] system.

---

## Core Idea
#### Aftermarket LOM for every System
Most Servers integrate a Baseband Managment Controller with and IPMI, LOM and often iKVM into the Mainboard.
- The main difference between Server and Desktop / Workstation Mainboards - aside from being designed with Server Chassis in mind, is the existance of said LOM.
  - The lack of a LOM makes it harder to upcycle and convert older systems into a Server.
    - It also allows to basically use any system as a Server!

---

## Use-Cases
### Upcycle older Systems into Servers
Save time and resources by using older systems as servers.
- This is ideal for small-scale and non-critical "learning" and "testing" envoirments.
### Remote Control of Systems in Hardware
Ideal for Legacy Setups that may have to be installed in sensitive areas and likely out of reach of technicians.
- I.e. Industrial and/or medical systems that are in seperately compartmentalized rooms.
  - Can also be used for remote installations that may otherwise necessitate costly hands-ons.
    - I.e. restarting a system that may not be responsive. 
### Remote Logging and Control
- In some sensitive setups, it may be necessary to transparently record all interactions done with the system.

---

## Features
### Core Features
#### Low Profile "PCI" card
Fits on low-profile PCIe brackets
#### PoE Powered
Since the idea of a LOM is to be hooked up to a network, it is reasonable to assume that PoE is avialable or can at least be injected easily.
##### Optional Internal Power
via Standby-Line from ATX Power Supply [5v_SB or Similar]
#### Transparent status Check
As it's being spliced into the Power & Reset Buttons'- as well as Power & Activity LEDs' Lines, the LOMcard can:
- See if the system is powered on
- See if the system has activity
- Send a Shutdown signal [power button "press"].
- Make a hard shutdown [long power button "press"].
- Do a reboot [reboot button "press"]
### Additional Features
#### 1U Bracket
For installing in 1U Servers which only have extremely narrow heights.
- Provides the PoE Port and 3 LEDs [PoE, Power/Activity, Programmable via GPIO]
#### Serial Console
Onboard USB to RS-232 Adaptor with Nullmodem/Crossover and Pin Header to connect to a serial port.
##### Optional USB to Serial Adapter to plug on 
To connect to Mainboards that don't have any Serial Header onboard.
#### PiKVM Support
Supporting a full KVM for OSes that don't support serial consoles 
- Connects to local Display/Keyboard/Mouse ports.
##### Remote-Reflashable "USB Pendrive" [SSD]
Allows for fully remote use of the System.
- Ideal for Installers or updating live distributions over the network.
  - Needs to shutdown the "Host"-System to safely dismount and remount the storage.

---

## Design
### Core Components
#### RP2040 Microcontroller
- Cheap
- Versatile
- More GPIOs than anyone would ever need.
#### PoE Extractor
- Providing Power to the LOMcard
#### Ethernet Chip
#### RS-232 Chip
### Optional Components
#### Standby Voltage Power Extractor
- Allows the use of Standby Voltage [i.e. ATX 5V_SB] to run the LOMcard
  - Reduces the Necessity for a PoE connection.
#### CM3 / CM4 header/connector
- Needed for PiKVM
#### HDMI2CSI Adaptor
- Needed for PiKVM
  - To accept the Video
#### VGA-to-HDMI Adaptor
- Needed for PiKVM
  - Needed for the HDMI2CSI board on Systems without HDMI-output
    - Alternatives like DP-to-HDMI or DVI-to-HDMI can be designed as well.
#### USB Console Module
- To provide a "Serial Console" on Systems without an RS-232 port.
  - Ideal for UNIX-alike OSes like FreeBSD, Linux, etc.
#### "Pendrive" SSD Module
- Requires PiKVM
  - Allows to be rewritten and booted from
    - Connects via USB
      - Is being switched between LOMcard and "Host"-System
  - Recommended to be used with Ventoy
    - But can be reflashed with basically anything.

---
