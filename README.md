# ADXL345
To Create driver file for ADXL345 sensor to communicate with SPI & I2C interfaces.

ADXL345 GPIO CONFIGURATIONS/REGISTER CONFIGURATIONS:

Enable I2C/SPI: - CS pin is used to enable serial port (This line must go low at start of transmission and high at end of transmission). The CS pin should always be tied high to VDD
I/O or be driven by an external controller because there is no default
mode if the CS pin is left unconnected.

SCL/SCLK -Data is updated on the falling edge of SCLK and should be sampled on the rising edge of SCLK.

SPI 3wire/4wire mode configuration:
DATA_FORMAT register(bit D6) - 0x31 -> When set,  selects 3 wire mode configuration,
                                            else, selects 4 wire mode configuration.

I2C Device configuration:
I2C DEVICE ADDRESS1 - With the ALT ADDRESS pin high, the 7-bit I2C address for the device is 0x1D. {0x3A for a write and 0x3B for a read}
I2C DEVICE ADDRESS2 - An alternate I2C address of 0x53 (followed by the R/W bit) can be chosen by grounding the SDO/ALT ADDRESS pin (Pin 12). {0xA6 for a write and 0xA7 for a read}

INTERRUPT PINS:

ADXL345 provides two output pins for driving interrupts: INT1 & INT2 [Default configuration of these pins is active high]
To change it to low, configure DATA FORMAT REGISTER(0X31) - Set INT_INVERT bit to 1

Interrupts are enabled by setting appropriate bit in INT_ENABLE register (Address 0x2E) and are mapped to either the INT1
pin or the INT2 pin based on the contents of the INT_MAP register (Address 0x2F).

Interrupt data registers (Address 0x32 to Address 0x37)
Interrupt bits:
1. DATA READY - Indicate data is available or not
2. SINGLE_TAP - Set this bit, when acceleration value is greater than THRESH_TAP Register(Address 0x1D)
3. DOUBLE TAP - Set this bit, when two acceleration value is greater than THRESH_TAP Register(Address 0x1D)
4. ACTIVITY   - Set this bit, when acceleration value is greater than THRESH_ACT register (Address 0x24)
5. INACTIVITY - Set this bit, when acceleration is lesser than THRESH_INACT register (Address 0x25)
6. FREE_FALL  - Set this bit, when acceleration is lesser than THRESH_FF register (Address 0x28)
7. WATERMARK  - When no of samples equals the value stored in (Register FIFO_CTL, Address 0x38)
8. OVERRUN    - the overrun bit is set when new data replaces unread data in the DATAX, DATAY, and DATAZ registers (Address 0x32 to Address 0x37).


