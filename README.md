# 1. 4 Bit Adder functionality verification

**Aim:**

To write a verilog code for 4bit adder and verify the functionality using Test bench.<br>

&emsp;&emsp;Write Verilog Code<br>

&emsp;&emsp;Verify the Functionality using Test-bench.<br>

**Tool Required:**

&emsp;&emsp;Functional Simulation: nclaunch Simulator (nclaunch) <br>

**4-bit Adder Design:**

&emsp;&emsp;To construct a 4-bit adder, need to chain together four 1-bit full adders. Each full adder computes the sum and carry for one bit of the two numbers. The carry-out from one adder feeds into the carry-in of the next adder in the sequence. This process adds the two 4-bit numbers bit by bit, with the carry propagating through each stage, resulting in a final sum and carry-out at the end.<br>

&emsp;&emsp;To design a 1-bit full adder, the first step is to create a truth table that represents all possible combinations of the inputs (A, B, and CIN) and the corresponding outputs (Sum(S) and COUT).<br>

![image](https://github.com/user-attachments/assets/716a26b6-a449-42e0-9e2d-cdbaa4b291b9)

Here’s the truth table for a 1-bit full adder:

![tt](https://github.com/user-attachments/assets/0b3ab24f-1d7e-4a01-80ce-5e7406f4082b)

**Fig 1 : Diagram and truth table of full adder**

**Logic Expressions:**

1.	Sum (S):
   
&emsp;&emsp;S=A⊕B⊕CIN

&emsp;&emsp;Where ⊕ represents XOR.

3.	Carry out (COUT):
   
&emsp;&emsp;COUT=(A&B) | (CIN&(A^B))

![image](https://github.com/user-attachments/assets/7d6fa554-2614-4f19-aa68-65c9e6153caa)

**Fig 2:Diagram of 4 Bit Adder**

**Creating Source Codes**

&emsp;&emsp;In the Terminal, type gedit <filename>.v (ex: gedit 4bitadder.v). <br>

&emsp;&emsp;A Blank Document opens up into which the following source code can be typed down. <br>

&emsp;&emsp;Note : File name should be with HDL Extension<br>

**a) Verify the Functionality**

&emsp;&emsp;Three Codes shall be written for implementation of 4-bit Adder as follows, <br>

&emsp;&emsp;&emsp;&emsp;fa.v → Single Bit 3-Input Full Adder [Sub-Module / Function] <br>

&emsp;&emsp;&emsp;&emsp;fa_4bit.v → Top Module for Adding 4-bit Inputs. <br>

&emsp;&emsp;&emsp;&emsp;fa_4bit_test.v → Test bench <br>

### fulladder.v program:-

           module full_adder(A,B,CIN,S,COUT);
           input A,B,CIN;
           output S,COUT;
           assign S=A^B^CIN;
           assign COUT=(A&B) | (CIN&(A^B));
           endmodule

### 4bit fulladder.v program:-


             module fulladd_4bit(A,B,C0,S,C4);
             input [3:0] A,B;
             input C0;
             output [3:0] S;
             output C4;
             wire C1,C2,C3;
             full_adder fa0 (A[0],B[0],C0,S[0],C1);
             full_adder fa1 (A[1],B[1],C1,S[1],C2);
             full_adder fa2 (A[2],B[2],C2,S[2],C3);
             full_adder fa3 (A[3],B[3],C3,S[3],C4);
             endmodule

### 4bit fulladder test.v program:-

           module test_4bit;
           reg [3:0] A;
           reg [3:0] B; reg C0;
           wire [3:0] S; wire C4;
           fulladd_4bit dut (A,B,C0,S,C4);
           initial
           begin
           A=4'b0011;B=4'b0011;C0=1'b0;
           #10; A=4'b1011;B=4'b0111;C0=1'b1;
           #10; A=4'b1111;B=4'b1111;C0=1'b1;
           #10;
           end initial
           #50 $finish;
           endmodule

**Functional Simulation:**

&emsp;&emsp;Invoke the cadence environment by type the below commands <br>

&emsp;&emsp;tcsh (Invokes C-Shell) <br>

&emsp;&emsp;source /cadence/install/cshrc (mention the path of the tools) <br>

&emsp;&emsp;```(The path of cshrc could vary depending on the installation destination)<br>```
      
&emsp;&emsp;After this you can see the window like below <br>

![WhatsApp Image 2024-11-24 at 19 24 53_b041e45a](https://github.com/user-attachments/assets/dc96c1a0-9ca2-447d-971d-aa95c9b99b4f)


**Fig 3:Invoke the Cadence Environment**

&emsp;&emsp;To Launch Simulation tool <br>

&emsp;&emsp;&emsp;&emsp;linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design <br>

&emsp;&emsp;&emsp;&emsp;or<br>

&emsp;&emsp;&emsp;&emsp;linux:/> nclaunch& // On subsequent calls to NCVERILOG <br>

&emsp;&emsp;It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .<br>

![image](https://github.com/user-attachments/assets/ab18e6ba-e831-48dc-ba78-e6038e6f93db)

**Fig 4:Setting Multi-step simulation**

&emsp;&emsp;Select Multiple Step and then select “Create cds.lib File” .<br>

&emsp;&emsp;Click the cds.lib file and save the file by clicking on Save option <br>

![image](https://github.com/user-attachments/assets/e5c7cda9-ea94-4d3f-92c8-b32fea7403c5)

**Fig 5:cds.lib file Creation**

&emsp;&emsp;Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. <br>

&emsp;&emsp;Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .<br>

&emsp;&emsp;&emsp;&emsp;We are simulating verilog design without using any libraries <br>

&emsp;&emsp;&emsp;&emsp;A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure <br>

![image](https://github.com/user-attachments/assets/781b297a-11e9-4140-89c5-ee3b0d15bbd4)

**Fig 6: Selection of Don’t include any libraries**

&emsp;&emsp;A ‘NCLaunch window’ appears as shown in figure below <br>

&emsp;&emsp;Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. <br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .<br>

&emsp;&emsp;To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. <br>

![WhatsApp Image 2024-10-05 at 9 31 03 AM](https://github.com/user-attachments/assets/74fd48ce-d8d0-4f76-9fdf-e47e41d12ff2)

**Fig 7: Nclaunch Window**

**Step 1: Compilation:– Process to check the correct Verilog language syntax and usage**

&emsp;&emsp;Inputs: Supplied are Verilog design and test bench codes <br>

&emsp;&emsp;Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file <br>

**Steps for compilation:**

&emsp;&emsp;1. Create work/library directory (most of the latest simulation tools creates automatically) <br>
&emsp;&emsp;2. Map the work to library created (most of the latest simulation tools creates automatically) <br>
&emsp;&emsp;3. Run the compile command with compile options <br>
&emsp;&emsp;i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v<br>

&emsp;&emsp;Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code <br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation<br>

![WhatsApp Image 2024-10-05 at 9 31 03 AM](https://github.com/user-attachments/assets/16300ea2-63ce-4be2-8b50-95781ad3205f)


**Fig 8: Compiled database in worklib**

&emsp;&emsp;After compilation it will come under worklib you can see in right side window<br>

&emsp;&emsp;Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. <br>

&emsp;&emsp;The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”<br>

**Step 2: Elaboration:– To check the port connections in hierarchical design**

&emsp;&emsp;Inputs: Top level design / test bench Verilog codes <br>

&emsp;&emsp;Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file <br>

&emsp;&emsp;Steps for elaboration – Run the elaboration command with elaborate options <br>

&emsp;&emsp;&emsp;&emsp;1.	It builds the module hierarchy <br>
&emsp;&emsp;&emsp;&emsp;2.	Binds modules to module instances <br>
&emsp;&emsp;&emsp;&emsp;3.	Computes parameter values <br>
&emsp;&emsp;&emsp;&emsp;4.	Checks for hierarchical names conflicts <br>
&emsp;&emsp;&emsp;&emsp;5.	It also establishes net connectivity and prepares all of this for simulation<br>
   
&emsp;&emsp;After elaboration the file will come under snapshot. Select the test bench and elaborate it.<br>


![WhatsApp Image 2024-10-05 at 9 31 03 AM](https://github.com/user-attachments/assets/e25db1de-21a4-437b-87eb-45f417f9f803)


**Fig 9: Elaboration Launch Option**

**Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour.**

&emsp;&emsp;Inputs: Compiled and Elaborated top level module name <br>

&emsp;&emsp;Outputs: Simulation log file, waveforms for debugging <br>

&emsp;&emsp;Simulation allow to dump design and test bench signals into a waveform <br>

&emsp;&emsp;Steps for simulation – Run the simulation command with simulator options<br>

![image](https://github.com/user-attachments/assets/4b2514a2-e4a9-4f98-84e8-b1bfe398b4b0)

**Fig 10: Design Browser window for simulation**

![image](https://github.com/user-attachments/assets/31f15463-9623-47e8-84e5-d17e93033884)

**Fig 11: Launching Simulation Waveform WindowSimulation Waveform Window**

![image](https://github.com/user-attachments/assets/979f9be4-250f-4dfd-8baf-5ab2d8202cf2)

**Fig 12: Simulation Waveform Window**


### Result:

the functionality of 4-Bit Adder was successfully verified using a test bench and simulated with the nclaunch tool.













