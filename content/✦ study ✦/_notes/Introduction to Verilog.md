### Key Concepts
- **Define Verilog**
	- hardware description language (HDL) that can be used to simulate and synthesize hardware designs
		- Simulation --> analyze functional and timing behaviour of hardware design
		- Synthesis --> converts hardware design into form for physical implementation of device
	- *Why the name?:* Verilog = Veri-fication + Log-ic
- **What are the levels of modelling abstraction?**
	1. Transistor level
		- continuous time/signals; transistor is modelled by resistor-capacitor network 
	2. Switch level
		- continuous time; continuous/discrete voltage; linear equations define models
	3. Gate level
		- continuous time; discrete voltage; transistors grouped into gates
	4. **Register Transfer level**
		- discrete time (i.e. clock cycle); hardware is modelled as assignment to registers driven by combinational circuits
	5. Transaction level
		- transfers data over a bus with building blocks of processors, controllers etc.
	6. Electronic System level
		- models entire system including hw/sw
- **What is a LUT3?**
	- Three-input lookup table that produces a single output
		- Lookup tables are small ROMs that can be preconfigured to implement any output function of a small number of inputs
	- A larger version of this can be represented by a ROM
- **What is a BUFG?**
	- Inferred for all clock signals; ensures that all signal is routed in a way that signal can be used as a clock signal
- **Explain how simulation timing is inferred in Verilog?**
	- The following compiler directive is at top of simulation testbench file: `timescale 1ns/1ps`
	- It specifies the time unit and precision for modules that follow it: `timescale <time unit>/<time_precision>`
		- time_unit: measurement of delays and simulation time
		- time_precision: how delay values are rounded during simulation
	- Limited to 1, 10, 100; units from seconds to femtoseconds
	- Verilog uses discrete-event simulation to determine steady-state behavior of h.w. designs
		- A discrete-event simulator models operation of system using sequence of events
			- events represent a change in value in model at a specific time
		- Efficient for simulating designs of hardware
- **Explain the stratified event queue**
	- Responsible for storing pending events until they have been processed
	- It stores the following types of events
		- Active events
			- Includes activities such as:
				- blocking assignments
				- evaluation of R.H.S of non-blocking assignment
				- continuous assignment
				- $display command execution
				- evaluation of inputs and changing outputs of primitives
			- never update one signal in two procedural blocks with blocking assignments
			- active events can be removed from queue
		- Inactive events
			- Type of blocking assignment with 0 time unit delay
				- avoids a race condition; schedules assignment later
		- Non-blocking assignment events
			- Update the left hand side of a non-blocking assignment using previously computed right hand side values
			- copy of value in active event
		- Monitor events
			- execute $monitor and $strobe commands (similar to display except output values represent state of system at end of current simulation time step)
		- Future events
			- event schedule for a future step; delayed assignments are future events
			- they will become active events as time progresses
- **What is the difference between discrete-event vs continuous?**
	- In discrete-time simulation, time step is not fixed
		- when current simulation time step ends, time advances to time of next scheduled event
		- changes to inputs observed as they occur
	- in continuous simulation, time step is fixed
		- changes to state is evaluated at fixed intervals of time
		- changes to inputs will be observed when next time step starts
### Code (Cheat Sheet)
##### **Modules**
Blocks of verilog code that encapsulates functionality
- Used to describe 
	1. Top-level hardware designs
	2. Hardware subsystems and components
	3. Simulation testbenches
###### **Syntax**
```systemverilog
module <name> (
  [port list]
);
// contents of the module
endmodule
```
###### **Example**
```systemverilog
module AND_gate (
	input a, 
	input b,
	output out
);
	assign out = a & b;
endmodule
```
##### **Ports**
- Signals that act as inputs and outputs to a module
- Not required in test bench since module drives signals internally;
###### **Syntax**
- Three port types can be used
	- Input 
	- Output
	- Inout --> bidirectional port
##### **Test bench**
###### **Syntax**
```systemverilog
module ModuleTB (
	input i1,
	input i2,
	output reg o1
)

	initial 
	begin
		$monitor ($time, " ns a=%b, b=%b, out=%b", i1, i2, o1);
			o1 = 0;
		#10 o1 = 1;
		$finish
	end
endmodule

module TB;
	wire i1, i2, o1;
	Module u1 (i1, i2, o1);
	ModuleTB u2 (i1, i2, o1);
endmodule
```

Outputs should be defined as reg since they are driven by a procedural block
##### **Identifiers**
- Used for signal names, port names, and module names
###### **Syntax**
- Can not start with $ or a digit
- Only two non-alphanumeric character allowed: underscores `_` and dollar signs `$`
- Case-sensitive
##### **Numbers**
- Binary, octal, decimal or hexadimal
###### **Syntax**
`[size]'[base_format][number]`
###### **Examples**

