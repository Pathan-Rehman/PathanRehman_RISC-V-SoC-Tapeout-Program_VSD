# Task-2 Installation of OpenSource EDA Tools

***

## Installing a Virtual Machine

### Install VirtualBox

<img width="1877" height="860" alt="image" src="https://github.com/user-attachments/assets/74157767-002a-4ed0-80cf-637b8ad0e3bf" />

1. Go to the [VirtualBox website](https://www.virtualbox.org/).

<img width="1846" height="851" alt="image" src="https://github.com/user-attachments/assets/51eedcec-9e99-4111-9e94-17944c5db765" />

2. Download the appropriate installer for your Operating System (Windows, Mac, Linux).
3. Run the installer and follow the default installation steps.

### Create a Virtual Machine

<img width="1918" height="1013" alt="image" src="https://github.com/user-attachments/assets/2c4b6963-fe52-48fb-b322-8404051bae40" />

1. Open VirtualBox and click **New**.

<img width="1058" height="698" alt="image" src="https://github.com/user-attachments/assets/663cb8c7-4cd0-4224-8db3-82d247f1d800" />

3. Give your VM a name, e.g., *Ubuntu-VLSI*.
4. Type: **Linux**; Version: **Ubuntu (64-bit)**.

<img width="1061" height="702" alt="image" src="https://github.com/user-attachments/assets/8242ab44-7d02-484a-a5a3-8adeccd6ee6a" />

5. Assign RAM: minimum **4096 MB (4 GB)** recommended.

<img width="1062" height="706" alt="image" src="https://github.com/user-attachments/assets/b743352c-9fe1-41e7-8fdb-2f182763a7b6" />

6. Create a virtual hard disk: at least **40 GB** (dynamically allocated).
7. Finish setup.

***

## Installing Ubuntu in VirtualBox

1. Download the Ubuntu ISO (LTS version recommended: [Ubuntu 24.04.3 LTS](https://ubuntu.com/download/desktop).


2. In VirtualBox:
   - Select the VM → **Settings → Storage → Empty CD/DVD drive** → attach the ISO.
3. Start the VM.
4. Ubuntu installer will boot:
   - Choose **Install Ubuntu**.
   - Follow prompts: set language, keyboard, Wi-Fi, username, and password.
   - Install updates and enable third-party software (recommended).
5. Once installed, remove the ISO from the virtual drive and restart.

***

## Installing Required Tools

Now that Ubuntu is running, open the **Terminal** (Ctrl+Alt+T) and proceed.

### Step 1: General Development Tools
These are needed for basic programming and compilation.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential git make gcc g++ python3 python3-pip -y
```

- *build-essential* → includes GCC, G++ and Make.
- Git and Python support scripting and code management.

### Step 2: Application Validation Tools (GCC)
- Already included in `build-essential`.
- Test with:
  ```bash
  gcc --version
  ```
- Compile a test C program:
  ```bash
  echo '#include <stdio.h>\nint main(){printf("Hello VLSI\\n");}' > test.c
  gcc test.c -o test
  ./test
  ```

### Step 3: Specification Modeling (Cross-Compilers)
For running code on simulated processors:

- **RISC-V GCC**:
  ```bash
  sudo apt install gcc-riscv64-unknown-elf -y
  riscv64-unknown-elf-gcc --version
  ```

- **ARM GCC**:
  ```bash
  sudo apt install gcc-arm-none-eabi -y
  arm-none-eabi-gcc --version
  ```

### Step 4: RTL and Hardware Description Languages
Install Verilog and simulators.

- **Icarus Verilog**:
  ```bash
  sudo apt install iverilog gtkwave -y
  ```
  Test with:
  ```bash
  iverilog -v
  ```

- **Optional Open Source Languages**:
  - *Chisel* (Scala-based, requires Java & SBT):
    ```bash
    sudo apt install default-jdk scala sbt -y
    ```
  - *BlueSpec* is commercial, but you can explore its free variants from academic sources.

### Step 5: SOC Partitioning and Functional Verification
Simulation and peripheral IP modeling needs:
- **Verilator** (faster than Icarus):
  ```bash
  sudo apt install verilator -y
  ```

### Step 6: Physical Design (EDA Toolchain)
Open-source tools you can try for back-end workflows:

- **OpenROAD + OpenLane (Floorplanning, Placement, Routing)**  
  Installation (simplified using Docker):
  ```bash
  sudo apt install docker.io -y
  git clone https://github.com/The-OpenROAD-Project/OpenLane.git
  cd OpenLane
  make
  ```

- **Magic VLSI (Layout Viewer/Editor)**:
  ```bash
  sudo apt install magic -y
  ```

- **KLayout (for GDSII viewing)**:
  ```bash
  sudo apt install klayout -y
  ```

### Step 7: Hardware Board Testing
While actual board testing requires silicon, you can emulate using **QEMU**:
```bash
sudo apt install qemu-system -y
```
This lets you boot RISC-V or ARM binaries without a physical board.

***

## Final Environment Summary

Your Ubuntu VM will now have:

- GCC (for initial C program testing).
- Cross-compilers (RISC-V, ARM GCC for specification modeling).
- iverilog, verilator, gtkwave (for RTL simulation).
- Magic, KLayout, OpenLane (for physical design and layout).
- QEMU (board emulation).


***
