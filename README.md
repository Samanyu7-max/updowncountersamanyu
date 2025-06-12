// updowncounter
module hello(
    input clk,//clock pulses
    input reset,//reset setting it back to 0
    input up_down,//like enable
    output reg [3:0] count // 4-bit counter we can change the width  any time
);

always @(posedge clk or posedge reset) begin
    if (reset)
        count <= 4'b0000; // Reset count to 0
    else begin
        if (up_down)
            count <= count + 1; // Increment
        else
            count <= count - 1; // Decrement
    end
end

endmodule


//testbench
module tb_hello;

    // Inputs
    reg clk;
    reg reset;
    reg up_down;

    // Output
    wire [3:0] count;

    hello dut (
        .clk(clk),
        .reset(reset),
        .up_down(up_down),
        .count(count)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk; // Toggle every 5ns
    end

    initial begin
        $display("Time\tReset\tUp_Down\tCount");
        $monitor("%0t\t%b\t%b\t%b", $time, reset, up_down, count);
        reset = 1; up_down = 0;
        #10;

        reset = 0; up_down = 1; // Count up
        #50;

        up_down = 0; // Count down
        #50;

        reset = 1; // Reset again
        #10;

        $finish;
    end

endmodule