| formatted number in verilog | value                      |
| --------------------------- | -------------------------- |
| 4'b1010                     | $(1010)_2$                 |
| 6'o27                       | $(27)_8$                   |
| 1024                        | $(1024)_{10}$              |
| 8’b10101111                 | $(10101111)_2$             |
| 8’b1010_1111                | $(10101111)_2$             |
| 8’hAF                       | $(AF)_{16}$                |
| 32’hF                       | $(0000000F)_{16}$          |
| 1’bz                        | Z (impedance)              |
| -6’d5                       | $5_{10}$; two's complement |

##### **Operators**
###### **Syntax**
![[Verilog Operators.png]]
##### **Keywords**
###### **Syntax**
![[Verilog Keywords.png]]
##### **Datatypes**
- Net datatypes represent physical connection between two entities such as "wires"
	- As a scalar --> single wire; as a vector --> bus of wires
	- Defaults to wire; need to specify `reg` otherwise
	- Note; there are other net datatypes
		- `wand`: wired-AND connection
		- `wor`: wired-OR connection
		- `supply0`: connect to Logic 0 of power supply
		- `supply1`: connect to Logic 1 of power supply
- Variable datatypes represent assigned data values and store information for a module
	- As a scalar and vector --> reg represents n bits of data
		- all procedural block outputs are reg datatypes
	- other variable datatypes,
		- integer datatype represents 32 bit integers
		- real datatype represents real numbers i.e. floating point
		- realtime datatype represents time using real numbers
		- time datatype represents sim. time
- Note about nets and variables: Reg can not be driven with an assign statement, only in procedural blocks (like initial and always)
- Data values are either 0, 1, X or Z
	- uninitialized net has value of Z
	- uninitializes variable has value of X
- Ordering of inputs has no effect on performance.
##### **Procedural Blocks**
Represent an independent model of control; two types exist:
- Initial procedural block executes only once 
- Always procedural block continuously executes
Sensitivity List describes when always block starts execution 
- Includes a signal edge i.e. `posedge`, `negedge` and signal which triggers the block's execution
- If there are no lists,
	- creates a combinational circuit to work with; OR infers a latch to store data
	- Latch interference is undesired side-effect of failing to consider all input combinations
		- default case and else clause can be used to avoid this
##### **Assignments**
- A blocking assignment uses = assignment operator
	- copies the r.h.s to l.h.s at time of execution
- A non-blocking assignment uses <= assignment operator
	- all assignments happen concurrently at one instance in time
	- for edge-triggered sequential logic!
- The order of it does not matter.
###### **Example**
```systemverilog
module AssignmentExample1(  
	input i1,  
	input clk,  
	output reg [3:0] o1,  
	output reg [3:0] o2  
);  
	initial o1 = 4'b0000;  
	initial o2 = 4'b0000;  
	// o1 uses blocking assignments  
	always @(posedge clk)  
	begin  
		o1[0] = i1;  
		o1[1] = o1[0];  
		o1[2] = o1[1];  
		o1[3] = o1[2];  
	end  
	// o2 uses non-blocking assignments  
	always @(posedge clk)  
	begin  
		o2[0] <= i1;  
		o2[1] <= o2[0];  
		o2[2] <= o2[1];  
		o2[3] <= o2[2];  
	end  
endmodule
```

##### **Case Statements**
There are three types of case statements:
1. case: standard case format
2. casez: case statement that treats Z and ? in case items as don't care values
3. casex: case statement that treats Z, X and ? in case items as don't care values
###### **Syntax**
```systemverilog
case(expression)
	case_item_1:
		case_statement_1;
	default:
		case_statement_default;
```
##### **Generate Blocks**
Allows to instantiate modules in a loop to save time; example of utility when creating a 8-bit module of individual modules
###### **Syntax**
```systemverilog
genvar i;
generate
	for (i = x; i < y; i = i + 1)
	begin: block_name
		// declare instance in terms of i
	end
endgenerate
```

##### **Testbench**
Piece of code that is used to test out another piece of code; 
- Simply a module that drives the inputs to another module and monitors the outputs
###### **Syntax**
- `$monitor`: outputs a message when value of one arguments changes
- `$time`: outputs current simulation time
- `$display`: output a message at any time
- `$timeformat`: system function that sets the default formatting of times output during simulation runs
	- `$timeformat (<unit format>, <precision>, <suffix string>);`
		- unit number = -6 for us, -9 for ns, -12 for ps
		- precision is number of decimal places
		- suffix string is text string to follow output of time
###### **Example**
```systemverilog
module HelloWorld;
	initial
	begin
		$display("Hello World");
		$finish;
	end
endmodule
```

### Example Problems
1. Create a 1-bit full adder module that computes the sum and carry out for three input bits; create a testbench stimulus
2. Create a 4:2 Mux with procedural blocks given inputs of a, b, sel, and c (Slide 90)
	- Write a testbench to monitor changes and connect it to module
3. Provide a synthesizable DFFE Example (Slide 97)
4. How to create a periodic clock signal? [[clk|Generate Clock Signals]]
5. Build a 4:1 mux using a case statement with testbench
6. Create a priority encoder with `?` symbol in cases
7. Create a 8 bit adder using full adders with testbench


