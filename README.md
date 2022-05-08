# verilogsheet
Cheat sheet for Verilog and other notes

reset_timing, read_xdc (file) or create_clock -name clk -period 4 -waveform {0 2} [get_ports clk], last report_timing (can use GUI)

```
`timescale 1ns / 1ps

module ModuleName
  #(parameter PNAME = 4,
  localparam LPNAME = CPNAME*1) // comment
  (
  input wire clk,
  input wire reset,
  input wire [PNAME-1:0]din,
  output wire [LPNAME-1:0]dout
  );  
endmodule
```

```
`timescale 1ns / 1ps

module ModuleNameTestbench(
  );
  
  parameter PNAME = 4;
  localparam LPNAME = CPNAME*1;
  
  localparam tCK = 0.75;
  
  reg clk;
  reg reset;
  reg  [PNAME-1:0]din;
  wire [LPNAME-1:0]dout;
  
  integer i; // loop variable
  
  ModuleName #(.PNAME(PNAME)
  ) dut (.clk(clk),
  .reset(reset)
  .din(din),
  .dout(dout)
  );
  
  always #(tCK*0.5) clk = ~clk;
  
  initial
  begin
    clk = 1;
    din = 0;

    #(4*tCK)
    $stop;
  end;
  
endmodule

```

```
input wire  [TypeW-1:0]dqin    [DimA-1:0][DimB-1:0],

  genvar i;
  generate
    for (i = 0; i < Cnt ; i=i+1)
    begin:MN
      ModuleName #(.PNAME(PNAME)) MNi (
      .clk(clk),
      .reset(reset),
      .din(din[i]),
      .dout(dout[i])
      );
    end
  endgenerate
```

```
`ifdef ABC
  input ABC
  `elsif DEF
  input DEF
  `endif
```
