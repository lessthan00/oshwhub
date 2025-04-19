# [电路已验证;基于VL813的USB3.0-HUB设计](https://oshwhub.com/goodyuhuang/ji-yu-VL813de-USB3.0-HUBshe-ji)

[VL160 - USB-C™ 2：4 数据开关，带 CC 功能，适用于 USB 3.1](https://www.via-labs.com/product_show.php?id=72)
[VL813 - 超高速 USB 3.0 集线器控制器](https://www.via-labs.com/product_show.php?id=81)

1、此版本电源切换电路存在一定缺陷，不过不妨碍使用。缺陷详见原理图，计划下个版本改进。
3、EEPROM用于存放固件升级，不焊接也不会影响使用。
4、阻抗按1.0mm板厚双层板设计，使用嘉立创的计算工具得到。为更好的阻抗匹配打样时请打样1.0mm的板厚。

更正VER1.0提及的第二点。之前只有一面USB3.0是芯片问题，焊接新的芯片后无论USBA-TypeC还是TypeC-TypeC都能实现双面USB3.0速度。
3、使用2.5寸硬盘测试过，在HUB不外接电源时读取速度能达到290M/S。2.5寸硬盘直接接电脑测速为280M/S左右。

1、USB3.0与USB2.0差异
USB2.0的座子一般为白色，USB3.0的座子一般为蓝色。
USB2.0只有一组差分线DP/DM。USB3.0有两组差分线TX_P&TX_N/RX_P&RX_N。
USB3.0速率最高为480Mbps，而USB3.0根据不同Gen有不同速率

3、USB3.0设计注意事项
阻抗控制： 建议USB3.0的差分阻抗控制90Ω误差10%，USB2.0差分阻抗控制90Ω误差10%。
时延控制： 建议USB3.0差分对内需等长设计，误差小于5mil。USB2.0等长误差控制小于10mil。
隔直电容： 建议选取0402以下封装电容，容值官方SPEC要求75nF-265nF之间，布局时靠近端子放置。
对内交叉： USB3.0 的P/N如果走线上有交差，可以将差分对的P/N交换，USB3允许P/N反转。

4、其它设计知识
CC引脚： Configuration Channel，通道配置引脚。这是 Type-C 的关键通道。它的作用有检测正反插、检测USB连接识别、提供多大电压和电流、USB设备间数据与VBUS的连接建立与管理等。市面上通用快充线与普通数据线（双Type-C接口）区别就在CC引脚。
DFP： Downstream Facing Port，下行端口，可以理解为Host，DFP提供VBUS、数据。在协议规范中DFP特指数据的下行传输，笼统意义上指的是数据下行和对外提供电源的设备。典型的DFP设备是电源适配器。
UFP： Upstream Facing Port，上行端口，可以理解为Device，UFP从VBUS中取电，并可提供数据。典型的UFP设备是U盘，移动硬盘。