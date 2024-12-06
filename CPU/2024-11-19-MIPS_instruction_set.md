---
title: MIPS 指令集
date: 2024-11-19
tags: CPU
categories: 学习
---

# MIPS 指令集

任何指令执行的第一步都是取指令

## 指令集功能需求

1. 存储器（MEM）
    1. 指令存储器 & 数据存储器 (分离的存储器模拟了 cache 结构)
    2. 指令存储器只有读取数据功能(取指令)
    3. 数据寄存器既有读取数据功能又有写入数据功能
2. 寄存器堆 (32个32位寄存器)
    1. 能同时读出 rs 和 rt 两个寄存器
    2. 可以写数据到 rt 和 rd 寄存器
3. PC - 获取当前正在执行的指令
4. NPC - 下一条指令地址的计算单元
5. 扩展立即数 (零扩展和符号扩展)
6. ALU - 执行 ADD, SUB, OR 等运算的计算单元

## 数据通路的主要功能部件

1. 指令寄存器 (IM - instruction memory)
    + 读数据：输入地址，输出数据 (即指令)
2. 数据存储器 (DM - data memory)
    - 读数据：输入地址，输出数据1
    - 写数据：输入地址和数据
3. 寄存器堆 (RF - register file)
    - 读寄存器：输入两个寄存器编号，输出两个 32 位值
    - 写寄存器：输入写寄存器编号 & 一个32位值
4. PC
5. NPC (NextPC)
    - 计算下一个PC 值：输入PC，输入 Imm，输出计算结果
6. ALU (mrithmetic logic unit)
    - ADD, SUB, OR ：输入两个操作数，输出计算结果