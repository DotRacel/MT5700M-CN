# Table of Contents
- [Table of Contents](#table-of-contents)
- [MT5700M-CN](#mt5700m-cn)
  - [Connection Methods](#connection-methods)
  - [Related Resources](#related-resources)
  - [Specification](#specification)

# MT5700M-CN
![](./images/mt5700m-cn.png)

The MT5700M-CN supports 5G NR NSA and SA dual-mode networking, along with 5G and industry-specific features such as 3CC carrier aggregation, Super Uplink (SUL), uRLLC, 5G LAN, and more. It supports 5G Sub-6 GHz with frequency band coverage for **mainland China** and is backward compatible with 4G/3G. The peak downlink and uplink rates of 5G NR reach up to 4 Gbps and 1.5 Gbps, respectively. It is encased in an M.2 package and integrates a rich set of hardware interfaces.

## Connection Methods
The MT5700M-CN module features an external interface in the form of an **M.2 Key-B interface**.

It has adapted `ECM, NCM, and RNDIS` universal drivers in kernel version **2.6.22 and later**. The default interfaces integrated with the USB serial port driver include: `PCUI, Diag, SerialB, SerialC, ECM, NCM, and GPS`.

## Related Resources
- [MT5700M PHY AT ETH Control](https://github.com/Coming-2022/mt5700m_at_control)
- [luci-app-modem with support](https://github.com/Siriling/openwrt-app-actions/tree/c3c47cb0aeb4652bcc6f27e76ec1be8b5f74edec/applications/luci-app-modem)
- [MT570X Windows USB Driver](./drivers/MT570X-user-windows.zip)
- More coming soon...

## Specification
![](./images/spec/0.png)
![](./images/spec/1.png)