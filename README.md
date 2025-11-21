# Seven-Segment Display Driver using Verilog HDL

## Aim  
To design and simulate a Verilog HDL seven-segment display driver that converts a 4-bit binary input into the corresponding digits 0–9.
 
## Apparatus Required  
- **Vivado 2023.1**
- **Spartan 7 FPGA**  

## Procedure  

## 1. Launch Vivado 2023.1
- Open Vivado 2023.1 and create a new project.
- Select **RTL Project** and enable **Do not specify sources at this time**.

## 2. Create Verilog Design File
- Create a new Verilog design file.
- Type the Verilog code for the Seven Segment Display.
- The code should convert a 4-bit input into the corresponding seven-segment output.

## 3. Create Constraint File
- Create a new XDC constraint file.
- Assign the FPGA pins for input switches, output segments, and the common anode/cathode according to the Real Digital Boolean Board (XC7S50CSGA324-1) pin mapping.

## 4. Synthesize the Design
- Click on **Run Synthesis** to check for design correctness.
- Ensure there are no syntax or mapping errors.

## 5. Implement the Design
- After successful synthesis, click on **Run Implementation**.
- Verify timing and pin placement in the implementation summary.

## 6. Generate Bitstream
- Click **Generate Bitstream** to create the programming file.
- Wait for the process to complete.

## 7. Program the FPGA
- Connect the Boolean Board to your PC.
- Open **Hardware Manager**, click **Open Target → Auto Connect**, and program the device with the generated bitstream.

## 8. Observe the Output
- Use the 4-bit DIP switches to provide binary inputs.
- Observe the Seven Segment Display showing the corresponding digits 0–9.

---
## Logic Diagram

<img width="589" height="511" alt="bcd2 7 segment" src="https://github.com/user-attachments/assets/e6922e13-6ec0-4f40-87ec-47be8862204d" />


## Verilog Code for Seven-Segment Display  

```verilog
module bcd_to_7segment(
    input  [3:0] bcd,
    output reg [6:0] seg,
    output reg [3:0] an
);

always @(*) 
begin
    an <= 4'b1110;
    case (bcd)
        4'b0000: seg = 7'b1000000;
        4'b0001: seg = 7'b1111001;
        4'b0010: seg = 7'b0100100;
        4'b0011: seg = 7'b0110000;
        4'b0100: seg = 7'b0011001;
        4'b0101: seg = 7'b0010010;
        4'b0110: seg = 7'b0000010;
        4'b0111: seg = 7'b1111000;
        4'b1000: seg = 7'b0000000;
        4'b1001: seg = 7'b0010000;
        default: seg = 7'b1111111;
    endcase
end

endmodule

```
## Constraint file for Seven-Segment Display
```
## DIP SWITCHES (SW0-SW3 for BCD input)
set_property -dict { PACKAGE_PIN V2 IOSTANDARD LVCMOS33 } [get_ports {bcd[0]}]
set_property -dict { PACKAGE_PIN U2 IOSTANDARD LVCMOS33 } [get_ports {bcd[1]}]
set_property -dict { PACKAGE_PIN U1 IOSTANDARD LVCMOS33 } [get_ports {bcd[2]}]
set_property -dict { PACKAGE_PIN T2 IOSTANDARD LVCMOS33 } [get_ports {bcd[3]}]

## 7-SEGMENT DISPLAY (a,b,c,d,e,f,g,dp)
set_property -dict { PACKAGE_PIN D7 IOSTANDARD LVCMOS33 } [get_ports {seg[0]}]
set_property -dict { PACKAGE_PIN C5 IOSTANDARD LVCMOS33 } [get_ports {seg[1]}]
set_property -dict { PACKAGE_PIN A5 IOSTANDARD LVCMOS33 } [get_ports {seg[2]}]
set_property -dict { PACKAGE_PIN B7 IOSTANDARD LVCMOS33 } [get_ports {seg[3]}]
set_property -dict { PACKAGE_PIN A7 IOSTANDARD LVCMOS33 } [get_ports {seg[4]}]
set_property -dict { PACKAGE_PIN D6 IOSTANDARD LVCMOS33 } [get_ports {seg[5]}]
set_property -dict { PACKAGE_PIN B5 IOSTANDARD LVCMOS33 } [get_ports {seg[6]}]
set_property -dict { PACKAGE_PIN A6 IOSTANDARD LVCMOS33 } [get_ports {seg[7]}]

## ANODE CONTROL (active-low)
set_property -dict { PACKAGE_PIN D5 IOSTANDARD LVCMOS33 } [get_ports {an[0]}]
set_property -dict { PACKAGE_PIN C4 IOSTANDARD LVCMOS33 } [get_ports {an[1]}]
set_property -dict { PACKAGE_PIN C7 IOSTANDARD LVCMOS33 } [get_ports {an[2]}]
set_property -dict { PACKAGE_PIN A8 IOSTANDARD LVCMOS33 } [get_ports {an[3]}]
```
## FPGA Implementation Output

<img width="782" height="540" alt="image" src="https://github.com/user-attachments/assets/6d549830-34b0-4916-9370-fc680e71f881" />


---

## Conclusion
In this experiment, a seven-segment display driver was successfully implemented using Verilog HDL in FPGA.This experiment demonstrates the practical application of Verilog HDL in designing and controlling digital hardware components, highlighting its importance in developing reliable and efficient digital systems.
