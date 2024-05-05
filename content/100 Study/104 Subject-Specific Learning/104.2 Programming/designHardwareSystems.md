---
title: Designing Custom Hardware Systems
---
To construct a custom hardware system, here are the following methods:
- use off-shelf components on a breadboard board
	- advantages
		- easy to create + update designs
		- cheap and reusable platform
	- disadvantages
		- small number of chips + wire on one board
		- limited to low frequencies, low currents, low voltages
(prototype boards can not even be reused, but maybe more durable)

- use off-shelf components on a custom PCB
	- advantages
		- boards can be designed easily on CAD tools
		- fabrication is relatively quick + cheap
	- disadvantages
		- boards can't be reused
		- one mistake may render a board useless
		- soldering small parts might need specialized equipment

- use configurable hardware board
	- advantages
		- easy to design
		- easy to upgrade
		- reusable platform
	- disadvantages
		- expensive
		- intellectual property cores are expensive
		- hardware performance + scope of design limited to board

- use custom ASIC (application specific integrated circuit)
	- advantages
		- best performance
		- low cost production in high volumes
	- disadvantages
		- expensive CAD software
		- fabrication is time + money
		- intellectual property cores are expensive
		- one mistake means that chip is uesless


System on a Chip (SoC): user-designed fully-functional system implemented on a single chip. 
- Microprocessor of microcontroller
- Communication port
- Volatile and non-volatile storage
- Other components: timers, parallel interfaces etc.

Programmable Logic Device (PLD): digital logic chip that allows configuration and interconnection of internal logic blocks. Computer chip that can be rewired to implement a custom digital circuit using primitive building blocks
- SRAM (Static Random Access Memory)
- EEPROM (Electronically Erasable Programmable ROM - It will retain config even if disconnected from power)
- NOR Flash (USB memory keys use this)
- Antifuse (Least flexible of these chips) 
![[AntiFuse.jpg]]

FPGA (Field Programmable Gate Array): A type of high-density PLD that is suitable for complex hardware design implementation
- Can implement a multi-core processor system with ease.
System on a Programmable Chip: SoC that is implemented using a high-density PLD that is reconfigurable
- Advantages: flexible, upgradable
- Disadvantages: lower system performance, more expensive in large quantities.