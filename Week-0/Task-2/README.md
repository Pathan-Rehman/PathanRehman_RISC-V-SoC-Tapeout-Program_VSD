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

![Alt Txt](https://github.com/Pathan-Rehman/PathanRehman_RISC-V-SoC-Tapeout-Program_VSD/blob/main/Week-0/Task-2/Images/Recording%202025-09-19%20160802.gif)

2. In VirtualBox:
   - Select the VM → **Settings → Storage → Empty CD/DVD drive** → attach the ISO.
3. Start the VM.
4. Ubuntu installer will boot:
   - Choose **Install Ubuntu**.
   - Follow prompts: set language, keyboard, Wi-Fi, username, and password.
   - Install updates and enable third-party software (recommended).
5. Once installed, remove the ISO from the virtual drive and restart.

***

Here are the installation instructions for Yosys, Icarus Verilog (iverilog), and GTKWave.
***

## Installing Required Tools

Now that Ubuntu is running, open the **Terminal** (`Ctrl+Alt+T`) and proceed with the following commands for each tool:

### General Development Tools

Install system essentials (if not already present):

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential git make gcc g++ python3 python3-pip -y
```
- `build-essential` includes GCC, G++, and Make.
- `git` enables version control.
- `python3`, `python3-pip` support scripting.

***

### Yosys (Open SYnthesis Suite) Installation

<img width="867" height="592" alt="image" src="https://github.com/user-attachments/assets/30d1282a-c31e-400f-b027-216728b3490a" />

```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get install build-essential clang bison flex \
  libreadline-dev gawk tcl-dev libffi-dev git \
  graphviz xdot pkg-config python3 libboost-system-dev \
  libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make
sudo make install
```
- This will build and install Yosys from source. If `make` is not installed, run `sudo apt install make` first.

***

### Icarus Verilog (iverilog) and GTKWave Installation

<img width="807" height="694" alt="image" src="https://github.com/user-attachments/assets/a13201de-d67e-49e0-95bd-d0c20304d304" />


<img width="486" height="74" alt="image" src="https://github.com/user-attachments/assets/f69426f1-d292-4cf3-90f5-d1b5c5d0742a" />


```bash
sudo apt-get update
sudo apt-get install iverilog gtkwave
sudo apt install gtkwave   # For GTKWave only
```
- Both iverilog and gtkwave are simulation and waveform viewing tools, respectively.
- Test installation with:
  ```bash
  iverilog -v
  ```

***

## Final Environment Summary

Your Ubuntu VM will now have:
- GCC (for initial C program testing).
- Yosys (for RTL synthesis and analysis).
- Icarus Verilog and GTKWave (for RTL simulation and waveform viewing).

These tools support key steps in the VLSI SOC design flow, from application and specification validation, to RTL simulation and synthesis, all within your virtualized, isolated Linux development environment.

- Magic, KLayout, OpenLane (for physical design and layout).
- QEMU (board emulation).


***
