# UniXNU-sm8250-common

Shared Qualcomm SM8250 (Snapdragon 865) support for UniXNU device ports.

| Path | Contents |
| --- | --- |
| soc.toml | format 2 SoC description: source pin, component selection |
| configs/sm8250.config | kernel configuration shared by SM8250 devices |
| dts/sm8250.dtsi | mainline SoC device tree (v6.12) as the reference |
| patches/xnu/series | XNU patch series applied for this SoC |

Used by [UniXNU-kebab](https://github.com/stevedang67889/UniXNU-kebab) through
the soc source in its eeds.toml.
## Hardware facts measured on kebab (OnePlus 8T)

These are read from the phone's own live device tree and from the firmware log;
they are the values the ADT has to agree with.

| Item | Value |
| --- | --- |
| DRAM banks | `0x80000000`+`0x39900000`, `0xC0000000`+`0xC0000000`, `0x200000000`+`0x200000000` |
| Kernel window used for bring-up | `0xC0000000`, 3 GiB (DarwinBoot allocation) |
| GIC distributor | `0x17A00000`, 64 KiB |
| GIC redistributor | `0x17A60000`, 1 MiB, stride `0x20000` |
| Virtual timer INTID | 27 |
| Timer frequency | 19.2 MHz |
| PSCI | `smc`; eight cores at MPIDR affinities `0x000,0x100,...,0x700` |
| Debug UART | `0xA90000` (QUPv3 SE12, GPIO 34/35), 115200 8N1 |
| UEFI FD load region | `0x9FC00000` + `0x300000` (from `xbl` `uefiplat.cfg`) |
| Framebuffer | `0x9C000000`, 1080x2400, row 4320 bytes, 32 bpp |

The full DRAM map is discontiguous. The format-2 ADT generator accepts one
range, so the bring-up declares a single window and lets DarwinBoot place the
kernel inside it.