Resources to learn Verilog:
- [Verilog Tutorial for Beginners](https://www.chipverify.com/verilog/verilog-tutorial)
- [SystemVerilog Tutorial](https://www.chipverify.com/systemverilog/systemverilog-tutorial): Modern extension to Verilog. 
- [HDLBits](https://hdlbits.01xz.net/wiki/Main_Page): LeetCode setup

ASIC and FPGA:
- https://www.youtube.com/watch?v=78MBLqm0OAQ
- Tiny Tapeout?

***Questions***
- What do you call languages that need statements to end with ;?
- Review ANSI Syntax? 

**Problem 1:** Build a circuit with no inputs and one output. That output should always drive 1 (or logic high).

```systemverilog
module top_module (output one);
	assign one = 4'b1;
	// Alternatively, they recommend the below line
	assign real_one = 1'b1
endmodule;
```
What's the warning message here with 4 vs 1? It's truncating the top bits which is an issue?

**Problem 2:** Build a circuit with no inputs and one output that outputs a constant 0
Same as above, just no hints. There is a note on syntax: HDLBits uses 2001 ANSI-style port declaration syntax since easier to read and removes typos. 
```systemverilog
module top_module ( zero );
    output zero;
    // Verilog-1995
endmodule

module top_module ( output zero ); 
    // Verilog-2001
endmodule
```

**Problem 3:** Create a module with one input and one output that behaves like a wire.
- Wires are directional so information flows from a source (also called driver that drives a value onto a wire) to the sinks
	- So, when we assign, value of signal on right is driven onto to wire on left; it's a continuous assignment so even if values change, it's driven onto it.
- Ports in module have a direction (input, driven into and output, driven out of)
```systemverilog
module top_module( input in, output out );
	assign out = in;
endmodule
```

**Problem 4:** Create a module with 3 inputs and 4 outputs that behaves like wires that makes these connections:
a -> w
b -> x
b -> y
c -> z
- The order in which they appear does not matter; assignments are not copying values over but describing connections between things.
- Note, input and output wires already exist i.e. `input wire a` is same as `input a`
```systemverilog
module top_module( 
    input a,b,c,
    output w,x,y,z );
    assign w = a;
    assign x = b;
    assign y = b;
    assign z = c;

endmodule
```

**Problem 5:** Create a module that implements a NOT gate.
```systemverilog
module top_module( input in, output out );
	assign out = ~in;
endmodule
```

**Problem 6:** Create a module that implements an AND gate.
```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
	assign out = a & b;
endmodule
```

**Problem 7:** Create a module that implements a NOR gate.
```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    assign out = ~(a|b);
endmodule
```

**Problem 8:** Create a module that implements an XNOR gate.
```systemverilog
module top_module( 
    input a, 
    input b, 
    output out );
    assign out = (a&b)|(~a&~b);
endmodule
```

**Problem 9:** Implement this
![](https://hdlbits.01xz.net/mw/images/3/3a/Wiredecl2.png)

```systemverilog
`default_nettype none
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out,
    output out_n   ); 
    
    wire ab;
    wire cd;
    wire pre;
    
    assign ab = a & b;
    assign cd = c & d;
    
    assign pre = ab | cd;
    assign out = pre;
    assign out_n = ~pre;

endmodule
```
Note: I need better naming for these wires. How do you name intermediary wires?

**Problem 10:** 7458 (chip with four AND gates and two OR gates)
![](https://hdlbits.01xz.net/mw/images/e/e1/7458.png)

```systemverilog
module top_module ( 
    input p1a, p1b, p1c, p1d, p1e, p1f,
    output p1y,
    input p2a, p2b, p2c, p2d,
    output p2y );

    wire p1y1;
    wire p1y2;
    wire p2y1;
    wire p2y2;
    
    assign p1y1 = p2a & p2b;
    assign p1y2 = p2c & p2d;
    assign p2y1 = p1a & p1c & p1b;
    assign p2y2 = p1f & p1e & p1d;
    
    assign p2y = p1y1 | p1y2;
    assign p1y = p2y1 | p2y2;
endmodule
```

**Problem 11:** Vector0
Vectors are used to group related signals using one name to make it more convenient to manipulate. For example, grouping various wires as `wire[7:0]`.
- Declaration of a vector places dimensions before name of vector: `wire[7:0] name`

Build a circuit that has one 3-bit input, then outputs the same vector, and also splits it into three separate 1-bit outputs. Connect output `o0` to the input vector's position 0, `o1` to position 1, etc.
![](https://hdlbits.01xz.net/mw/images/a/ae/Vector0.png)
```systemverilog
module top_module ( 
    input wire [2:0] vec,
    output wire [2:0] outv,
    output wire o2,
    output wire o1,
    output wire o0  ); // Module body starts after module declaration
    
    assign outv = vec;
    assign o0 = vec[0];
    assign o1 = vec[1];
    assign o2 = vec[2];
endmodule
```

Alternatively:
```systemverilog
assign outv = vec;
assign {o2, o1, o0} = vec;
```

reg = register?

**Problem 12:** Vector1
- Declaring vectors: `opt:portDirection type [upper:lower] vector_name` where type is usually wire or reg. Note, if declaring input or output, this will also be added
	- Endianness of a vector is whether LSB has a lower index or higher index. It can't be changed later on. 
- Implicit nets: Source of hard to detect bugs. What are nets?
	- Net-type signals can be "implicitly" created by an assign statement or attach something undeclared to a module port
		- one-bit wires and causes bugs if you had intended to use a vector
	- Disabling creation of implicit nets can be done using the `` `default_nettype none `` directive
- Unpacked vs. packed arrays: Packed dimensions are the vector indices written before vector name (bits are packed together in a blob in software), where as unpacked elements are declared after name for memory arrays.
- when lengths of the right and left sides don't match, it is zero-extended or truncated as appropriate.
- interesting vector selections:
	- `w[3:0]      // Only the lower 4 bits of w`
	- `z[-1:-2]    // Two lowest bits of z`
	- `x[1:1]      // ...the lowest bit of x`
	- `assign w[3:0] = b[0:3];    // Assign upper 4 bits of b to lower 4 bits of w. w[3]=b[0], w[2]=b[1], etc.`

Build a combinational circuit that splits an input half-word (16 bits, `[15:0]` ) into lower `[7:0]` and upper `[15:8]` bytes.
```systemverilog
`default_nettype none     // Disable implicit nets. Reduces some types of bugs.
module top_module( 
    input wire [15:0] in,
    output wire [7:0] out_hi,
    output wire [7:0] out_lo );

    assign out_hi = in[15:8];
    assign out_lo = in[7:0];
endmodule
```

**Problem 13**: Vector 2
A 32-bit vector can be viewed as containing 4 bytes (bits `[31:24]`, `[23:16]`, etc.). Build a circuit that will reverse the _byte_ ordering of the 4-byte word.
```systemverilog
module top_module( 
    input [31:0] in,
    output [31:0] out );//

    // assign out[31:24] = ...;
    assign out[31:24] = in[7:0];
    assign out[23:16] = in[15:8];
    assign out[15:8] = in[23:16];
    assign out[7:0] = in[31:24];

endmodule
```

**Problem 14**: Vector Gates
Build a circuit that has two 3-bit inputs that computes the bitwise-OR of the two vectors, the logical-OR of the two vectors, and the inverse (NOT) of both vectors. Place the inverse of `b` in the upper half of `out_not` (i.e., bits `[5:3]`), and the inverse of `a` in the lower half.

![](https://hdlbits.01xz.net/mw/images/1/1b/Vectorgates.png)
- Note: A bitwise operation between two N-bit vectors replicates the operation for each bit of the vector and produces a N-bit output, while a logical operation treats the entire vector as a boolean value
![](https://i.ytimg.com/vi/kAFuVw-byq0/maxresdefault.jpg)

```systemverilog
module top_module( 
    input [2:0] a,
    input [2:0] b,
    output [2:0] out_or_bitwise,
    output out_or_logical,
    output [5:0] out_not
);
    assign out_or_bitwise = a | b;
    assign out_or_logical = a || b;
    
    assign out_not[2:0] = ~a;
    assign out_not[5:3] = ~b;
	
endmodule
```

**Problem 15**: Gates4
Build a combinational circuit with four inputs, `in[3:0]`.
There are 3 outputs:
- out_and: output of a 4-input AND gate.
- out_or: output of a 4-input OR gate.
- out_xor: output of a 4-input XOR gate.

```systemverilog
module top_module( 
    input [3:0] in,
    output out_and,
    output out_or,
    output out_xor
);
    assign out_and = in[0] & in[1] & in[2] & in[3];
    assign out_or = in[0] | in[1] | in[2] | in[3];
    assign out_xor = in[0] ^ in[1] ^ in[2] ^ in[3];
endmodule
```

**Problem 16:** Vector3
Part selection is used to select portions of a vector. Concatenation operator `{}` is used to create larger vectors by concatenating smaller portions together

Example:
```systemverilog
input [15:0] in;
output [23:0] out;

assign {out[7:0], out[15:8]} = in;         // Swap two bytes. Right side and left side are both 16-bit vectors.
assign out[15:0] = {in[7:0], in[15:8]};    // This is the same thing.
assign out = {in[7:0], in[15:8]};       
// This is different. The 16-bit vector on the right is extended to
// match the 24-bit vector on the left, so out[23:16] are zero.
// In the first two examples, out[23:16] are not assigned.
```

Given several input vectors, concatenate them together then split them up into several output vectors. There are six 5-bit input vectors: a, b, c, d, e, and f, for a total of 30 bits of input. There are four 8-bit output vectors: w, x, y, and z, for 32 bits of output. The output should be a concatenation of the input vectors followed by two 1 bits:

```systemverilog
module top_module (
    input [4:0] a, b, c, d, e, f,
    output [7:0] w, x, y, z);
    
    wire [31:0] data;
    
    assign data[31:0] = {a[4:0],b[4:0],c[4:0],d[4:0],e[4:0],f[4:0]};
    assign {w[7:0], x[7:0], y[7:0], z[7:2]} = data;
    assign z[1:0] = 2'b11;
    
endmodule
```

**Problem 17:** Vectorr
Given an 8-bit input vector `[7:0]`, reverse its bit ordering.
```systemverilog
module top_module( 
    input [7:0] in,
    output [7:0] out
);
    assign out[7:0] = {in[0], in[1], in[2], in[3], in[4], in[5], in[6], in[7]};
endmodule
```

Recommended Solution Notes:
```systemverilog
module top_module (
	input [7:0] in,
	output [7:0] out
);
	
	assign {out[0],out[1],out[2],out[3],out[4],out[5],out[6],out[7]} = in;
	
	/*
	// I know you're dying to know how to use a loop to do this:

	// Create a combinational always block. This creates combinational logic that computes the same result
	// as sequential code. for-loops describe circuit *behaviour*, not *structure*, so they can only be used 
	// inside procedural blocks (e.g., always block).
	// The circuit created (wires and gates) does NOT do any iteration: It only produces the same result
	// AS IF the iteration occurred. In reality, a logic synthesizer will do the iteration at compile time to
	// figure out what circuit to produce. (In contrast, a Verilog simulator will execute the loop sequentially
	// during simulation.)
	always @(*) begin	
		for (int i=0; i<8; i++)	// int is a SystemVerilog type. Use integer for pure Verilog.
			out[i] = in[8-i-1];
	end


	// It is also possible to do this with a generate-for loop. Generate loops look like procedural for loops,
	// but are quite different in concept, and not easy to understand. Generate loops are used to make instantiations
	// of "things" (Unlike procedural loops, it doesn't describe actions). These "things" are assign statements,
	// module instantiations, net/variable declarations, and procedural blocks (things you can create when NOT inside 
	// a procedure). Generate loops (and genvars) are evaluated entirely at compile time. You can think of generate
	// blocks as a form of preprocessing to generate more code, which is then run though the logic synthesizer.
	// In the example below, the generate-for loop first creates 8 assign statements at compile time, which is then
	// synthesized.
	// Note that because of its intended usage (generating code at compile time), there are some restrictions
	// on how you use them. Examples: 1. Quartus requires a generate-for loop to have a named begin-end block
	// attached (in this example, named "my_block_name"). 2. Inside the loop body, genvars are read only.
	generate
		genvar i;
		for (i=0; i<8; i = i+1) begin: my_block_name
			assign out[i] = in[8-i-1];
		end
	endgenerate
	*/
	
endmodule
```

**Problem 18:** Vector4
- concatenation operator: concatenate vectors to form larger vectors
- replication vector: repeat vector and concatenate e.g.

```systemverilog
{5{1'b1}}           // 5'b11111 (or 5'd31 or 5'h1f)
{2{a,b,c}}          // The same as {a,b,c,a,b,c}
{3'd5, {2{3'd6}}}   // 9'b101_110_110. It's a concatenation of 101 with
                    // the second vector, which is two copies of 3'b110.
```

Build a circuit that sign-extends an 8-bit number to 32 bits. This requires a concatenation of 24 copies of the sign bit (i.e., replicate `bit[7`] 24 times) followed by the 8-bit number itself.

**KEY EXAMPLE:** How to sign-extend?
```systemverilog
module top_module (
    input [7:0] in,
    output [31:0] out );//

    // assign out = { replicate-sign-bit , the-input };
    assign out = {{24{in[7]}}, in[7:0]};

endmodule
```

**Problem 19:** Vector5
Given five 1-bit signals (a, b, c, d, and e), compute all 25 pairwise one-bit comparisons in the 25-bit output vector. The output should be 1 if the two bits being compared are equal.
```systemverilog
module top_module (
    input a, b, c, d, e,
    output [24:0] out );//

    wire [24:0] comp1;
    wire [24:0] comp2;
    // The output is XNOR of two vectors created by 
    // concatenating and replicating the five inputs.
    // assign out = ~{ ... } ^ { ... };
    assign comp1 = {{5{a}}, {5{b}}, {5{c}}, {5{d}}, {5{e}}}; 
    assign comp2 = {5{a, b, c, d, e}};
    assign out = ~{comp1} ^ {comp2};

endmodule
```
note: the brackets with these operators are funky.

**Problem 20:** Module
![](https://hdlbits.01xz.net/mw/images/c/c0/Module.png)
- There are two methods to connect a wire by port
	- By position: 
		- When instantiating, ports are connected left and right according to declaration: `mod_a instance1 ( wa, wb, wc );`
	- By name:
		- By name allows wires to remain correctly connected even if port list changes: `mod_a instance2 ( .out(wc), .in1(wa), .in2(wb) );`

```systemverilog
module top_module ( input a, input b, output out );
    mod_a(.in1(a), .in2(b), .out(out));
endmodule
```

**Problem 21**: Module pos
```systemverilog
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
    mod_a(out1,out2,a,b,c,d);

endmodule
```

**Problem 22: Module name**
```systemverilog
module top_module ( 
    input a, 
    input b, 
    input c,
    input d,
    output out1,
    output out2
);
    mod_a(.in1(a), .in2(b), .in3(c), .in4(d), .out1(out1), .out2(out2));
endmodule
```

**Problem 23:** Three Modules
![](https://hdlbits.01xz.net/mw/images/6/60/Module_shift.png)

```systemverilog
module top_module ( input clk, input d, output q );
    wire q1;
    wire q2;
    
    my_dff(.clk(clk), .d(d), .q(q1));
    my_dff(.clk(clk), .d(q1), .q(q2));
    my_dff(.clk(clk), .d(q2), .q(q));
    
endmodule
```

**Problem 24:** Module shift8
```systemverilog
module top_module ( 
    input clk, 
    input [7:0] d, 
    input [1:0] sel, 
    output [7:0] q 
);
	// failing cause i didn't make this 7:0
    wire [7:0] q1;
    wire [7:0] q2;
    wire [7:0] q3;
	
    my_dff8(.clk(clk), .d(d), .q(q1));
    my_dff8(.clk(clk), .d(q1), .q(q2));
    my_dff8(.clk(clk), .d(q2), .q(q3));
    
    always @(*) begin
        case(sel)
	        // 2'h0: q = d;
            2'b00 : q = d;
            2'b01 : q = q1;
            2'b10 : q = q2;
            2'b11 : q = q3;
        endcase
    end
    
endmodule
```

**Problem 25**: Module add
```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
    wire[15:0] s1, s2;
    wire c1, c2;
    
    add16(.a(a[15:0]), .b(b[15:0]), .cin(0), .sum(s1), .cout(c1));
    add16(.a(a[31:16]), .b(b[31:16]), .cin(c1), .sum(s2), .cout(c2));
    
    assign sum = {s2, s1};
    
endmodule
```

**Problem 26:** Module f_add
```systemverilog
module top_module (
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);//
	wire[15:0] s1, s2;
    wire c1, c2;
    
    add16(.a(a[15:0]), .b(b[15:0]), .cin(0), .sum(s1), .cout(c1));
    add16(.a(a[31:16]), .b(b[31:16]), .cin(c1), .sum(s2), .cout(c2));
    
    assign sum = {s2, s1};
endmodule

module add1 ( input a, input b, input cin,   output sum, output cout );

// Full adder module here
    wire [1:0] res;
    assign res = a+b+cin;
    assign sum = res[0];
    assign cout = res[1];

endmodule
```

**Problem 27:** Module cseladd
![](https://hdlbits.01xz.net/mw/images/3/3e/Module_cseladd.png)

```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    output [31:0] sum
);
    wire sel, c1, c2;
    wire[15:0] s1, s2, d1, d2;
    
    add16(.a(a[15:0]), .b(b[15:0]), .cin(0), .cout(sel), .sum(s1));
    add16(.a(a[31:16]), .b(b[31:16]), .cin(0), .cout(c1), .sum(d1));
    add16(.a(a[31:16]), .b(b[31:16]), .cin(1), .cout(c2), .sum(d2));
    
    always @(*) begin
        case (sel)
            1'b0: s2 = d1;
            1'b1: s2 = d2;
        endcase
    end
        
    assign sum = {s2, s1};

endmodule
```

**Problem 28:** Module addsub
![](https://hdlbits.01xz.net/mw/images/a/ae/Module_addsub.png)

```systemverilog
module top_module(
    input [31:0] a,
    input [31:0] b,
    input sub,
    output [31:0] sum
);
    wire [31:0] b_n;
    wire [15:0] s1, s2;
    wire c;
    
    assign b_n = b ^ {32{sub}};
    
    add16(.a(a[15:0]), .b(b_n[15:0]), .cin(sub), .cout(c), .sum(s1));
    add16(.a(a[31:16]), .b(b_n[31:16]), .cin(c), .cout(), .sum(s2));
 
    assign sum = {s2, s1};
endmodule
```

**Problem 29:** Alwaysblock1
- Procedures (always are procedures) provide alternative way for describing circuits
	- For synthesizing hardware, the two relevant ones are:
		- Combinational `always @(*)`
		- Clocked `always @(posedge clk)`
	- Combinational always blocks are equivalent to assign statements
		- syntax inside this is different. 
			- can't contain continuous assignments
			- richer set of statements (if-then, case etc.)
		- For combinational always blocks, always use a sensitivity list of (*)

Build an AND gate using both an assign statement and a combinational always block. (Since assign statements and combinational always blocks function identically, there is no way to enforce that you're using both methods. But you're here for practice, right?...)

```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module(
    input a, 
    input b,
    output wire out_assign,
    output reg out_alwaysblock
);
    
    always@(*) begin
        out_alwaysblock = a & b;
    end
    assign out_assign = a & b;

endmodule
```

**Problem 30:** Alwaysblock1
![](https://hdlbits.01xz.net/mw/images/4/40/Alwaysff.png)
Build an XOR gate three ways, using an assign statement, a combinational always block, and a clocked always block. Note that the clocked always block produces a different circuit from the other two: There is a flip-flop so the output is delayed.

```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module(
    input clk,
    input a,
    input b,
    output wire out_assign,
    output reg out_always_comb,
    output reg out_always_ff   );

    assign out_assign = a ^ b;
    
    always @(*) begin
        out_always_comb = a ^ b;
    end
    
    always @(posedge clk) begin
        out_always_ff = a ^ b;
    end
endmodule
```

**Problem 31:** Always if
Build a 2-to-1 mux that chooses between a and b. Choose b if _both_ sel_b1 and sel_b2 are true. Otherwise, choose a. Do the same twice, once using assign statements and once using a procedural if statement.
```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module(
    input a,
    input b,
    input sel_b1,
    input sel_b2,
    output wire out_assign,
    output reg out_always   ); 
    
    assign out_assign = sel_b1 ? (sel_b2 ? b : a) : a;
    always@(*) begin
        if (sel_b1) begin
            if (sel_b2) begin
            	out_always = b;
        	end 
            else begin
                out_always = a;
            end
        end 
        else begin
            out_always = a;
        end
    end

endmodule
```

**Problem 32:**
- behaviour of "keep outputs unchanged" means the current state needs to be _remembered_, and thus produces a _latch_.
-  Combinational circuits must have a value assigned to all outputs under all conditions

Question is to fix a bug in given code:
```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module (
    input      cpu_overheated,
    output reg shut_off_computer,
    input      arrived,
    input      gas_tank_empty,
    output reg keep_driving  ); //

    always @(*) begin
        if (cpu_overheated)
           shut_off_computer = 1;
        else 
            shut_off_computer = 0;
    end

    always @(*) begin
        if (~arrived)
       		keep_driving = ~gas_tank_empty;
        else
            keep_driving = 0;
    end

endmodule
```

**Problem 33:** Always case
- Case statements are like sequence of if-elseif-else that compares one expression to a list of others
- Case begins with `case`, each case item is a colon and no switch
- Each case item can execute **one** statement;
	- That's why `begin..end` are used when more than one statement exists
- Duplicate case items are allowed but only the first match is used
create a 6-to-1 multiplexer

```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module ( 
    input [2:0] sel, 
    input [3:0] data0,
    input [3:0] data1,
    input [3:0] data2,
    input [3:0] data3,
    input [3:0] data4,
    input [3:0] data5,
    output reg [3:0] out   );//
    always@(*) begin  // This is a combinational circuit
        case(sel)
           3'b000:
            out = data0;
           3'b001:
            out = data1;
           3'b010:
            out = data2;
           3'b011:
            out = data3;
           3'b100:
            out = data4;
           3'b101:
            out = data5;
           default:
            out = 3'b000;
        endcase
    end
endmodule
```

**Problem 34**: Always case 2
A _priority encoder_ is a combinational circuit that, when given an input bit vector, outputs the position of the first 1 bit in the vector. For example, a 8-bit priority encoder given the input 8'b10010000 would output 3'd4, because `bit[4] `is first bit that is high.

Build a 4-bit priority encoder. For this problem, if none of the input bits are high (i.e., input is zero), output zero. Note that a 4-bit number has 16 possible combinations.

```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module (
    input [3:0] in,
    output reg [1:0] pos  );
    always@(*) begin
        case(in)
            4'b0001:
                pos = 2'b00;
            4'b0010:
                pos = 2'b01;
            4'b0011:
                pos = 2'b00;
            4'b0100:
                pos = 2'b10;
            4'b0101:
                pos = 2'b00;
            4'b0110:
                pos = 2'b01;
            4'b0111:
                pos = 2'b00;
            4'b1000:
                pos = 2'b11;
            4'b1001:
                pos = 2'b00;
            4'b1010:
                pos = 2'b01;
            4'b1011:
                pos = 2'b00;
            4'b1100:
                pos = 2'b10;
            4'b1101:
                pos = 2'b00;
            4'b1110:
                pos = 2'b01;
            4'b1111:
                pos = 2'b00;
            default:
                pos = 2'b00;
        endcase
    end
endmodule
```
Redo this with casez for priority encoders!

**Problem 35:** Always casez
- Build a priority encoder for 8-bit inputs. Given an 8-bit vector, the output should report the first (least significant) bit in the vector that is 1. Report zero if the input vector has no bits that are high. For example, the input 8'b10010000 should output 3'd4, because bit[4] is first bit that is high.
```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module (
    input [7:0] in,
    output reg [2:0] pos );
    
    always@(*) begin
        casez(in[7:0])
            8'bzzzz_zzz1: pos[2:0] = 3'b000;
            8'bzzzz_zz1z: pos[2:0] = 3'b001;
            8'bzzzz_z1zz: pos[2:0] = 3'b010;
            8'bzzzz_1zzz: pos[2:0] = 3'b011;
            8'bzzz1_zzzz: pos[2:0] = 3'b100;
            8'bzz1z_zzzz: pos[2:0] = 3'b101;
            8'bz1zz_zzzz: pos[2:0] = 3'b110;
            8'b1zzz_zzzz: pos[2:0] = 3'b111;
            default: pos[2:0] = 3'b000;
        endcase
    end
endmodule
```

**Problem 36:** Always nolatches
Suppose you're building a circuit to process scancodes from a PS/2 keyboard for a game. Given the last two bytes of scancodes received, you need to indicate whether one of the arrow keys on the keyboard have been pressed. This involves a fairly simple mapping, which can be implemented as a case statement (or if-elseif) with four cases.

Your circuit has one 16-bit input, and four outputs. Build this circuit that recognizes these four scancodes and asserts the correct output.

```systemverilog
// synthesis verilog_input_version verilog_2001
module top_module (
    input [15:0] scancode,
    output reg left,
    output reg down,
    output reg right,
    output reg up  ); 
    always @(*) begin
        up = 1'b0; 
        down = 1'b0; 
        left = 1'b0; 
        right = 1'b0;
        
        case(scancode[15:0])
            16'he06b: left = 1'b1;
            16'he072: down = 1'b1;
            16'he074: right = 1'b1;
            16'he075: up = 1'b1;
            default: begin
                up = 1'b0; 
                down = 1'b0; 
                left = 1'b0; 
                right = 1'b0;
            end
        endcase
    end
endmodule
```

**problem 37**: Conditional
Given four unsigned numbers, find the minimum. Unsigned numbers can be compared with standard comparison operators (a < b). Use the conditional operator to make two-way _min_ circuits, then compose a few of them to create a 4-way _min_ circuit. You'll probably want some wire vectors for the intermediate results.

```systemverilog
module top_module (
    input [7:0] a, b, c, d,
    output [7:0] min);//

    // assign intermediate_result1 = compare? true: false;
	wire[7:0] cmp1, cmp2;
    always @(*) begin
        cmp1 = a > b ? b : a;
        cmp2 = c > d ? d : c;
        min = cmp1 > cmp2 ? cmp2 : cmp1;
    end
endmodule
```

**Problem 38:** Reduction
Parity checking is often used as a simple method of detecting errors when transmitting data through an imperfect channel. Create a circuit that will compute a parity bit for a 8-bit byte (which will add a 9th bit to the byte). We will use "even" parity, where the parity bit is just the XOR of all 8 data bits.

```systemverilog
module top_module (
    input [7:0] in,
    output parity);
    
    assign parity = ^in;

endmodule
```

**Problem 39**: Gates100
```systemverilog
module top_module( 
    input [99:0] in,
    output out_and,
    output out_or,
    output out_xor 
);

    assign out_and = &in;
    assign out_or = |in;
    assign out_xor = ^in;
endmodule
```

**Problem 40**: Vector100r
```systemverilog
module top_module( 
    input [99:0] in,
    output [99:0] out
);
    always @(*) begin	
        for (int i=0; i<100; i++)	
            out[i] = in[100-i-1];
	end
	// Alternatively 
	// out[i] = in[$bits(out)-i-1];
	// $bits() is a system function that returns the width of a signal.
	//  $bits(out) is 100 because out is 100 bits wide.
endmodule
```

**Problem 41:** Popcount255
```systemverilog
module top_module( 
    input [254:0] in,
    output [7:0] out );

    always @(*) begin	
        out[7:0] = 7'b00000000;
        for (int i=0; i<255; i++)	// int is a SystemVerilog type. Use integer for pure Verilog.
            if (in[i] == 1)
                out[7:0] = out[7:0] + 1;
	end
endmodule
```
Better solution is just adding `in[i]` to `out`

**Problem 42**: Adder100i
```systemverilog
module top_module( 
    input [99:0] a, b,
    input cin,
    output [99:0] cout,
    output [99:0] sum );

    genvar i;
    
    generate
        for (i = 0; i < 100; i=i+1)
            begin : g1
                if (i == 0) begin
                    assign sum[i] = (a[i] ^ b[i] ^ cin);
                	assign cout[i] = (a[i] & b[i]) | (a[i] & cin) | (b[i] & cin);
                end 
                else begin
                    assign sum[i] = (a[i] ^ b[i] ^ cout[i-1]);
                    assign cout[i] = (a[i] & b[i]) | (a[i] & cout[i-1]) | (b[i] & cout[i-1]);
                end
            end
    endgenerate
endmodule
```

**Problem 43:** bcdadd100
```systemverilog
module top_module( 
    input [399:0] a, b,
    input cin,
    output cout,
    output [399:0] sum );

    genvar i;
    
    wire[399:0] c;
    
    generate
        for(i = 0; i < 400; i=i+4)
            begin : g0
                if (i == 0)
                    bcd_fadd(.a(a[3:0]), .b(b[3:0]), .cin(cin), .cout(c[i]), .sum(sum[3:0]));
                else
                    bcd_fadd(.a(a[i+3:i]), .b(b[i+3:i]), .cin(c[i/4 - 1]), .cout(c[i/4]), .sum(sum[i+3:i]));
            end
    endgenerate
    assign cout = c[99];
    
    
endmodule
```

#### CIRCUITS
**Problem 44:** fadd
```systemverilog
module top_module( 
    input a, b, cin,
    output cout, sum );
    
    assign sum = (a ^ b ^ cin);
	assign cout = (a & b) | (a & cin) | (b & cin);

endmodule
```

**Problem 45:** Exams/m2014 q4h
```systemverilog
module top_module (
    input in,
    output out);
    
    assign out = in;

endmodule
```

**Problem 46:** Exams/m2014 q4i
```systemverilog
module top_module (
    output out);
	assign out = 0;
endmodule
```

**Problem 47:**  Exams/m2014 q4e
```systemverilog
module top_module (
    input in1,
    input in2,
    output out);
    assign out = ~(in1 | in2);
endmodule
```

**Problem 48:** Exams/m2014 q4f
```systemverilog
module top_module (
    input in1,
    input in2,
    output out);
    
    assign out = in1 & ~in2;

endmodule
```

**Problem 49:** Exams/m2014 q4g
```systemverilog
module top_module (
    input in1,
    input in2,
    input in3,
    output out);
    assign out = ~(in1 ^ in2) ^ in3;
endmodule
```

**Problem 50:** Gates
```systemverilog
module top_module( 
    input a, b,
    output out_and,
    output out_or,
    output out_xor,
    output out_nand,
    output out_nor,
    output out_xnor,
    output out_anotb
);
    assign out_and = a & b;
    assign out_or = a | b;
    assign out_xor = a ^ b;
    assign out_nand = ~(a & b);
    assign out_nor = ~(a | b);
    assign out_xnor = ~(a ^ b);
    assign out_anotb = a & ~b;

endmodule
```

**Problem 51**: 7420
```systemverilog
module top_module ( 
    input p1a, p1b, p1c, p1d,
    output p1y,
    input p2a, p2b, p2c, p2d,
    output p2y );

    assign p1y = ~(p1a & p1b & p1c & p1d);
    assign p2y = ~(p2a & p2b & p2c & p2d);

endmodule
```

**Problem 52:** Truthtable1
```systemverilog
module top_module( 
    input x3,
    input x2,
    input x1,  // three inputs
    output f   // one output
);

    assign f = (x2 & ~x3 & ~x1) | (~x3 & x2 & x1) | (x3 & x1 & ~x2) | (x3 & x2 & x1);
endmodule
```
==Review how to simplify this circuit from ECE 124


**Problem 53:** Mt2015 eq24
```systemverilog
module top_module ( input [1:0] A, input [1:0] B, output z ); 
    always@(*) begin
        if (A == B)
            z = 1;
        else 
            z = 0;
        end
endmodule
```
Easier if this is a ternary operation

**Problem 54: Mt2015 q4a

```systemverilog
module top_module (input x, input y, output z);
    assign z = (x^y) & x;
endmodule
```

**Problem 55:** Mt2015 q4b
```systemverilog
module top_module ( input x, input y, output z );
    assign z = (~x & ~y) | (x & y);
endmodule
```

**Problem 56:** Mt2015 q4
```systemverilog
module a (input x, input y, output z);
    assign z = (x^y) & x;
endmodule

module b ( input x, input y, output z );
    assign z = (~x & ~y) | (x & y);
endmodule

module top_module (input x, input y, output z);
	wire a_out, b_out;

      // Instantiate modules a and b, connecting their inputs and outputs
      a a_instance (x, y, a_out);
      b b_instance (x, y, b_out);

  	assign z = (a_out | b_out) ^ (a_out & b_out);
    
endmodule
```

With this one, I need to instantiate it before using those modules ?

**Problem 57:** ringer
```systemverilog
module top_module (
    input ring,
    input vibrate_mode,
    output ringer,       // Make sound
    output motor         // Vibrate
);
    
    assign ringer = ring ? (vibrate_mode ? 0 : 1) : 0;
    assign motor = ring ?  (vibrate_mode ? 1 : 0): 0;

endmodule
```

Optimized:
```systemverilog
module top_module(
	input ring, 
	input vibrate_mode,
	output ringer,
	output motor
);
	
	// When should ringer be on? When (phone is ringing) and (phone is not in vibrate mode)
	assign ringer = ring & ~vibrate_mode;
	
	// When should motor be on? When (phone is ringing) and (phone is in vibrate mode)
	assign motor = ring & vibrate_mode;
	
endmodule
```

**Problem 58:** Thermostat
```systemverilog
module top_module (
    input too_cold,
    input too_hot,
    input mode,
    input fan_on,
    output heater,
    output aircon,
    output fan
); 
    
    assign heater = mode & too_cold;
    assign aircon = ~mode & too_hot;
    assign fan = fan_on | (mode & too_cold) | (~mode & too_hot);

endmodule
```

optimally,
```systemverilog
// Fan should be on when either heater or aircon is on, and also when requested to do so (fan_on = 1).
assign fan = heater | aircon | fan_on;
// Heater is on when it's too cold and mode is "heating".
assign heater = (mode & too_cold);
// Aircon is on when it's too hot and mode is not "heating".
assign aircon = (~mode & too_hot);
```

**Problem 59:** Popcount3
```systemverilog
module top_module( 
    input [2:0] in,
    output [1:0] out );

    assign out = in[0] + in[1] + in[2];

endmodule
```

**problem 60:** gatesv
```systemverilog
module top_module( 
    input [3:0] in,
    output [2:0] out_both,
    output [3:1] out_any,
    output [3:0] out_different );

    assign out_both[0] = in[0] & in[1];
    assign out_both[1] = in[1] & in[2];
    assign out_both[2] = in[2] & in[3];
    
    assign out_any[1] = in[1] | in[0];
    assign out_any[2] = in[1] | in[2];
    assign out_any[3] = in[3] | in[2];
    
    assign out_different[0] = in[0] ^ in[1];
    assign out_different[1] = in[1] ^ in[2];
    assign out_different[2] = in[2] ^ in[3];
    assign out_different[3] = in[3] ^ in[0];
    
    
endmodule
```

==Optimize this!!

**problem 61:** Gatesv100

```systemverilog
module top_module( 
    input [99:0] in,
    output [98:0] out_both,
    output [99:1] out_any,
    output [99:0] out_different );

    assign out_both = in[98:0] & in[99:1];
    assign out_any = in[99:1] | in[98:0];
    assign out_different[98:0] = in[98:0] ^ in[99:1];
    assign out_different[99] = in[0] ^ in[99];
endmodule
```

**problem 62:** Mux2to1
```systemverilog
module top_module( 
    input a, b, sel,
    output out ); 
	assign out = sel ? b : a;
endmodule
```

**Problem 63:** Mux2to1v
```systemverilog
module top_module( 
    input [99:0] a, b,
    input sel,
    output [99:0] out );

    assign out = sel ? b : a;
endmodule
```

**Problem 64:** Mux9to1v
```systemverilog
module top_module( 
    input [15:0] a, b, c, d, e, f, g, h, i,
    input [3:0] sel,
    output [15:0] out );
	
    always@(*) begin
        case(sel)
            4'b0000:
                out = a;
            4'b0001:
                out = b;
            4'b0010:
                out = c;
            4'b0011:
                out = d;
            4'b0100:
                out = e;
            4'b0101:
                out = f;
            4'b0110:
                out = g;
            4'b0111:
                out = h;
            4'b1000:
                out = i;
            default:
                out[15:0] = 16'b11111111_11111111;
        endcase
    end
endmodule
```

their solution:
```systemverilog
module top_module (
	input [15:0] a,
	input [15:0] b,
	input [15:0] c,
	input [15:0] d,
	input [15:0] e,
	input [15:0] f,
	input [15:0] g,
	input [15:0] h,
	input [15:0] i,
	input [3:0] sel,
	output logic [15:0] out
);

	// Case statements can only be used inside procedural blocks (always block)
	// This is a combinational circuit, so use a combinational always @(*) block.
	always @(*) begin
		out = '1;		// '1 is a special literal syntax for a number with all bits set to 1.
						// '0, 'x, and 'z are also valid.
						// I prefer to assign a default value to 'out' instead of using a
						// default case.
		case (sel)
			4'h0: out = a;
			4'h1: out = b;
			4'h2: out = c;
			4'h3: out = d;
			4'h4: out = e;
			4'h5: out = f;
			4'h6: out = g;
			4'h7: out = h;
			4'h8: out = i;
		endcase
	end
	
endmodule
```

**Problem 65:** Mux256to1
```systemverilog
module top_module( 
    input [255:0] in,
    input [7:0] sel,
    output out );
    
    assign out = in[sel];

endmodule
```


**Problem 66:** Mux256to1v
```systemverilog
module top_module( 
    input [1023:0] in,
    input [7:0] sel,
    output [3:0] out );
	
    assign out = in[sel*4+:4];
endmodule
```

**Problem 67:** adder3
```systemverilog
module top_module( 
    input [2:0] a, b,
    input cin,
    output [2:0] cout,
    output [2:0] sum );
    
    fa fa1(a[0], b[0], cin, cout[0], sum[0]);
    fa fa2(a[1], b[1], cout[0], cout[1], sum[1]);
    fa fa3(a[2], b[2], cout[1], cout[2], sum[2]);
    
endmodule

module fa( 
    input a, b, cin,
    output cout, sum );
    
    assign sum = (a ^ b ^ cin);
	assign cout = (a & b) | (a & cin) | (b & cin);

endmodule
```

**Problem 68:** hadd
```systemverilog
module top_module( 
    input a, b,
    output cout, sum );
    
    assign sum = (a ^ b);
	assign cout = (a & b);

endmodule
```

**Problem 69:** Exams/m2014 q4j
```systemverilog
module top_module (
    input [3:0] x,
    input [3:0] y, 
    output [4:0] sum);
    
    wire [4:0] cout;
    
    genvar i;
    
    generate
        for (i = 0; i < 4; i=i+1)
            begin : g1
                if (i == 0)
                    fa(x[0], y[0], 0, cout[0], sum[0]);
                else
                    fa(x[i], y[i], cout[i-1], cout[i], sum[i]);
            end
    endgenerate
    
    assign sum[4] = cout[3];
    
endmodule

module fa( 
    input a, b, cin,
    output cout, sum );
    
    assign sum = (a ^ b ^ cin);
	assign cout = (a & b) | (a & cin) | (b & cin);

endmodule
```

**Problem 70:**
```systemverilog
module top_module (
    input [7:0] a,
    input [7:0] b,
    output [7:0] s,
    output overflow
); //
 
    assign s = a + b;
    assign overflow = a[7] == b[7] ? (s[7] != a[7]) : 0;

endmodule
```

**Problem 71:** 
```systemverilog
module top_module( 
    input [99:0] a, b,
    input cin,
    output cout,
    output [99:0] sum );

    assign {cout, sum} = a + b + cin;
    
endmodule
```

**Problem 72:** Bcdadd4
```systemverilog
module top_module ( 
    input [15:0] a, b,
    input cin,
    output cout,
    output [15:0] sum );
    
    wire cout1[3:0];
    
    bcd_fadd f1(a[3:0], b[3:0], cin, cout1[0], sum[3:0]);
    bcd_fadd f2(a[7:4], b[7:4], cout1[0], cout1[1], sum[7:4]);
    bcd_fadd f3(a[11:8], b[11:8], cout1[1], cout1[2], sum[11:8]);
    bcd_fadd f4(a[15:12], b[15:12], cout1[2], cout, sum[15:12]);
    
endmodule
```

**Problem 73:**
```systemverilog
module top_module(
    input a,
    input b,
    input c,
    output out  ); 

    assign out = a | c | (b & ~c);
endmodule
```


**Problem 74:** kmap2
```systemverilog
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out  ); 
    
    assign out = (~c & ~b) | (~a & b & ~c & ~d) | (~a & b & d & c) | (c & d & a) | (c & ~d & ~a);

endmodule
```

**Problem 74**:
```systemverilog
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out  ); 

    assign out = a | (c & ~a & ~b);
    
endmodule
```

**Problem 75**:
```systemverilog
module top_module(
    input a,
    input b,
    input c,
    input d,
    output out  ); 
    
    assign out = ((~a&~b | a&b) & (~c&d | c&~d)) | ((~a&b | a&~b) & (~c&~d | c&d));

endmodule
```

**Problem 76:**
```systemverilog
module top_module (
    input clk,    // Clocks are used in sequential circuits
    input d,
    output reg q );//

    // Use a clocked always block
    //   copy d to q at every positive edge of clk
    //   Clocked always blocks should use non-blocking assignments
    always@(posedge clk)
        begin
            q = d;
        end

endmodule
```

**Problem 77:**
```systemverilog
module top_module (
    input clk,
    input [7:0] d,
    output [7:0] q
);
    always@(posedge clk) begin
        q[7:0] = d[7:0];
    end

endmodule
```

**Problem 78:** 
```systemverilog
module top_module (
    input clk,
    input reset,            // Synchronous reset
    input [7:0] d,
    output [7:0] q
);
    always@(posedge clk) begin
        q[7:0] = !reset ? d[7:0] : 8'b0000_0000;
    end
endmodule
```

**Problem 79:** 
```systemverilog
module top_module (
    input clk,
    input reset,
    input [7:0] d,
    output [7:0] q
);
    always @(negedge clk) begin
        q[7:0] = reset ? 8'h34 : d[7:0];
    end
endmodule
```

**Problem 80**
```systemverilog
module top_module (
    input clk,
    input areset,   // active high asynchronous reset
    input [7:0] d,
    output [7:0] q
);
    always@(posedge clk or posedge areset) begin
        if (areset) begin
            q <= 8'b0000_0000;
        end else begin
            q <= d;
        end
    end
endmodule
```


**problem 81**
```systemverilog
module top_module (
    input clk,
    input resetn,
    input [1:0] byteena,
    input [15:0] d,
    output [15:0] q
);
    
    always@(posedge clk) begin
        if (!resetn) begin
            q <= 16'b0000_0000_0000_0000;
        end else begin
            if (byteena[0]) begin
                q[7:0] <= d[7:0];
            end
            if (byteena[1]) begin
                q[15:8] <= d[15:8];
            end
        end
    end

endmodule
```

**Problem 82**
```systemverilog
module top_module (
    input d, 
    input ena,
    output q);

    always@(*) begin
        if (ena) begin
            q = d;
        end
    end
    
endmodule
```

**Problem 83** DFF
```systemverilog
module top_module (
    input clk,
    input d, 
    input ar,   // asynchronous reset
    output q);

    always@(posedge clk or posedge ar) begin
        if (ar) begin
            q <= 1'b0;
        end else begin
            q <= d;
        end
        
    end
    
endmodule
```

**Problem 84** Exams/m2014 q4c
```systemverilog
module top_module (
    input clk,
    input d, 
    input r,   // synchronous reset
    output q);

    always@(posedge clk) begin
        q = r ? 1'b0 : d;
    end
endmodule
```

**Problem 85** Exams/m2014 q4d
```systemverilog
module top_module (
    input clk,
    input in, 
    output out);
    
    always @(posedge clk) begin
        out = in ^ out;
    end

endmodule
```


**Problem 86** DFF gate
```systemverilog
module top_module (
	input clk,
	input L,
	input r_in,
	input q_in,
	output reg Q);
	
    always@(posedge clk) begin
        if (L) begin
            Q = r_in;
        end
        else begin
            Q = q_in;
        end
    end
    
endmodule
```

**Problem 87:**
```systemverilog
module top_module (
    input clk,
    input w, R, E, L,
    output Q
);
    
    always @(posedge clk) begin
        if (E) begin
            if (L) begin
                Q <= R;
            end else begin
                Q <= w;
            end
        end
        else begin
            if (L) begin
                Q <= R;
            end 
        end
    end 
endmodule
```

**Problem 88:**
```systemverilog
module top_module (
    input clk,
    input x,
    output z
); 
    reg q1, q2, q3;
    reg d1, d2, d3;
        
    always@(posedge clk) begin        
        d1 = x ^ q1;
        d2 = x & ~q2;
        d3 = x | ~q3;
        
        q1 = d1;
        q2 = d2;
        q3 = d3;
        
    end
    assign z = ~(q1 | q2 | q3);

endmodule
```

**TEMPLATE**
**Problem XX:** XX
```systemverilog

```