# LinuxCore-v2 BSP (NUC980)

This project provides a clean and reproducible Buildroot-based Linux BSP environment for the NUC980 platform.

The goal of this repository is to:

* Maintain a portable build system
* Keep all project-specific configurations under version control
* Enable fast setup on new machines

---

## 📦 Project Structure

```
LinuxCore-v2-BSP/
├── buildroot/                  # Vendor Buildroot (submodule)
├── br2-external/               # Project-specific configuration (MAIN)
│   ├── configs/
│   │   └── linuxcore_v2_nuc980_defconfig
│   ├── board/linuxcore/nuc980/
│   │   ├── linux.config
│   │   ├── uboot.config
│   │   ├── rootfs-overlay/
│   │   ├── post-build.sh
│   │   └── post-image.sh
│   ├── Config.in
│   ├── external.desc
│   └── external.mk
├── output/                     # Build output (ignored)
├── dl/                         # Download cache (ignored)
├── ccache/                     # Compiler cache (ignored)
└── README.md
```

---

## 🚀 Setup (WSL / Ubuntu)

### 1. Install dependencies

```
sudo apt update
sudo apt install -y \
  build-essential git wget curl unzip rsync bc bison flex \
  libssl-dev libncurses-dev python3 cpio file xz-utils
```

---

### 2. Clone repository

```
git clone https://github.com/turgayhopal/LinuxCore-v2-BSP.git
cd LinuxCore-v2-BSP
git submodule update --init --recursive
```

---

## ⚙️ Build Instructions

### Load project configuration

```
make -C buildroot O=../output BR2_EXTERNAL=../br2-external linuxcore_v2_nuc980_defconfig
```

### Build system

```
make -C buildroot O=../output BR2_EXTERNAL=../br2-external
```

---

## 📁 Output

Build artifacts will be located in:

```
output/images/
```

Typical outputs include:

* Kernel image
* Root filesystem
* Bootable images (if configured)

---

## 🔧 Configuration Workflow

### Modify Buildroot config

```
make -C buildroot O=../output menuconfig
```

### Modify Linux kernel config

```
make -C buildroot O=../output linux-menuconfig
```

### Save Buildroot config

```
make -C buildroot O=../output savedefconfig \
BR2_DEFCONFIG=../br2-external/configs/linuxcore_v2_nuc980_defconfig
```

### Save Linux kernel config

```
make -C buildroot O=../output linux-update-defconfig
```

---

## 🧠 Important Notes

* Do NOT commit:

  * `output/`
  * `dl/`
  * `ccache/`

* Only commit:

  * `br2-external/`

* This project is **config-driven**
  Everything important is stored in configuration files.

---

## 🔄 Clean Build

```
rm -rf output
make -C buildroot O=../output BR2_EXTERNAL=../br2-external linuxcore_v2_nuc980_defconfig
make -C buildroot O=../output BR2_EXTERNAL=../br2-external
```

---

## 🎯 Goal

This repository ensures:

* Reproducible builds
* Portable BSP setup
* Easy onboarding on new machines

---

## 📌 Future Improvements

* NUC980 device tree integration
* Custom drivers
* RootFS service automation
* Production-ready image generation

---

## 👨‍💻 Author

Turgay Hopal
