# Table of Contents
- [Table of Contents](#table-of-contents)
- [MT5700M-CN](#mt5700m-cn)
  - [Connection Methods](#connection-methods)
    - [USB Modes](#usb-modes)
    - [PCIe Mode](#pcie-mode)
  - [Related Resources](#related-resources)
  - [Specification](#specification)

# MT5700M-CN
![](./images/mt5700m-cn.png)

The MT5700M-CN supports 5G NR NSA and SA dual-mode networking, along with 5G and industry-specific features such as 3CC carrier aggregation, Super Uplink (SUL), uRLLC, 5G LAN, and more. It supports 5G Sub-6 GHz with frequency band coverage for **China** mainly and is backward compatible with 4G/3G. The peak downlink and uplink rates of 5G NR reach up to 4 Gbps and 1.5 Gbps⚡

## Connection Methods

The MT5700M-CN module features an external interface in the form of an **M.2 Key-B interface**.

### USB Modes

It only supports application scenarios as a **USB DEVICE**. A DEVICE does not have the ability to initiate communication actively and must wait for instructions from the HOST. It is recognized by the HOST through a hardware connection and handshake process, and during the enumeration process, it provides descriptor information (such as device ID, vendor ID, function description, etc.) to allow the HOST to understand its capabilities and complete the configuration.

When used as a *DEVICE*, there are a total of 9 USB port configuration modes, which can be switched using the command `AT^SETMODE=<mode>`.

|Mode|Description|
|-|-|
|0|Linux ECM Normal, `ECM+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|1|Windows ECM Normal,  `DIAG+PCUI+Serial_B+Serial_C+GPS+NCM`|
|2|Linux ECM Debug, `ECM+DIAG+PCUI+ADB+Serial_B+Serial_C+GPS`|
|3|Windows ECM Debug, `DIAG+PCUI+Serial_B+Serial_C+GPS+ADB+NCM`|
|4|Linux NCM Normal(Default), `NCM+DIAG+PCUI+Serial_B+Serial_+GPS`|
|5|Linux NCM Debug, `NCM+DIAG+PCUI+ADB+Serial_B+Serial_C+GPS`|
|6|Windows RNDIS, `RNDIS+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|7|Windows MBIM (Not Supported Yet), `MBIM+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|8|PPP, `Modem+DIAG+PCUI+Serial_B+Serial_C+GPS`|

It can be observed that, regardless of the mode, the following serial ports are always provided:
- **PCUI**: Used for AT command communication
- **Serial_B/C**: Used in conjunction with DIAG for log collection
- **DIAG**: Used for debugging and collecting log information

Only in debug modes will **ADB** be provided.

### PCIe Mode

The module supports PCIe RC (Root Complex) mode **ONLY**. In this mode, the modem will act as the host, providing network support for other endpoint devices like an Ethernet chipset or a WiFi chipset.

-  By using the command `AT^TDPCIELANCFG=2`, the network port PHY chip type connected to the PCIe bus can be set to `RTL8125` (supporting a 2.5Gbps rate). The default setting for `AT^TDPCIELANCFG` is 1, which corresponds to `RTL8111` (supporting a 1Gbps rate).

It has adapted `ECM, NCM, and RNDIS` universal drivers in kernel version **2.6.22 and later**. The default interfaces integrated with the USB serial port driver include: `PCUI, Diag, SerialB, SerialC, ECM, NCM, and GPS`.

## Related Resources
- [MT5700M PHY AT ETH Control](https://github.com/Coming-2022/mt5700m_at_control)
- [luci-app-modem with support](https://github.com/Siriling/openwrt-app-actions/tree/c3c47cb0aeb4652bcc6f27e76ec1be8b5f74edec/applications/luci-app-modem)
- [MT570X Windows USB Driver](./drivers/MT570X-user-windows.zip)
- [TD-Tech MT5700 PPT](./images/other/TD-Tech%205G%20MT5700%20Series%20202303.pptx)
- More coming soon...

## Specification
![](./images/spec/0.png)
![](./images/spec/1.png)