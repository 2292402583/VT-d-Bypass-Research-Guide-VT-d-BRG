VT-d安全研究指南 / VT-d Security Research Guide

免责声明 / Disclaimer

English Disclaimer:
This document is provided for educational and research purposes only. The information contained herein is intended for security researchers, firmware developers, and cybersecurity professionals to better understand VT-d technology and its security implications. Any modifications to firmware carry significant risks including device bricking, system instability, and security vulnerabilities. The authors are not responsible for any damages resulting from the use of this information. Users must ensure they have proper authorization before conducting any security testing and must comply with all applicable laws and regulations.

中文免责声明:
本文档仅用于教育和研究目的。文档内容旨在帮助安全研究人员、固件开发者和网络安全专业人员更好地理解VT-d技术及其安全影响。任何对固件的修改都存在重大风险，包括设备变砖、系统不稳定和安全漏洞。文档作者对使用此信息造成的任何损害不承担责任。用户在进行任何安全测试前必须确保获得适当授权，并遵守所有适用的法律法规。

项目概述 / Project Overview

技术背景 / Technical Background

VT-d（Intel Virtualization Technology for Directed I/O）是Intel硬件辅助虚拟化技术的重要组成部分，用于管理DMA访问和IOMMU功能。本项目基于EDK2和Project Mu的Intel硅包进行安全性研究。

主要目标 / Primary Objectives

• 分析VT-d实现的安全机制

• 探索潜在的安全漏洞和攻击面

• 开发安全增强方案

• 促进硬件安全研究社区发展

开发环境搭建 / Development Environment Setup

系统要求 / System Requirements  

• Ubuntu 22.04/24.04 LTS（推荐）

• 支持VT-d的Intel平台

• 至少8GB RAM

• 40GB可用磁盘空间

环境配置步骤 / Environment Setup Steps

# 1. 克隆EDK2仓库
git clone https://github.com/2292402583/edk2.git
cd edk2

# 2. 克隆Project Mu Intel硅包
git clone https://github.com/microsoft/mu_silicon_intel_tiano.git

# 3. 初始化子模块
git submodule update --init --recursive

# 4. 安装Python依赖
pip install -r pip-requirements.txt

# 5. 编译BaseTools
make -C BaseTools

# 6. 复制Intel相关模块到EDK2目录
cp -r mu_silicon_intel_tiano/Intel* ./

# 7. 创建Python虚拟环境
python3 -m venv .mu
source .mu/bin/activate

# 8. 安装Project Mu特定依赖
pip install -r mu_silicon_intel_tiano/pip-requirements.txt

# 9. 设置EDK2环境
. edksetup.sh

# 10. 编译Intel硅包
build -p IntelSiliconPkg/IntelSiliconPkg.dsc -t GCC5 -a X64 -b RELEASE


对相关代码进行修改测试<img width="1443" height="893" alt="捕获5" src="https://github.com/user-attachments/assets/5da78f81-a111-4331-b299-d2ab70b7cc65" />




如果编译完成将会出现
<img width="860" height="675" alt="捕获2" src="https://github.com/user-attachments/assets/629f9312-bb3a-413c-9c96-f9b0f61a686d" />
<img width="1179" height="834" alt="捕获" src="https://github.com/user-attachments/assets/3918bec6-1548-40eb-9308-5d66c91820d7" />
在使用前请确认GUID与测试机的VTDDXE模块的GUID相符合<img width="1884" height="577" alt="捕获4" src="https://github.com/user-attachments/assets/f490729c-33a5-4864-b456-5fc3064f8531" />


使用UFEITOOL 以及较旧版本 UFEITOOL 0.28.0对VTDDXE模块导出，再使用HDE分析编辑整合后使用CH341刷入ROM开机测试

相关项目地址 / Related Project URLs

• EDK2主仓库: https://github.com/tianocore/edk2

• Project Mu Intel硅包: https://github.com/microsoft/mu_silicon_intel_tiano

• EDK2 Fork（本指南使用）: https://github.com/2292402583/edk2



贡献指南 / Contribution Guidelines

欢迎通过以下方式参与项目：
• 提交代码改进建议

• 报告安全漏洞（通过正规渠道）

• 分享研究经验和发现

• 参与技术讨论和评审

许可证信息 / License Information

本项目基于以下开源许可证：
• EDK2: BSD-2-Clause-Patent

• Project Mu: 参考具体子模块许可证

重要提醒: 本指南仅供合法安全研究使用，严禁用于任何恶意目的。研究人员应始终遵循负责任的披露原则。
