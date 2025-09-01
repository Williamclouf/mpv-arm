# 🎬 MPV for Apple Silicon Macs

A comprehensive guide to build **mpv** media player from source on Apple Silicon Macs with **Vulkan support**.

[![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-blue?logo=apple)](https://www.apple.com/macos/)
[![MPV](https://img.shields.io/badge/MPV-Latest-red?logo=mpv)](https://mpv.io/)
[![Vulkan](https://img.shields.io/badge/Vulkan-Supported-green?logo=vulkan)](https://www.vulkan.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📋 Prerequisites

Before building mpv, ensure you have the following installed:

- 🛠️ [**Xcode**](https://developer.apple.com/xcode/) - Apple's development tools
- 🍺 [**Homebrew**](https://brew.sh/) - Package manager for macOS
- 🖥️ **macOS 11.0+** - Required for Apple Silicon support
- 💾 **~2GB free space** - For dependencies and build artifacts
- ⏱️ **20-30 minutes** - Estimated build time

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

Download the [**build-mpv_silicon.sh**](https://github.com/hongmd/mpv-arm/blob/main/build-mpv_silicon.sh) script and place it in your mpv directory:

```bash
# Download the build script
curl -O https://raw.githubusercontent.com/hongmd/mpv-arm/main/build-mpv_silicon.sh
chmod +x build-mpv_silicon.sh
```

**What the script does:**
- Sets up meson build system
- Compiles mpv with optimized settings for Apple Silicon
- Creates macOS app bundle
- Handles static linking for standalone app

### Step 5: Install Additional Tools

Install dylibbundler for app bundling:

```bash
brew install dylibbundler
```

### Step 6: Build MPV

Make the script executable and run it:

```bash
# Build with static linking (recommended for distribution)
./build-mpv_silicon.sh --static

# OR build without static linking (smaller file, requires system libraries)
./build-mpv_silicon.sh
```

**Build Options Explained:**
- `--static`: Creates self-contained app with all dependencies bundled
- Without `--static`: Smaller app but requires system libraries

The build process will:
1. Configure meson build system
2. Compile mpv with ARM64 optimizations
3. Run tests to verify the build
4. Create macOS app bundle (if --static is used)

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

## ⚙️ Configuration

### Recommended mpv.conf for Apple Silicon

Create `~/.config/mpv/mpv.conf` for optimal performance:

```ini
# Use Vulkan for hardware acceleration
vo=gpu-next
gpu-api=vulkan

# Apple Silicon optimizations
hwdec=videotoolbox
profile=gpu-hq

# High quality scaling
scale=ewa_lanczos
dscale=mitchell
cscale=ewa_lanczos

# Performance settings
vd-lavc-threads=8
cache=yes
demuxer-max-bytes=150M
```

## 🐛 Troubleshooting

If you encounter issues:

1. **Xcode Command Line Tools**: `xcode-select --install`
2. **Update Homebrew**: `brew update && brew upgrade`
3. **Clean builds**: `rm -rf build/` before rebuilding
4. **Vulkan issues**: Check MoltenVK installation: `brew list molten-vk`
5. **Build errors**: Ensure you're in the mpv source directory
6. **App won't open**: Check code signing: `codesign -v /Applications/mpv.app`

## 📄 License

This repository's documentation and modifications are licensed under the [MIT License](LICENSE).

**Important Note:** 
- The build script may contain code from other sources
- This license applies to documentation, guides, and original contributions
- Please refer to original sources for script attribution
- MPV itself is licensed under GPLv2+

## 🙏 Credits

- **Original build script** by [dbrookman](https://gist.github.com/dbrookman) - [Source Gist](https://gist.github.com/dbrookman/74b8bcfb37a23452f7137b83bca9580f)
- **MPV Project** - The amazing media player we're building
- **MoltenVK** - Vulkan on Metal implementation
- **Homebrew** - Package management for macOS

---

⭐ **Star this repository** if it helped you build mpv successfully!
