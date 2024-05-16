# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

# APPARATUS REQUIRED:

Vivado 2023.1

# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.


**LOGIC DIAGRAM**

# SR FLIPFLOP

![301740946-77fb7f38-5649-4778-a987-8468df9ea3c3](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/4e11d72e-7401-4fa7-9e17-977a8e5c056a)

# JK FLIPFLOP

![301743103-1510e030-4ddc-42b1-88ce-d00f6f0dc7e6](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/20ec58e1-ff7d-48ad-896f-325fd15b9978)

# T FLIPFLOP

![301743290-7a020379-efb1-4104-85ee-439d660baa08](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/f59a93a1-c4a1-4f0d-b8ec-59afae83aaba)


# D FLIPFLOP

![301743389-dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/061329ff-7ea8-4011-88a0-a346b84b7329)

# COUNTER

![301743514-a1fc5f68-aafb-49a1-93d2-779529f525fa](https://github.com/Jayanth-T/VLSI-LAB-EXP-4/assets/106177371/48d8dfc6-1504-43fc-8178-4baca02ac055)


# VERILOG CODE:

# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```
# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# MOD 10 Counter
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
UP-DOWN COUNTER

VERILOG CODE:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

# OUTPUT WAVEFORM:

# D Flip Flop

![324386856-c69130e3-a98b-4e74-8d93-00fd9a28adee](https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/1594f4d7-8e42-43ca-9cc0-f8dbebdd367f)

<img width="962" alt="324386882-8dcd27b3-b314-44e0-98b3-4ca014a3f29f" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/656845cc-29e9-48d0-b2d7-d510d921ee6c">

# JK Flip Flop

![324387028-9ac25e31-d982-4048-801f-34c8e60e4a15](https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/02ef104f-8e85-4ec2-a6ea-2b24dd40eabf)


<img width="962" alt="324387069-db0d3db0-bc32-4390-b6f7-9e73cb218cd8" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/7a065d7c-9898-4c7f-88d3-3357386ce2e0">


# SR Flip Flop

![324387177-0d97e53a-3527-4823-b4ab-38272498b06c](https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/b2267d45-902d-4e3f-9569-e98b50cfee9f)

<img width="962" alt="324387220-d11d0554-21eb-4149-b27c-2cfc51b85b42" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/bea76a0e-4ef9-48b5-954a-c88ec757408a">


# T Flip Flop

![324387340-8efaa494-0b44-47b6-ad6e-91cea49a5587](https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/e37658b4-49e8-417f-afcb-03c3e1f20b39)

<img width="962" alt="324387396-c7c6823d-c6d0-4f28-b517-85b10bbd58b1" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/6d52d36b-f685-416e-85d6-7faad0c8aee3">


# MOD-10 Counter

<img width="962" alt="324387552-d3e95591-8f66-43c6-883f-2db39ae45171" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/f3a3b9bc-9645-4ce1-91bf-65237fdd5b93">

<img width="962" alt="324387589-3617b0e2-e8e2-4b09-bbd2-9f41a2e7daab" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/01931e66-6c86-4542-86a8-100f296cd0e4">


# Ripple Carry Counter

<img width="962" alt="324387701-d54c5740-b120-4b02-a412-9c9e99b59a37" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/21a39d4e-fd2d-43bb-955e-78c6781c53bd">


<img width="962" alt="324387746-526b194a-682f-4dc9-af1f-38d8ac487508" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/f01225a9-b09b-4a7e-a9ae-b50cbe80c779">


# UP Down Counter

<img width="617" alt="324387870-22c82bbc-4741-4d42-a438-598b1bcab13c" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/3988b689-eaa0-4ef2-8a4d-c0c035f5c232">

<img width="962" alt="324387907-6e3117fd-23a2-4993-bf44-c2db45b62240" src="https://github.com/Jestus27/VLSI-LAB-EXP-4/assets/167751233/5dc92778-9179-41f6-b14d-37740f2cb1c8">


# RESULT:
Hence thus given To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado
