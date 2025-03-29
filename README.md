# Two-stage op-amp design
![Two-stage op-amp](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Schematic/Op-amp.png)

Open-source two-stage operational amplifier

# Contents
- [Used Tools](#Used-Tools)
- [Parameters](#Parameters)
- [Schematic](#Schematic)
- [Pre-Layout Simulation](#Pre-Layout-Simulation)
- [Layout](#Layout)

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
    <td>Compensation capacitor</td>
    <td>800fF</td>
</tr>
<tr>
    <td>Slew Rate</td>
    <td> 18 V/µs</td>
</tr>
</table>

# Schematic
![Two-stage op-amp](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Schematic/Schematic.png)

# Pre-Layout Simulation

**Common-mode gain**

![Common-Mode-Gain](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Common-mode%20gain.png)

**Derivative**

![Derivative](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Derivative.png)

**Differential-mode gain**

![Differential-Mode-Gain](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Differential-mode%20gain.png)

**ICMR**

![ICMR](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/ICMR.png)

**PSRR**

![PSRR](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/PSRR.png)

# Slew rate
![Slew=Rate](https://github.com/CircuitCraftsman/Two-stage-Op-amp/blob/main/Simulation/Pre-layout/Slew%20rate.png)

# Script for full simulation

<pre>*********** OP-AMP CHARACTERIZATION SCRIPT ***********

* Include Technology and Models
.lib /usr/local/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice tt

* Circuit Under Test
.include ./Op-amp.spice
X1 Vinp Vinn Vout Vdd Vss Vref Op-amp

* Power Supplies
Vdd Vdd 0 DC 1.8 AC 1
Vss Vss 0 DC 0

* Differential Inputs (for diff-mode gain)
Vcm Vin_common 0 DC 0.9
Vdiff Vinp Vin_common DC 5m
Vdiff2 Vinn Vin_common DC -5m

* Bias Current Source
Iref Vdd Vref DC 10u

* Load
CL Vout 0 1p

*************** AC ANALYSIS: Diff-mode gain + PSRR ***************
.control
set filetype=ascii

ac dec 100 1 1G
let diff_in = v(Vinp) - v(Vinn)
let diff_gain = v(Vout)/diff_in
let psrr_plus = v(Vout)/v(Vdd)

* Save Plots
plot db(diff_gain) > diff_gain.dat
plot db(psrr_plus) > psrr.dat

.endc

*************** TRAN ANALYSIS: Slew Rate ***************
* Apply large signal input
Vin_slew Vinp 0 PULSE(-1.8 1.8 0n 1n 1n 10u 20u)
Vinn Vinn 0 DC 0.9

.control
tran 0.01u 25u
plot v(Vout) > slew.dat
plot deriv(v(Vout)) > slew_deriv.dat
.endc

*************** DC ANALYSIS: ICMR ***************
* Sweep common-mode input
Vcm Vin_common 0 DC 0
Vinp Vinp Vin_common DC 5m
Vinn Vinn Vin_common DC -5m

.control
dc Vcm 0 1.8 0.01
plot v(Vout) > icmr.dat
.endc

*************** NOISE ANALYSIS: Input-referred noise ***************
* For noise, small-signal sources should be in place
* AC sources applied to input

* Differential excitation
Vac Vinp 0 AC 1
Vinn Vinn 0 AC 0

.control
noise v(Vout) Vinp dec 100 1 1G 1
* Print total integrated noise from 1Hz to 1GHz
print inoise_total onoise_total
plot onoise > output_noise.dat
plot inoise > input_noise.dat
.endc

.end
 ``` </pre>
