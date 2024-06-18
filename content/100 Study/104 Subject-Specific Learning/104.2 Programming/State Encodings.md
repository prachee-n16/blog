Binary encodings
- this is the naive way of assigning state bits where we don't pay attention to the bits changing i.e. assign the next available binary number
- why is this a problem?
	- every state bit needs to be considered when finding current state
	- state transitions will be slower for more bit number changes
	- for large FSM, this is poor performance
		- number of state bits is $log_2(n)$ where n = total number of states
			- if n is 5 or more, 3 bits are required
- why is this good?
	- minimizes total number of bits required (note: gray coding has same advantage w/o sacrificing performance)
	- for small FSM, this works well: performance b/wn gray coding or one-hot encoding and binary coding is minimal
		- time to decode two bits instead of single bits is negligible AND at most two bits change values
![[FSM_example.png]]

Consider state travel from testbench described in slide:
- 0 reset = 1 so we stay on state 1 
- 20 reset = 0 and d=00 so state 1
- 40 d=00  so state 1
- 60 d = 01 so state 2
- 80 d = 01 so state 3
- 100 d = 01 so state 4
- 120 d = 10 so state 8
- 140 d = 10 so state 8
- 160 d = 00 so state 4
- 180 d = 00 so state 3
- 200 d = 10 so state 7
- 220 d = 10 so state 7
- 240 d = 00 so state 3
- 260 d = 01 so state 4
- 280 d = 01 so state 4
- 300 d = 01 so state 4
- 320 d = 01 so state 4
- 340 d = 01 so state 4

```
begin  
	$timeformat(-9, 0, " ns");  
	$monitor("time=%0t, d=%b, out=%b", $time, d, out);  
	#20 reset=0;  20s
	#40 d=2'b01;  60s
	#60 d=2'b10;  120s
	#40 d=2'b00;  160s
	#40 d=2'b10;  200s
	#40 d=2'b00;  240s
	#20 d=2'b01;  260s
	#80 $finish;  
end
```

Write a FSM for this.
- It is possible in SystemVerilog to use an enumerated type to define the states of a state machine
`typedef enum {Idle, State1, State2, State3} states;`
`states state`

```verilog
module FSM3 (
	input clk,
	input reset,
	input [1:0] d,
	output reg [3:0] out
);

	reg [2:0] state=3'b000;
	parameter State1=3'b000, State2=3'b001, State3=3'b010, State4=3'b011;
	parameter State5=3'b100, State6=3'b101, State7=3'b110, State8=3'b111;
	always@(posedge clk, posedge reset)
	begin
		if (reset)
			state <= State1;
		else
			case(state)
				State1:
					begin
						case(d)
							2'b00: state <= State1;
							2'b01: state <= State2;
							2'b10: state <= State5;
							default: state <= State1;
					endcase
						out <= 4'b0001;
				State2: //correct
					begin
						case(d)
							2'b00: state <= State1;
							2'b01: state <= State3;
							2'b10: state <= State6;
							default: state <= State2;
					endcase
						out <= 4'b0010;
				State3: //correct
					begin
						case(d)
							2'b00: state <= State2;
							2'b01: state <= State4;
							2'b10: state <= State7;
							default: state <= State3;
					endcase
						out <= 4'b0011;
				State4: //correct
					begin
						case(d)
							2'b00: state <= State3;
							2'b10: state <= State8;
							default: state <= State4;
					endcase
						out <= 4'b0100;
				State5:
					begin //correct
						case(d)
							2'b00: state <= State1;
							default: state <= State5;
					endcase
						out <= 4'b1001;
				State6:
					begin
						case(d)
							2'b00: state <= State2;
							default: state <= State6;
					endcase
						out <= 4'b1010;
				State7:
					begin
						case(d)
							2'b00: state <= State3;
							default: state <= State7;
					endcase
						out <= 4'b1011;
				State8:
					begin
						case(d)
							2'b00: state <= State4;
							default: state <= State8;
					endcase
						out <= 4'b1100;
	end
```

Gray Coding
- improves binary encoding by ensuring only one state bit changes as state transitions occur
- if states transition to more than two other states, gray coding needs intermediate states.
	- degrade performance of FSM in a synchronous system
- if feasible, gray coding improves by ensuring one state bit changes value
	- leads to faster state transitions --> improved performance

One hot encoding
- uses more state bits to allow easy detection of current states
	- before we examined all state bits; if we assume only 1 bit is active, current bit is determined by 1 bit
		- all 0's for idle state
	- best variation is use 1 to indicate every possible state so, # of states = # of state bits
- disadvantages: there are many state bit combinations that are never used
	- 8 state means 8 valid states and 248 invalid
- good for Finite state machines with complicated state transitions AND less regular the state transitions, the better

Worst negative slack = measure of difference between clock period and processing time.
- A worst negative slack of 18.215 ns with a 20 ns clock period tells us that the processing of the state machine requires approximately 1.785 ns to complete

Note:
FSM outputs appear one cycle after a state change due to the registering of the outputs. In the first clock period, state changes and then output reflects state change on second clock period. How to make this faster?
- outputs can be predicted by considering the current state and the inputs

