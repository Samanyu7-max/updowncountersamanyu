# updowncounter
# updowncounter
module up_down_counter (
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


