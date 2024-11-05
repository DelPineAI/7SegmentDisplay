# 7-Segment Alphanumeric Display with Boolean Algebra

## Overview

This project demonstrates the use of Boolean algebra to control a 7-segment alphanumeric display. The goal is to determine which segments should light up to display specific characters, using only Boolean logic derived from truth tables and Karnaugh maps (K-maps). The design was implemented on a Basys 3 FPGA board using Vivado software, but the Boolean logic can be applied to other platforms, including simulations or homemade circuits using LEDs and switches.

## How It Works

### Input/Output Logic

The display takes two input bits (`S(0)` and `S(1)`) and uses Boolean logic to control the seven segments (`a` to `g`) of the display. Each input combination corresponds to a specific character being displayed by lighting up the appropriate segments.

#### Truth Table

| `S(1)` | `S(0)` | Segment `a` | Segment `b` | Segment `c` | Segment `d` | Segment `e` | Segment `f` | Segment `g` |
|--------|--------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|
|   0    |   0    |      1      |      1      |      1      |      1      |      1      |      1      |      0      |
|   0    |   1    |      0      |      1      |      1      |      0      |      0      |      0      |      0      |
|   1    |   0    |      1      |      1      |      0      |      1      |      1      |      0      |      1      |
|   1    |   1    |      1      |      1      |      1      |      1      |      0      |      0      |      1      |

### Karnaugh Map (K-Map) Optimization

For each segment (a-g), a Boolean expression was derived using K-maps to minimize the logic needed for implementation. Here's an example of how segment `a` was determined using Boolean algebra:

1. **Truth Table**:
   - Segment `a` is on for the following inputs: `S(1) = 0`, `S(0) = 0`; `S(1) = 1`, `S(0) = 0`; and `S(1) = 1`, `S(0) = 1`.

2. **Karnaugh Map**:

| S(1) \ S(0) | 0 | 1 |
|-------------|---|---|
| **0**       | 1 | 0 |
| **1**       | 1 | 1 |


The Boolean expression for `a` after K-map simplification:  
`a = S(1) OR NOT S(0)`

### Boolean Expressions for Each Segment

- `a = S(0) AND NOT S(1)`
- `b = S(0) XOR S(1)`
- `c = (NOT S(1) AND NOT S(0)) OR (NOT S(0) AND S(1)) OR (S(1) AND S(0))`
- `d = S(0) XOR S(1)`
- `e = S(0) AND NOT S(1)`
- `f = S(0) AND NOT S(1)`
- `g = S(0) AND S(1)`

## Basys 3 FPGA Implementation

The project was implemented using the Basys 3 FPGA board and Vivado software. The Boolean logic was written in VHDL, synthesized, and then programmed onto the FPGA to display alphanumeric characters on a 7-segment display.

### Code Example (VHDL)

```vhdl
entity final_epic is
Port ( S : in  STD_LOGIC_VECTOR (1 downto 0);
       a : out STD_LOGIC;
       b : out STD_LOGIC;
       c : out STD_LOGIC;
       d : out STD_LOGIC;
       e : out STD_LOGIC;
       f : out STD_LOGIC;
       g : out STD_LOGIC);
end final_epic;

```

### Boolean Expressions for Each Segment

```vhdl
architecture Behavioral of final_epic is
begin

- `a = S(0) AND NOT S(1)`
- `b = S(0) XOR S(1)`
- `c = (NOT S(1) AND NOT S(0)) OR (NOT S(0) AND S(1)) OR (S(1) AND S(0))`
- `d = S(0) XOR S(1)`
- `e = S(0) AND NOT S(1)`
- `f = S(0) AND NOT S(1)`
- `g = (S(0) AND NOT S(1)) OR (S(1) AND S(0))`

end Behavioral;
```

### Constraints:

To map the logic to the Basys 3 board, the following constraints were used:

**\#\#7 Segment Display**:
```vhdl
set_property PACKAGE_PIN W7 [get_ports {a}]
set_property IOSTANDARD LVCMOS33 [get_ports {a}]
set_property PACKAGE_PIN W6 [get_ports {b}]
set_property IOSTANDARD LVCMOS33 [get_ports {b}]
set_property PACKAGE_PIN U8 [get_ports {c}]
set_property IOSTANDARD LVCMOS33 [get_ports {c}]
set_property PACKAGE_PIN V7 [get_ports {d}]
set_property IOSTANDARD LVCMOS33 [get_ports {d}]
set_property PACKAGE_PIN U5 [get_ports {e}]
set_property IOSTANDARD LVCMOS33 [get_ports {e}]
set_property PACKAGE_PIN V5 [get_ports {f}]
set_property IOSTANDARD LVCMOS33 [get_ports {f}]
set_property PACKAGE_PIN U7 [get_ports {g}]
set_property IOSTANDARD LVCMOS33 [get_ports {g}]
```

**\#\#Switches**:
```vhdl
set_property PACKAGE_PIN V17 [get_ports {S[1]}]
set_property IOSTANDARD LVCMOS33 [get_ports {S[1]}]
set_property PACKAGE_PIN V16 [get_ports {S[0]}]
set_property IOSTANDARD LVCMOS33 [get_ports {S[0]}]
```
## DIY Alternative: Building at Home without an FPGA

If you don't have access to a Basys 3 FPGA, you can still experiment with this project using simple hardware components like LEDs, switches, and logic gates.

### Steps:

1. **Create a Circuit**:  
   Use LEDs to represent each segment of the 7-segment display (`a`-`g`) and switches to control the input bits (`S(0)` and `S(1)`).

2. **Build the Logic**:  
   Using basic logic gates (AND, OR, NOT, XOR), implement the Boolean algebra expressions for each segment. For example, use an AND gate to control segment `a` based on the expression `S(0) AND NOT S(1)`.

3. **Test the Display**:  
   Toggle the switches to simulate different input combinations, and observe how the LEDs light up to form different alphanumeric characters.

### Components Needed:

- 7 LEDs (for segments `a`-`g`)
- 2 switches (for inputs `S(0)` and `S(1)`)
- Logic gates (AND, OR, NOT, XOR)
- Breadboard and wires

## Conclusion

This project illustrates how Boolean algebra can be applied to control a 7-segment display. By optimizing the logic with Karnaugh maps and implementing the design on an FPGA, we can efficiently control the segments to display characters. This method can be extended to other projects and replicated using simple hardware for learning purposes.

## Author

**Edward Del Pino**

*June 2024*

- [LinkedIn](https://www.linkedin.com/in/edward-del-pino)
- [GitHub](https://github.com/DelPineAI)
- [Instagram](https://www.instagram.com/edwarddelpiiino/)
