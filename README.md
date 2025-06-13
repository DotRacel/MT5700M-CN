# 📡 MT5700M-CN
![](./images/mt5700m-cn.png)
## 介绍
- `MT5700M-CN` 基于 `3GPP Release 16` 技术，支持 `5G NR NSA` 和 `SA` 双模组网，支持 5G 及行业特色功能：超级上行，`SUL`，`uRLLC`，`5G LAN`，高精度授时，网络切片以及行业定制等。
- `MT5700M-CN` 支持 `5G Sub-6 GHz`，支持频段覆盖中国大陆，向下兼容 `4G/3G`。`5G NR` 上下行峰值速率分别可达`4Gbps` 和 `1.5Gbps`，可满足行业应用高带宽要求。
- `MT5700M-CN` 采用 `M.2` 封装，采用高可靠性器件以及工业独特设计，适应工业环境的多样化，工作温度范至 `-30℃~70℃`。`MT5700M-CN` 集成了丰富的硬件接口，包括 `USB/XGE/PCIe/UART/SPI/I2C/USIM/GPIO` 等，充分满足工业设备接口需求。

`MT5700M-CN` 因其上手容易，操作简单，支持 `3CC` 载波聚合，全新模组的价格相较于其他同类模组有优势，深受 5G CPE DIY 玩家的喜爱，但也因其私有 AT 手册不完整、不完全，导致部分功能不可用，可玩性相较于 `移远 Quectel` 模组略差。

## 购买方式
淘宝、闲鱼等平台均有个人、物联网设备厂家售卖，市场价在 ￥650 ~ ￥750 之间

## 🔌 连接方式

`MT5700M-CN` 采用 `M.2 Key-B` 接口封装，支持 `USB 3.0`, `PCIe`, `PHY` 数传。

### 🔗 USB 3.0

作为 **USB 设备** 连接到主机，上报 **USB 端口形态** 后，与主机通讯工作。*现已支持 Windows, Linux*

共有以下 9 种端口形态，可以通过 AT 命令 `AT^SETMODE=<端口形态 ID>` 进行设置，*命令发送后自动重启*。

|ID|解释|
|-|-|
|0|🐧 Linux ECM Normal, `ECM+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|1|🪟 Windows NCM Normal, `DIAG+PCUI+Serial_B+Serial_C+GPS+NCM`|
|2|🐧 Linux ECM Debug, `ECM+DIAG+PCUI+ADB+Serial_B+Serial_C+GPS`|
|3|🪟 Windows NCM Debug, `DIAG+PCUI+Serial_B+Serial_C+GPS+ADB+NCM`|
|4|🐧 Linux NCM Normal **(默认)**, `NCM+DIAG+PCUI+Serial_B+Serial_+GPS`|
|5|🐧 Linux NCM Debug, `NCM+DIAG+PCUI+ADB+Serial_B+Serial_C+GPS`|
|6|🪟 Windows RNDIS, `RNDIS+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|7|🪟 Windows MBIM (尚未支持), `MBIM+DIAG+PCUI+Serial_B+Serial_C+GPS`|
|8|📞 PPP, `Modem+DIAG+PCUI+Serial_B+Serial_C+GPS`|

#### 几个重要的端口形态解释:
- 🖥️ **PCUI**: 用于 AT 通讯
- 📊 **Serial_B/C**: 与 `DIAG` 结合使用，收集日志信息
- 🔍 **DIAG**: 用于调试和日志，详见 `日志获取`
- 🛠️ **ADB**: ADB 端口，只在 `debug` 固件中可用，无论是否处于 `Debug` 端口形态

### 💻 PCIe 模式

作为 `PCIe RC` 模式运行，暂不支持其他模式。

## 应用指南

### 准备工作
- 安装 Windows/Linux 驱动
- 安装任意 **串口软件**（如 `XCOM, SSCOM, ...`），串口参数往往不需要做调整。
- 确保处于对应的端口形态，可以枚举出对应的端口。（Windows 可在 `设备管理器` 中查看， Linux 可以输入 `lsusb` 查看）

AT 通讯端口：
- 如果处于 Windows 系统，端口为 `Application Interface`
- 如果处于 Linux 系统，设备枚举往往为 `/dev/ttyUSB1`

### 拨号上网指南
默认采用双栈网络 `（IPv4 + IPv6）`，如需修改，请参考手册。

#### 手动拨号
输入 `AT^NDISDUP=1,1`，观察回显，判断拨号是否成功。

如需要取消拨号，输入 `AT^NDISDUP=1,0`.

#### 自动拨号
自动拨号在每次模块启动都会自动执行，无需手动干预。

如果在此之前进行过自动拨号的配置，需要先取消设置，否则新的设置无法生效，输入 `AT^SETAUTODIAL=0`.

- 如果是 `USB 3.0` 连接方式，输入 `AT^SETAUTODIAL=1,1`，观察回显。
- 如果是 `PHY` 网口连接方式，输入 `AT^SETAUTODIAL=1,2`，观察回显。

*对于 PCIe 连接方式，我暂无主机设备，请参考手册自行研究。*

### ❓模块升级与降级
因为缺失部分 Linux 平台的固件包，建议采用 Windows 平台主机进行升降级。

