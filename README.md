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
