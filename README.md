### 嵌入式软件 · 从裸机驱动到上位机

写能跑在板子上的代码，也写能连上板子的程序。关注实现是否可调试、参数是否可复现。

---

## 技术栈

| 层面 | 内容 |
| --- | --- |
| MCU | STM32F103 / F4 系列 |
| 语言 | C（主力）、C#、少量 C++ |
| 工具链 | Keil MDK、ARM Compiler 5 / 6、GCC（MinGW-w64）、J-Link / ST-Link |
| 底层 | STM32 标准外设库、HAL、定时器 PWM 与输入捕获、ADC、USART、I2C、FreeRTOS |
| 外设 | 直流电机与 H 桥驱动、舵机、HC-SR04、红外 NEC 解码、OLED、四路循迹 |
| 上位机 | WinForms / WPF、TCP Socket、MySQL |

## 项目

### [My_Car](https://github.com/ThisLovely/My_Car) · STM32 红外遥控 + 超声波避障小车

双轮差速平台，标准外设库裸机实现。红外 NEC 解码做五向遥控与分档调速；避障采用单超声波 + 舵机扫视，前方受阻时左右各测一次再择向绕行。驱动层与协议层分离，统一暴露 `XXX_Init()` 接口，应用层不碰寄存器。

### [ARMCC](https://github.com/ThisLovely/ARMCC) · ARM Compiler 5.06 文件集

Keil MDK 从 5.37 起不再随包分发 AC5，只保留基于 Clang 的 AC6，大量标准外设库老工程因此打不开。这里归档了 AC5 的完整安装前缀（`bin` / `include` / `lib` / `sw`），放进 `ARM\ARMCC` 即可恢复编译。

### [mingw64](https://github.com/ThisLovely/mingw64) · Windows x64 GCC 工具链

MinGW-w64 GCC 15.2.0 完整前缀，posix 线程 + SEH 异常 + UCRT。用于在 Windows 上搭 VSCode 的 C/C++ 环境，仓库 README 给出了 `tasks.json`、`c_cpp_properties.json`、`launch.json` 三份可直接复制的配置。

## 仓库说明

`My_Car` 是工程本体，`ARMCC` 与 `mingw64` 是开发环境归档——把踩过的坑连同可用的文件一起留下来，省掉别人重新找一遍的时间。

---

<sub>代码优先，说明其次。仓库里的问题欢迎开 Issue 讨论。</sub>
