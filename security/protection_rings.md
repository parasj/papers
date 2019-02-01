# A Hardware Architecture for Implementing Protection Rings

* Protection rings are nuanced protection modes beyond user/supervisor
* Ring 0 is most priviledged
* Multics segment descriptors indicate the highest ring that is allowed to read or write the segment
* Low rings of the system do not have execute permissions (lowest ring that has write permissions)

## Hardware support needed
* If OS is designed for portability, typically only 2 protection modes are used
* Rings mean that faults only affect lower rings (ring 3 can only affect ring 4)
* Recent OS have hypervisor mode -1 that allows VMM to control ring 0 hardware access
* Ring register controls memory regions, IO ports and access to special instructions
* CPU loads protection level from current code segment registers
