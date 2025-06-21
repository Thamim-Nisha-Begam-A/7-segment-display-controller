-- 7-segment-display-controller
-- 7-Segment Display Controller (VHDL)  This project implements a 7-segment display controller using VHDL. It decodes 4-bit binary ----input to display hexadecimal digits on a 7-segment display.
 
-- Features 
-- Displays 0–F on a single-digit 7-segment display
-- Includes clock divider for timing control
- Testbench for simulation
--Tools
--Vivado 2020.2 / Quartus Prime
--ModelSim / GHDL

--Usage
-- Simulate using `seven_segment_tb.vhd`
-- Synthesize and upload to FPGA

library ieee; 
use ieee.std_logic_1164.all; 
use ieee.std_logic_unsigned.all; 
entity num is 
   port(clk,reset: in std_logic; 
       --A: in STD_LOGIC_vector (7 downto 0);
       Y: out STD_LOGIC_vector (7 downto 0)); 
end num; 
architecture behave of num is 
signal temp: std_logic_vector(3 downto 0);
signal Sel : STD_LOGIC_VECTOR(3 downto 0); 
begin 
   cnt_block:process(clk,reset) 
   begin 
      if (reset = '1' or temp ="1001") then 
         temp <= "0000"; 
   	  elsif rising_edge(clk) then 
         temp <= temp+1; 
   	  end if; 
   end process cnt_block;
sel<=temp;
   muxc: process(Sel)
   begin
      case Sel is
            when "0000" => Y <= "00111111";
            when "0001" => Y <= "00000110";
            when "0010" => Y <= "01010011";
            when "0011" => Y <= "01001111";
            when "0100" => Y <= "01100110";
            when "0101" => Y <= "01101101";
            when "0110" => Y <= "01111110";
            when "0111" => Y <= "00000111";
            when "1000" => Y <= "01111111";
            --when "1001" => Y <= 01100111;
            when others => Y <= "01100111"; 
      end case;
   end process muxc;
end behave;


