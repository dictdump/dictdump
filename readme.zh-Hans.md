[English](readme.md) | [日本語](readme.ja.md) | [简体中文](readme.zh-Hans.md)

# 电子词典固件

本项目包含一系列卡西欧（Casio Ex-Word）电子词典固件和数据。 使用这个脚本提取： https://github.com/dictscript/dictscript

## 目录结构

-   `nor-and-nand/`: 存放不同型号词典的 NOR 和 NAND 固件镜像。
    -   `<model>/nor/`: 存放 NOR 镜像。
        -   `1fxxxcleaned-true`: 表示清除了提取的 NOR 数据。
        -   `trimmed-true`: 表示截去了文件尾部的空白 `FF` 数据。
        -   `unlocked-true`: 表示已解锁 Test Menu 的密码。
    -   `<model>/nand/`: 存放 NAND 镜像。
        -   `builded-nand-from-extracted-files`: 从提取的文件构建的 NAND 镜像。
        -   `extracted-nand-files-from-device`: 从设备上提取的 NAND 文件。
-   `nor-and-nand-extracted/`: 存放从词典的 NOR 和 NAND 中的资源文件提取的内容。
-   `nor-and-nand-updater/`: 存放固件更新程序。
    -   `CY-series-dataplus5-updater/UPDADN3.BIN`: 用于 DP5 系列的更新程序。
    -   `L-series-dataplus4-updater/UPDADN2.BIN`: 用于 DP4 系列的更新程序。
-   `addons-on-dictionary/`: 存放附加词典。
-   `addons-on-dictionary-extracted/`: 存放从附加词典中的资源文件提取的内容。

> **注意**: 大于100MB的文件被压缩分割了（*.xz.001, *.xz.002 ...）请合并解压后获取原始文件。

## 刷机指南

刷机流程需要在词典的工程模式（Test Menu）下进行。

1.  **进入 Test Menu**:
    1.  确保词典处于**关机**状态。
    2.  同时按住 **退出 + 上翻页 + 电源键** 约五秒钟，直到屏幕亮起并显示 "Model" 窗口。
    3.  松开按键，然后按 **两下右键**，再按 **输入键** 即可进入菜单。

2.  **准备 TF 卡**: 在 Test Menu 中选择相应选项，格式化一张 TF 卡（推荐 2GB）。

3.  **准备固件文件**:
    -   **NOR 固件**: 从 `nor-and-nand/<model>/nor/` 目录中选择一个合适的 NOR 镜像。推荐使用 `unlocked-true` 版本。将其重命名（例如 `CY123OSB.BIN`）并复制到 TF 卡根目录。
    -   **NAND 固件** (可选): 使用 `nand_build.py` 构建或从 `nor-and-nand/<model>/nand/` 中选择 NAND 镜像 (例如 `CY123D0B.bin`)，并复制到 TF 卡根目录。
    -   **更新程序**: 根据您的词典型号，从 `nor-and-nand-updater/` 目录中选择 `UPDADN2.BIN` 或 `UPDADN3.BIN`，并复制到 TF 卡根目录（`UPDADN2.BIN`可能是用于文件名LY开头的系列的固件的更新程序，`UPDADN3.BIN`可能是用于文件名CY开头的新一些型号）。

4.  **开始刷机**:
    -   将包含上述文件的 TF 卡插入词典。
    -   在 Test Menu 中选择 `OS UPDATE` 或相应选项开始刷机流程。

> **注意**: 刷机有风险，请务必备份您的数据。