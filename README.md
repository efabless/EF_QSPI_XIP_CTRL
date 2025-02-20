# EF_QSPI_XIP_CTRL

A QSPI XiP Flash COntroller with a parameterized Direct-Mapped Cache.
## The wrapped IP


 The IP comes with an AHBL Wrapper

#### Wrapped IP System Integration

```verilog
EF_QSPI_XIP_CTRL_APB INST (
	`TB_AHBL_SLAVE_CONN,
	.sck(sck)
	.ce_n(ce_n)
	.dout(dout)
	.din(din)
	.douten(douten)
);
```
> **_NOTE:_** `TB_APB_SLAVE_CONN is a convenient macro provided by [BusWrap](https://github.com/efabless/BusWrap/tree/main).
### Wrappers with DFT support
Wrappers in the directory ``/hdl/rtl/bus_wrappers/DFT`` have an extra input port ``sc_testmode`` to disable the clock gate whenever the scan chain testmode is enabled.
### External IO interfaces
|IO name|Direction|Width|Description|
|---|---|---|---|
|sck|output|1|SPI serial clock|
|ce_n|output|1|SPI chip select (Active Low).|
|dout|output|4|Flash controller SPI data out.|
|din|input|4|Flash controller SPI data in.|
|douten|output|4|Flash controller data out enable (Active Low)|
### Interrupt Request Line (irq)
This IP generates interrupts on specific events, which are described in the [Interrupt Flags](#interrupt-flags) section bellow. The IRQ port should be connected to the system interrupt controller.

## Implementation example  

The following table is the result for implementing the EF_QSPI_XIP_CTRL IP with different wrappers using Sky130 HD library and [OpenLane2](https://github.com/efabless/openlane2) flow.
|Module | Number of cells | Max. freq |
|---|---|---|
|EF_QSPI_XIP_CTRL|1973| 250 |
|EF_QSPI_XIP_CTRL_AHBL|1973|250|
## The Programmer's Interface


### Registers

|Name|Offset|Reset Value|Access Mode|Description|
|---|---|---|---|---|

## Firmware Drivers:
Firmware drivers for EF_QSPI_XIP_CTRL can be found in the [Drivers](https://github.com/efabless/EFIS/tree/main/Drivers) directory in the [EFIS](https://github.com/efabless/EFIS) (Efabless Firmware Interface Standard) repo. EF_QSPI_XIP_CTRL driver documentation  is available [here](https://github.com/efabless/EFIS/blob/main/Drivers/Docs/EF_QSPI_XIP_CTRL/README.md).
You can also find an example C application using the EF_QSPI_XIP_CTRL drivers [here](https://github.com/efabless/EFIS/tree/main/Drivers/Docs/EF_QSPI_XIP_CTRL/example).
## Installation:
You can install the IP either by cloning this repository or by using [IPM](https://github.com/efabless/IPM).
### 1. Using [IPM](https://github.com/efabless/IPM):
- [Optional] If you do not have IPM installed, follow the installation guide [here](https://github.com/efabless/IPM/blob/main/README.md)
- After installing IPM, execute the following command ```ipm install EF_QSPI_XIP_CTRL```.
> **Note:** This method is recommended as it automatically installs [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) as a dependency.
### 2. Cloning this repo: 
- Clone [EF_IP_UTIL](https://github.com/efabless/EF_IP_UTIL.git) repository, which includes the required modules from the common modules library, [ef_util_lib.v](https://github.com/efabless/EF_IP_UTIL/blob/main/hdl/ef_util_lib.v).
```git clone https://github.com/efabless/EF_IP_UTIL.git```
- Clone the IP repository
```git clone github.com/efabless/EF_QSPI_XIP_CTRL```

### The Wrapped IP Interface 

>**_NOTE:_** This section is intended for advanced users who wish to gain more information about the interface of the wrapped IP, in case they want to create their own wrappers.

<img src="docs/_static/EF_QSPI_XIP_CTRL.svg" width="600"/>

#### Module Parameters 

|Parameter|Description|Default Value|
|---|---|---|
|NUM_LINES|The cache number of lines.|16|
|LINE_SIZE|The cache line size in bytes.|32|
|RESET_CYCLES|The number of cycles needed for the s/w reset command; reset time = (RESET_CYCLES + 1) * 2 /(HCLK frequency).|999|

#### Ports 

|Port|Direction|Width|Description|
|---|---|---|---|
|sck|output|1|SPI serial clock|
|ce_n|output|1|SPI chip select (Active Low).|
|dout|output|4|Flash controller SPI data out.|
|din|input|4|Flash controller SPI data in.|
|douten|output|4|Flash controller data out enable (Active Low)|
