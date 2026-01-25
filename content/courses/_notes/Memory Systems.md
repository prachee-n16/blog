There are various types of memory systems, with some common examples:
- Registers are high-speed access memory area limited to saving a single word at a time
- Register files, commonly used with processors to build simple storage structures e.g. queues to track multiple values.
	- The capacity is still small, with high-speed access
- SRAM (Static Random Access Memory); It has low latency, small capacity and expensive
- DRAM (Dynamic Random Access Memory); It has high latency, large capacity and cheap
- SDRAM (Synchronous DRAM); It has high latency with burst support and cheap

Some memory support a single address at a time (single-ported) while others support two addresses at a time (dual-ported). 
- A simple dual port RAM has two ports, but the design is restricted to reading from one address and writing to one address
- A true dual port has two ports that allow for reading and writing from both ports simultaneously (bidirectional)
There can be more than one port, where one port = writing and other two ports = reading

How to implement 1 KiByte Memory in Verilog? i.e. organized as 256 x 32 bits
```systemverilog
module MB #(
	parameter [31:0] ADDRWIDTH=8,
	parameter [31:0] DATAWIDTH=32,
)
(
	input clk,
	input rst,
	input we,
	// This is an vector, a collection/bus of wires that represent the 
	// write address
	input [ADDRWIDTH - 1:0] wraddr,
	input [ADDRWIDTH - 1:0] rdaddr,
	input [DATAWIDTH - 1:0] wrdata,
	output reg [DATAWIDTH - 1:0] rddata,
);
	// Defines an array of vectors
	// i.e. 256 rows of vectors 31:0
	reg [DATAWIDTH - 1:0] mem[(2 ** ADDRWIDTH) - 1:0];

	always@(posedge clk) begin
		if(rst)
		begin
			// when reset, initialize all memory locations to 0
			// this code is not synthesizable. It can not assign these values to 256 locations in 1 clock period.
			`ifndef SYNTHESIS
			for (i = 0; i <= 2 ** ADDRWIDTH - 1; i = i + 1)
			begin
				mem[i] <= 0;
			end
			`endif
			rddata <= 0;
		end
		else
		begin
			if(we)
			begin
				mem[wraddr] <= wrdata;
			end
			rddata <= mem[rdaddr];
		end
	end
	integer i;
```

The elaborated design will introduce a latency as it registers the outputs since non-blocking assignments are being used.

To implement a multi-ported memory system, we implement two memories
- when writing a value, we update both memories by writing data to same address in both memories
- when reading a value, we can pass different read addresses which won't be shared across two memories. Since the data is same in both blocks, we can read from either block

Variation in Verilog will 
```systemverilog
...
begin
	if(we)
	begin
		mem0[wraddr] <= wrdata;
		mem1[wraddr] <= wrdata;
	end
	rddata0 <= mem0[rdaddr0];
	rddata1 <= mem1[rdaddr1];
end
```
