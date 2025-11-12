# **EXP5: Design and Simulation of RAM, ROM, and FIFO Memory with Read and Write Operations Using Verilog HDL**

---

## **Aim**
To design, simulate, and verify the functionality of **RAM**, **ROM**, and **FIFO memory** modules with **read and write operations** using Verilog HDL.

---

## **Apparatus Required**
- System with **Vivado Design Suite**
---

## **Theory**

### **1. Random Access Memory (RAM)**
RAM is a volatile memory used to store data temporarily during program execution. It supports both **read** and **write** operations. Data can be accessed randomly using the address lines.  
In Verilog, RAM can be modeled using a `reg` array with write operation controlled by a **write enable (WE)** signal.

### **2. Read Only Memory (ROM)**
ROM is a non-volatile memory where data is permanently stored and can only be **read**, not written. The contents are initialized during declaration using an `initial` block or `$readmemb`/`$readmemh` commands.

### **3. First In First Out (FIFO) Memory**
FIFO is a sequential buffer that stores data such that the **first data written is the first data read**. It uses two pointers — **write pointer** and **read pointer** — to manage data flow. FIFO finds application in data buffering and inter-module communication.

---

## **Program**

### **1. RAM Module**
```verilog
// 4x8 RAM with Read and Write Operations
module ram_4x8 (
    input clk,
    input we,
    input [1:0] addr,
    input [7:0] data_in,
    output reg [7:0] data_out
);
    reg [7:0] memory [3:0];

endmodule
```
### Testbench for RAM
```
module tb_ram_4x8;
    reg clk, we;
    reg [1:0] addr;
    reg [7:0] data_in;
    wire [7:0] data_out;

    ram_4x8 uut(clk, we, addr, data_in, data_out);

    always #5 clk = ~clk;

    initial begin
        clk = 0; we = 0;
        addr = 2'b00; data_in = 8'h00;
        #10 we = 1; addr = 2'b00; data_in = 8'hA5; // Write A5 at addr 00
        #10 addr = 2'b01; data_in = 8'h3C;         // Write 3C at addr 01
        #10 we = 0; addr = 2'b00;                  // Read addr 00
        #10 addr = 2'b01;                          // Read addr 01
        #10 $finish;
    end
endmodule
```
### Simulation Output for RAM
*
*
*
*
Paste the output here
*
*
### 2. ROM Module
```
// 4x8 ROM with Preloaded Data
module rom_4x8 (
    input [1:0] addr,
    output reg [7:0] data_out
);
    reg [7:0] memory [3:0];



endmodule
```
### Testbench for ROM
```
module tb_rom_4x8;
    reg [1:0] addr;
    wire [7:0] data_out;

    rom_4x8 uut(addr, data_out);

  
```
### Simulation Output for ROM
*
*
*
*
Paste the output here
*
*


### 3. FIFO Memory Module
```
// 4x8 FIFO Memory with Read and Write Operations
module fifo_4x8 (
    input clk, reset, wr_en, rd_en,
    input [7:0] data_in,
    output reg [7:0] data_out,
    output reg full, empty
);
    reg [7:0] fifo_mem [3:0];
    reg [1:0] wr_ptr, rd_ptr;
    reg [2:0] count;

    always @(posedge clk or posedge reset) begin
        if (reset) begin
            wr_ptr <= 0;
            rd_ptr <= 0;
            count <= 0;
            full <= 0;
            empty <= 1;
        end
        else begin
            // Write operation
            if (wr_en && !full) begin
                fifo_mem[wr_ptr] <= data_in;
                wr_ptr <= wr_ptr + 1;
                count <= count + 1;
         
    end
endmodule
```
### Testbench for FIFO
```
module tb_fifo_4x8;
    reg clk, reset, wr_en, rd_en;
    reg [7:0] data_in;
    wire [7:0] data_out;
    wire full, empty;

    fifo_4x8 uut(clk, reset, wr_en, rd_en, data_in, data_out, full, empty);

    always #5 clk = ~clk;

    initial begin
        clk = 0; reset = 1; wr_en = 0; rd_en = 0; data_in = 8'h00;
        #10 reset = 0;

        // Write data
        wr_en = 1; data_in = 8'h11; #10;
        data_in = 8'h22; #10;
        
endmodule
```
### Simulation Output for FIFO
*
*
*
*
Paste the output here
*
*
### Result

The RAM, ROM, and FIFO memory modules were successfully designed, simulated, and verified using Verilog HDL in Vivado Design Suite.
All read and write operations performed as expected during simulation.
