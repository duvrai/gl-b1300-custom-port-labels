# GL.iNet GL-B1300 Custom Port Labels

**OpenWrt version:** Created and tested for **v25.12.2** (and later 25.x releases).  
Should work on any recent OpenWrt 25.x build (and likely future versions as long as the device tree structure stays similar).

## What this does

This patch renames the three physical Ethernet ports on the GL-B1300 to much more descriptive names:

| Physical Port (left to right) | Old name | New name          | Default role     |
|-------------------------------|----------|-------------------|------------------|
| Left                          | lan2     | **gigabit1**      | **WAN**          |
| Middle                        | lan1     | **gigabit2**      | LAN              |
| Right (PoE capable)           | wan      | **gigabit3-poe**  | LAN + PoE input  |

### Benefits
- Much clearer labels in LUCI **Status → Overview → Port status**
- `gigabit1` is set as the default WAN port on first boot
- Perfect for PoE use-cases (use the rightmost port as a powered LAN port)

## How to use

### 1. Clone OpenWrt
```bash
git clone https://git.openwrt.org/openwrt/openwrt.git
cd openwrt
git checkout v25.12.2
```

### 2. Apply the patch
```bash
curl -L https://github.com/duvrai/gl-b1300-custom-port-labels/raw/main/patches/01-custom-port-labels.patch -o 01-custom-port-labels.patch
git apply 01-custom-port-labels.patch
```

### 3. Build
```bash
FORCE_UNSAFE_CONFIGURE=1 make menuconfig   # select GL.iNet GL-B1300
FORCE_UNSAFE_CONFIGURE=1 make -j$(nproc)
```

The firmware will be at:  
`bin/targets/ipq40xx/generic/openwrt-ipq40xx-glinet_gl-b1300-squashfs-sysupgrade.bin`

### 4. Flash
- Flash via LUCI or `sysupgrade`
- **Do not keep settings** (or run `firstboot` after flashing)

After first boot you will immediately see the new port names in LUCI.

## Credits
Created by Thomas (duvrai) with help from Grok.

---

**Repository:** https://github.com/duvrai/gl-b1300-custom-port-labels
