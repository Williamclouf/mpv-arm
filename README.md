# 🎬 MPV for Apple Silicon Macs

A comprehensive guide to build **mpv** media player from source on Apple Silicon Macs with **Vulkan support**.

[![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-blue?logo=apple)](https://www.apple.com/macos/)
[![MPV](https://img.shields.io/badge/MPV-Latest-red?logo=mpv)](https://mpv.io/)
[![Vulkan](https://img.shields.io/badge/Vulkan-Supported-green?logo=vulkan)](https://www.vulkan.org/)

## 📋 Prerequisites

Before building mpv, ensure you have the following installed:

- 🛠️ [**Xcode**](https://developer.apple.com/xcode/) - Apple's development tools
- 🍺 [**Homebrew**](https://brew.sh/) - Package manager for macOS

## 🚀 Installation Guide

### Step 1: Clone MPV Source Code

Clone the official mpv repository:

```bash
git clone https://github.com/mpv-player/mpv.git
cd mpv
```

To update your local clone to the latest version:

```bash
git reset --hard
git clean --force -d -x
git pull origin master
```

### Step 2: Install Vulkan Support

Install MoltenVK for Vulkan API support on Metal:

```bash
brew install molten-vk
```

### Step 3: Install Dependencies

Install mpv dependencies and libplacebo:

```bash
brew install --build-from-source --only-dependencies mpv && brew install libplacebo
```

### Step 4: Download Build Script

Download the [**build-mpv_silicon.sh**](https://github.com/hongmd/mpv-arm/blob/main/build-mpv_silicon.sh) script and place it in your mpv directory.

### Step 5: Install Additional Tools

Install dylibbundler for app bundling:

```bash
brew install dylibbundler
```

### Step 6: Build MPV

Make the script executable and run it:

```bash
chmod +x build-mpv_silicon.sh

# Build with static linking (recommended)
./build-mpv_silicon.sh --static

# Alternative: Build with bundle option
./build-mpv_silicon.sh --bundle
```

### Step 7: Install MPV.app

Copy the built application to your Applications folder:

```bash
cp -r build/mpv.app /Applications/
```

## 🔧 Optional Enhancements

### Install Media Tools

For enhanced streaming and downloading capabilities:

```bash
# Install streamlink and yt-dlp
brew install streamlink yt-dlp

# Create symlinks for compatibility (if needed)
sudo ln -sf /opt/homebrew/bin/streamlink /usr/local/bin/streamlink
sudo ln -sf /opt/homebrew/bin/yt-dlp /usr/local/bin/yt-dlp
```

## 📁 Build Artifacts

After successful build, you'll find:

- `build/mpv` - Command-line binary
- `build/mpv.app` - macOS application bundle

## ⚡ Features

- ✅ **Apple Silicon optimized** - Native ARM64 performance
- ✅ **Vulkan support** - Hardware-accelerated rendering via MoltenVK
- ✅ **Static linking** - Self-contained application bundle
- ✅ **Latest codecs** - Support for modern video formats

## 🐛 Troubleshooting

If you encounter issues:

1. Ensure Xcode Command Line Tools are installed: `xcode-select --install`
2. Update Homebrew: `brew update && brew upgrade`
3. Clean previous builds: `rm -rf build/` before rebuilding

## 📄 License

This build script is provided as-is. MPV itself is licensed under GPLv2+.

---

⭐ **Star this repository** if it helped you build mpv successfully!
