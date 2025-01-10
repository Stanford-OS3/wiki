This is an overview of the ASIC utilized in the system.

## Chip Overview ##

The ASIC for this system focuses on accelerating the multiply and accumulate operations utilizied for convolution. To do this, the architecture of the system focuses on doing one 3x3 elementwise multiply and accumulate per cycle. For the purposes of this project, we are calling these convolution engines. To take advantage of spatial locality, the operation is parallelized over multiple convolution engines to the extent that the I/O bandwidth and cache space affords. To connect the chip to the rest of the system, a special SPI-like protocol is used to transmit the image, filters, and outputs. 

## Convolution Engine ##

The convolution engine features an 8-bit add circuitry with a 16-bit multiply circuity for each filter element. Therefore, there are 9 of these items in each. Based on the clock frequency that is attempted to be achieved, we can utilize pipelining for the adders and multipliers. At the moment of writing this (Jan 2025), we do not need to pipeline the operations as the clock frequency is too low. 

## Cache System ##
The cache system is an optional component for taking advantage of temperoral locality. Since the cache consists of SRAM which can be quite expensive area-wise, there is a limited amount that can be used in our chip (~100 KB in the SKY130). There is the potential for a cache to be relatively difficult to achieve based on the bandwidth that can be achieved with both the input and cache.

Here is a link to SRAM IP we are looking to use SKY130 (if we use it): https://platform.efabless.com/design_catalog/ip_block/40

## SPI ## 
The SPI influence in this system can be seen with the use of a syncronizing clock, chip select, and input and output data pins. For the use of this system, there are 32 data input pins (from FPGA to ASIC) and 2 data output pins (from ASIC to FPGA). If it can be utilized, we can use multi-data rate to achieve a necessary bandwidth. 
