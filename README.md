# 你好，我是邹志伟 👋

嵌入式开发 · C 语言 · STM32 · 嵌入式 Linux

从单片机做到 Linux 服务端，独立完成过一个完整的 IoT 数据链路：
**传感器采集 → 无线上报 → 服务端落库 → Web 监控**。

---

## 代表项目

### 1. 温控风扇 IoT 系统（设备端 + 服务端，全链路独立完成）

一套自己从头写到尾的系统，不是教程复刻。

**设备端** — [stm32-esp8266-iot-gateway](https://github.com/zzw200498-hue/stm32-esp8266-iot-gateway)
- STM32F103 + 标准库裸机开发，DHT11 采集温湿度、OLED 显示、PWM 无级调速、旋转编码器手动控速
- ESP8266（AT 指令）WiFi 上报，TCP 长连接 + 心跳保活，断线由服务端感知
- 含开发报告、BOM、原理图、7 条踩坑记录

**服务端** — [fan-iot-server](https://github.com/zzw200498-hue/fan-iot-server)
- Linux C 手写，不依赖任何网络框架
- `epoll` 非阻塞 IO，自行处理 TCP 粘包切分
- 网络线程 / 工作线程分离，互斥锁 + 条件变量实现有界消息队列（满则丢包，保护网络线程不被阻塞）
- SQLite 持久化：每线程独立连接 + WAL 模式 + busy_timeout
- HTTP 接口提供历史查询与远程控制，浏览器直接打开监控台
- 信号驱动的优雅退出（SIGINT/SIGTERM），按 HTTP → 队列 → worker → 数据库 反序关停

**结果**：控温误差 ≤ ±1.0℃，连续运行 24 小时无异常。

---

### 2. STM32 智能温控风扇 — [STM32-Smart-Fan](https://github.com/zzw200498-hue/STM32-Smart-Fan)

自动 / 手动双模式闭环控温。高于 25℃ 线性调速，低于 20℃ 切编码器手动控制（4 级步进）；
PWM 频率锁定 25kHz 彻底消除电机啸叫；TIM2 中断驱动蜂鸣器高温报警 + 双色 LED 三级温度指示。

---

### 3. Snake-C — [Snake-C](https://github.com/zzw200498-hue/Snake-C)

C 语言工程能力递进演示：控制台原始版 → 控制台优化版 → Win32 图形版。
同一份游戏逻辑的三次重构，能看到代码是怎么从「能跑」变成「好维护」的。

---

### 4. linux-c-quiz — [linux-c-quiz](https://github.com/zzw200498-hue/linux-c-quiz)

VSCode 插件：C 语言 / Linux 知识点刷题工具。YAML 维护题库，TypeScript 开发，MIT 协议。

---

## 技术栈

| 方向 | 内容 |
|---|---|
| 语言 | C（熟练）、TypeScript、Shell |
| 单片机 | STM32F103 标准库开发，GPIO / 中断 / 定时器 / PWM / ADC / DMA / I2C / SPI / USART / 看门狗 |
| 嵌入式 Linux | 文件 IO、进程与 IPC、多线程与同步（pthread / 互斥锁 / 条件变量）、Socket 网络编程、epoll 多路复用、守护进程 |
| 存储 | SQLite（预处理语句、WAL、多线程连接管理） |
| 工具链 | GCC / GDB / Makefile / Git / Keil MDK / STM32CubeMX / OpenOCD |
| 硬件调试 | 万用表、示波器、逻辑分析仪，能独立读原理图与英文数据手册 |

---

## 学习轨迹

```
2026.07           2026.07-08          2026.08-10          2026.10
   │                  │                   │                  │
   ▼                  ▼                   ▼                  ▼
┌────────┐      ┌────────────┐     ┌────────────┐     ┌──────────────┐
│ C 语言  │─────▶│  STM32     │────▶│ Linux 应用 │────▶│ IoT 综合实战  │
│ 系统复习│      │ 全外设开发  │     │ 系统编程   │     │ 固件+服务端   │
└────────┘      └────────────┘     └────────────┘     └──────────────┘
```

过程中沉淀的 31 个外设练习工程与 Linux 学习笔记，保留在私有仓库，不占用公开列表。

---

## 联系

- 目标岗位：嵌入式 Linux 应用开发 / 嵌入式软件开发
- 状态：2027 届本科应届，可实习
- 交流：欢迎在本仓库提 Issue
