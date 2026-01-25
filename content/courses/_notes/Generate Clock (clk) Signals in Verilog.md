Approach 1:
```systemverilog
`timescale 1ns/1ps

module TB
	// init clk signal to value of 0 when declared
	reg clk=0;
	// use a parameter to specify desired clock period
	// Define parameters for constant values
	parameter clk_period = 20;
	// implement infinite loop to toggle clk signal value
	// not synthesizable code; just for simulation
	// toggle clk signal after waiting for half a clock period
	always 
		#(clk_period/2) clk=~clk;
endmodule
```

Approach 2: Fixed number of repetitions
```systemverilog
initial
begin
	clk = 1'b0
	repeat(9)
		#(clk_period/2) clk=~clk;
end
```

Approach 3: Infinite Loop Using Forever
```systemverilog
initial
begin
	clk = 1'b0;
	forever
		#clk_period/2 clk=~clk;
end
```