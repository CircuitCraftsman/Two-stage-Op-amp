# Two-stage op-amp
![Two-stage op-amp](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Schematic/Op-amp.png)

Open-source two-stage operational amplifier

# Contents
- [Used Tools](#Used-Tools)
- [Parameters](#Parameters)
- [Schematic](#Schematic)
- [Pre-Layout Simulation](#Pre-Layout-Simulation])
- [layout](#Layout)

# Used-Tools
- Xschem

    - Xschem is a schematic capture program; it allows the creation of hierarchical representation of circuits with a top down approach. By focusing on interfaces, hierarchy, and instance properties, a complex system can be described in terms of simpler building blocks. A VHDL, Verilog, or Spice netlist can be generated from the drawn schematic, allowing the simulation of the circuit. The key feature of the program is its drawing engine written in C and uses the Xlib drawing primitives; this gives very good speed performance, even in huge circuits. The user interface is built with the Tcl-Tk toolkit; TCL is the extension language.

- Ngspice

    - Ngspice is an open-source mixed-level/mixed-signal electronic circuit simulator. It is a successor of the latest stable release of Berkeley SPICE, version 3f.5, which was released in 1993. A small group of maintainers and the user community contribute to the ngspice project by providing new features, enhancements, and bug fixes.

- Magic VLSI

    - Magic is a venerable VLSI layout tool, written in the 1980s at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl. Due largely in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies. The open-source license has allowed VLSI engineers with a bent toward programming to implement clever ideas and help magic stay abreast of fabrication technology. However, it is the well thought-out core algorithms that lend to magic the greatest part of its popularity. Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.

- SkyWater 130

    - SKY130 is a mature 180nm-130nm hybrid technology developed by Cypress Semiconductor that has been used for many production parts. SKY130 is now available as a foundry technology through SkyWater Technology Foundry. The technology is the 8th generation SONOS technology node (130nm).

# Parameters

<table align="center">
<tr>
    <th>Parameters</th>
    <th>Value</th>
</tr>
<tr>
    <td>Differential Gain</td>
    <td>100dB</td>
</tr>
<tr>
    <td>Common Gain</td>
    <td>-38dB</td>
</tr>
<tr>
    <td>GBW</td>
    <td>20MHz</td>
</tr>
<tr>
    <td>CMRR</td>
    <td>138dB</td>
</tr>
<tr>
    <td>Slew Rate</td>
    <td> 18 V/µs</td>
</tr>
</table>

# Schematic
![Two-stage op-amp](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Schematic/Schematic.png)

# Pre-Layout Simulation
  
![Common-Mode-Gain](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Common-mode%20gain.png)

![Derivative](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Derivative.png)

![Differential-Mode-Gain](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Differential-mode%20gain.png)

![ICMR](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/ICMR.png)

![PSRR](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/PSRR.png)

![Slew=Rate](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Slew%20rate.png)


