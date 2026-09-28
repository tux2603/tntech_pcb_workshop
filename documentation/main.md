# Tennessee Tech PCB Design Workshop

## Overview

This workshop is designed to provide hands-on experience with PCB design and manufacturing processes. Participants will learn how to design a PCB using industry-standard software, understand the manufacturing process, and how to follow best practices for creating reliable and efficient PCB layouts. Due to time constraints, this workshop will not go over schematic capture or simulation, nor will it cover advanced topics such as high-speed design, RF design, or power electronics. Instead, the focus will be on the fundamentals of PCB design, including layout techniques, component placement, routing strategies, and design for manufacturability.

In the workshop, participants will be guided through the process of designing a simple PCB starting from a provided schematic. The goal will be to create a functional PCB layout that can be manufactured and assembled. The schematic used in this workshop is a simple microcontroller dev-board based on the STM32C071RB6N from STMicroelectronics. This microcontroller is a 32-bit ARM Cortex-M0+ device capable of running at up to 48 MHz with 128 kB of flash memory, 16 kB of SRAM. This device is suitable for a wide range of applications, and was selected because it can be programmed using a built-in USB DFU bootloader without the need for an external crystal or expensive programming tools. The final board can be programmed directly from the Arduino IDE, but will also work with other programming environments such as PlatformIO, STM32CubeIDE, and Keil MDK.

## Workshop Goals

By the end of this workshop, participants will be able to:
- Understand the basics of PCB design and layout.
- Use PCB design software to create a PCB layout from a schematic.
- Apply best practices for component placement, routing, and design for manufacturability.
- Prepare a PCB design for manufacturing, including generating Gerber files and a Bill of Materials (BOM).
- Assemble and test a simple PCB design.

## Workshop Materials and Resources

The only thing that participants will need to bring to the workshop is a laptop with KiCad 10.0 installed. KiCad is a free and open-source PCB design software that is widely used, both in the industry and by hobbysists. KiCad is available for Windows, MacOS, and Linux, and can be downloaded from the official KiCad website: [https://kicad.org/download/](https://kicad.org/download/). Participants are encouraged to install KiCad prior to the workshop to ensure that they have the latest version and that it is working properly on their system. All other materials, including the PCB and all components needed for the workshop, will be provided by the workshop organizers.

If you would like to assemble the PCB after the workshop, all of the parts are available for purchase from DigiKey, Mouser, or other electronics distributors. A boll of materials (BOM) for the PCB is provided [In this repository](../Tech%20PCB%20BOM.csv), and a DigiKey parts list is available [here](https://www.digikey.com/en/mylists/list/NAWFEKVTE1). Additional PCBs can be purcased from any major PCB manufacturer, such as [JLCPCB](https://jlcpcb.com/), [PCBWay](https://www.pcbway.com/), [OSH Park](https://oshpark.com/), or [DKRed](https://www.digikey.com/en/resources/dkred).

A quick reference guide to PCB design best practices can be found in the [PCB Design Best Practices](pcb_design_best_practices.md) document. Slides from the workshop will be uploaded in the future.

## External Resources

- **[KiCad Documentation](https://docs.kicad.org/)**: The official documentation for KiCad, including tutorials and reference materials.
- **[Phil's Lab YouTube Channel](https://www.youtube.com/@PhilsLab)**: A YouTube channel with tutorials and videos on PCB design, electronics, and related topics.

