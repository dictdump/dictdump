[English](readme.md) | [日本語](readme.ja.md) | [简体中文](readme.zh-Hans.md)

# Electronic Dictionary Firmware

This project contains a collection of firmware and data for Casio Ex-Word electronic dictionaries. Dumped using this script: https://github.com/dictscript/dictscript

## Directory Structure

-   `nor-and-nand/`: Stores NOR and NAND firmware images for different dictionary models.
    -   `<model>/nor/`: Stores NOR images.
        -   `1fxxxcleaned-true`: Indicates that the extracted NOR data has been cleaned.
        -   `trimmed-true`: Indicates that trailing blank `FF` data has been trimmed from the file.
        -   `unlocked-true`: Indicates that the Test Menu password has been unlocked.
    -   `<model>/nand/`: Stores NAND images.
        -   `builded-nand-from-extracted-files`: NAND image built from extracted files.
        -   `extracted-nand-files-from-device`: NAND files extracted from the device.
-   `nor-and-nand-extracted/`: Stores the contents extracted from resource files in the NOR and NAND of the dictionary.
-   `nor-and-nand-updater/`: Stores firmware updaters.
    -   `CY-series-dataplus5-updater/UPDADN3.BIN`: Updater for DP5 series.
    -   `L-series-dataplus4-updater/UPDADN2.BIN`: Updater for DP4 series.
-   `addons-on-dictionary/`: Stores additional dictionaries.
-   `addons-on-dictionary-extracted/`: Stores content extracted from resource files in additional dictionaries.

> **Note**: Files larger than 100MB are compressed and split (*.xz.001, *.xz.002...). Please merge and decompress them to get the original files.

### Flashing Guide

The flashing process is performed in the dictionary's engineering mode (Test Menu).

1.  **Enter Test Menu**:
    1.  Ensure the dictionary is **powered off**.
    2.  Press and hold **Exit + Page Up + Power** for about five seconds until the screen turns on and displays a "Model" window.
    3.  Release the keys, then press the **Right key twice**, and then press the **Enter key** to enter the menu.

2.  **Prepare TF Card**: Select the corresponding option in the Test Menu to format a TF card (2GB recommended).

3.  **Prepare Firmware Files**:
    -   **NOR Firmware**: Select a suitable NOR image from the `nor-and-nand/<model>/nor/` directory. The `unlocked-true` version is recommended. Rename it (e.g., `CY123OSB.BIN`) and copy it to the root of the TF card.
    -   **NAND Firmware** (Optional): Build with `nand_build.py` or select a NAND image from `nor-and-nand/<model>/nand/` (e.g., `CY123D0B.bin`) and copy it to the root of the TF card.
    -   **Updater Program**: Depending on your dictionary model, select `UPDADN2.BIN` or `UPDADN3.BIN` from the `nor-and-nand-updater/` directory and copy it to the root of the TF card (`UPDADN2.BIN` may be the firmware updater for the series whose file names begin with LY, and `UPDADN3.BIN` may be for newer models whose file names begin with CY).

4.  **Start Flashing**:
    -   Insert the TF card containing the above files into the dictionary.
    -   Select `OS UPDATE` or the corresponding option in the Test Menu to start the flashing process.

> **Note**: Flashing carries risks. Be sure to back up your data.