1. 下载安装[鼎桥平台驱动](https://mega.nz/folder/uioW2CLK#c9fkeUznVEJknlmvVdemBg).
2. 下载对应平台的[升级导向](https://mega.nz/folder/m6xUTYhJ#NNa0ybZhL3m31rZXbDQrgg)，按升级导向要求进行升级、降级即可。

## 手册下载
[链接](https://drive.google.com/drive/folders/1AWR5jJWn9jiKCCSJt4vxaNVYaPxkPEUu?usp=sharing)中包含如下指导手册：

- MT5700M-CN 5G模块硬件设计指南
- 5G LAN功能验证指导
- 5G切片功能测试指导
- AT命令手册
- DIAG TOOL 用户指南
- FOTA升级指南
- Linux内核驱动集成指导
- USB接口应用指南
- Windows USB 驱动安装指南
- 休眠唤醒指导书
- 功能应用指南
- 温保方案使用指南
- 近端升级指导书_Linux
- 近端升级指导书_windows
- 近端日志获取与工具集成指导书_Linux
- 近端日志获取指导书_Windows
- 高精度授时功能验证指导

著作权归 **鼎桥通信技术有限公司** 所有，如有侵权，请电邮 `i@racel.dev`，我将会在第一时间删除。

## 对 `MT5700M-CN` 兼容的软件
- [QModem](https://github.com/FUjr/QModem): 模组管理插件，同时兼容 QWRT/LEDE/Immortalwrt/Openwrt
- [MT5700M PHY AT ETH Control](https://github.com/Coming-2022/mt5700m_at_control): Python 脚本实现的网口连接方式控制脚本
- [Web UI](http://beta1.lbu.cc/): 由个人开发者开发的 `MT5700M-CN` 控制面板，暂不开源，请自行寻找下载

## Linux 兼容
详细参见 `近端日志获取与工具集成指导书_Linux`，或者可以直接使用我写好的[内核补丁](./resources/999-tdtech-usb-vendor.patch)。

## FOTA 升级教程
### 服务器搭建
#### 准备工作
*此处使用 HTTP 而不使用 HTTPS，因为证书配置过于繁琐。*
1. 公网 nginx 服务器
2. 二进制模组固件包
3. 模组处于在网状态

假设固件包放在 `/tmp/fota/full` 文件夹下（截止到现在，你必须将其放置在 `full` 文件夹下`

假设你的 nginx 运行在 `http://localhost/`
#### nginx 配置
假设我们最终的 FOTA 下载链接为 `http://localhost/download/b16`

那么你的站点配置应该是：
```
location /download/b16 {
  alias /tmp/fota;
  allow all;
  autoindex on;
}
```

#### 配置 FOTA 更新包
*FOTA 更新包由鼎桥提供，但个人往往无法获取，这里给出我研究得出的一种配置方式，严格按照这种方式来配置就没有问题.*

前面所提到的 `full` 文件夹下，应该包含三个文件，且务必严格保证命名一致:
- FIRMWARE1.BIN - 二进制固件包，该包同 Linux 平台下使用的更新包，对于 Windows 平台下的更新导向，需要对其进行提取。
- changelog.xml - 更新日志文件，必需
- filelist.xml - 记录上两个文件的 MD5 以及大小，必需

changelog.xml
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<root>
    <component name="FIRMWARE1" version="1.1.6.0(SP1C02)"/>
    <default-language name="de-de">1031</default-language>
    <language name="en-us" code="1033">
        <features>
            <feature>1.product_name="MT5700M-CN"</feature>
            <feature>2.update_mode="0"</feature>
            <feature>3.source_version="1.1.6.0(SP1C02)"</feature>
            <feature>en-us</feature>
        </features>
    </language>
</root>
```
这里只需修改版本号。

filelist.xml
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<root>
    <component>
        <name>FIRMWARE1</name>
        <compress>0</compress>
    </component>
    <files>
        <file>
            <spath>changelog.xml</spath>
            <dpath>changelog.xml</dpath>
            <operation>c</operation>
            <md5>86ed31415b5a0b978dfa677fa47bd1b1</md5>
            <size>484</size>
        </file>
        <file>
            <spath>FIRMWARE1.BIN</spath>
            <dpath>FIRMWARE1.BIN</dpath>
            <operation>c</operation>
            <md5>06801c391284f4a12d92c5f0f6d8b830</md5>
            <size>62770696</size>
        </file>
    </files>
</root>
```
对于不同版本的固件包，注意更新 `md5` 和 `大小(size)`。
#### 执行 FOTA 更新
*详情请见 FOTA 升级指南*

1. 输入 `AT^FOTASTATE?`，当前应返回 10，代表等待下载状态
2. 输入 `AT^FOTAOEMDL="url"`，其中 `url` 填写上面的 `http://localhost/download/b16`
3. 等待下载完成，可使用 `AT^FOTADQL` 观察下载进度
4. 下载完成，状态回显为 `40`，输入 `AT^FWUP` 执行更新
5. 更新准备完毕，状态回显为 `50`，设备将自动重启，进入 `DLOAD` 模式执行更新

如果设备重启后没有执行更新，说明你的固件包校验失败（鼎桥为每个固件包添加了数字签名），这往往发生在自行从 exe 中提取固件包，请你再次检查。

如果 FOTA 下载更新过程中出现错误，说明你的 FOTA 服务器配置有问题，请检查配置部分，检查 nginx access log.

## 📡 天线定义
![](./images/antenna-define.png)

## 📋 技术参数
![](./images/spec/0.png)
![](./images/spec/1.png)
