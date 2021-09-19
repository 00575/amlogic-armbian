# Armbian for Amlogic S9xxx STB

Compile the Armbian for Amlogic S9xxx STB. including install to EMMC and update related functions. Support Amlogic S9xxx STB are ***`s905x3, s905x2, s905x, s905w, s905d, s922x, s912`***, etc. such as ***`Phicomm-N1, Octopus-Planet, X96-Max+, HK1-Box, H96-Max-X3, Belink GT-King, Belink GT-King Pro, UGOOS AM6 Plus, Fiberhome HG680P, ZTE B860H`***, etc.

The latest version of the Armbian firmware can be downloaded in [Releases](https://github.com/ophub/amlogic-s9xxx-armbian/releases).

## Armbian Firmware instructions

| Model  | STB | Armbian Firmware |
| ---- | ---- | ---- |
| s905x3 | [X96-Max+](https://tokopedia.link/uMaH09s41db), [HK1-Box](https://tokopedia.link/xhWeQgTuwfb), [H96-Max-X3](https://tokopedia.link/KuWvwoYuwfb), [Ugoos-X3](https://tokopedia.link/duoIXZpdGgb), [X96-Air](https://tokopedia.link/5WHiETbdGgb), [A95XF3-Air](https://tokopedia.link/ByBL45jdGgb) | armbian_aml_s905x3_buster_k*.img |
| s905x2 | [X96Max-4G](https://tokopedia.link/HcfLaRzjqeb), [X96Max-2G](https://tokopedia.link/HcfLaRzjqeb) | armbian_aml_s905x2_buster_k*.img |
| s905x | [HG680P](https://tokopedia.link/HbrIbqQcGgb), [B860H](https://tokopedia.link/LC4DiTXtEib) | armbian_aml_s905x_buster_k*.img |
| s905w | [X96-Mini](https://tokopedia.link/ro207Hsjqeb), [TX3-Mini](https://www.tokopedia.com/beststereo/tanix-tx3-mini-2gb-16gb-android-7-1-kodi-17-3-amlogic-s905w-4k-tv-box) | armbian_aml_s905w_buster_k*.img |
| s922x | [Belink](https://tokopedia.link/RAgZmOM41db), [Belink-Pro](https://tokopedia.link/sfTHlfS41db), [Ugoos-AM6-Plus](https://tokopedia.link/pHGKXuV41db) | armbian_aml_s922x_buster_k*.img |
| s912 | [H96-Pro-Plus](https://tokopedia.link/jb42fsBdGgb), Octopus-Planet | armbian_aml_s912_buster_k*.img |
| s905d | Phicomm-N1 | armbian_aml_s905d_buster_k*.img |

## Install to EMMC and update instructions

Choose the corresponding firmware according to your STB. Then write the IMG file to the USB hard disk through software such as [Rufus](https://rufus.ie/) or [balenaEtcher](https://www.balena.io/etcher/). Insert the USB hard disk into the STB. Common for all `Amlogic S9xxx STB`.

- ### Install Armbian

Login in to armbian (default user: root, default password: 1234) → input command:

```yaml
armbian-install
```

- ### Update Armbian

Login in to armbian → input command:

```yaml
armbian-update
```
## Armbian firmware compilation method

Different amlogic armbian firmware, use the corresponding soc code to generate. Please choose according to your box soc model. `A single soc` can be directly input `sudo ./make s905d`. When `multiple soc` is compiled at the same time, please use `_` to connect multiple soc, such as `sudo ./make s905d_s905x3_s922x`

```yaml
sudo ./make s905x3_s905x2_s905x_s905w_s905d_s922x_s912
```

## Kernel

- The kernels of `amlogic s9xxx armbian` and `amlogic s9xxx openwrt` are common, you can directly use the [kernel](https://github.com/ophub/flippy-kernel) compiled by flippy to to `update armbian`.

- In the same way, you can also extract the kernel for openwrt from the armbian, The extracted kernel storage path in the `build/output/images` directory, and the file name is `amlogic-s9xxx-openwrt-kernel-*.tar.gz`. The kernel can be used in the [amlogic-s9xxx-openwrt](https://github.com/ophub/amlogic-s9xxx-openwrt/tree/main/amlogic-s9xxx/amlogic-kernel).

## Acknowledgments

The [armbian](https://github.com/armbian/build) directly calls the official source code for compilation, The `u-boot` uses related resources developed by [flippy](https://github.com/unifreq/openwrt_packit) for `amlogic s9xxx openwrt`. The compilation ideas refer to the tutorial of [ebkso](https://www.kflyo.com/howto-compile-armbian-for-n1-box), thanks.

## License

[LICENSE](https://github.com/ophub/build-armbian/blob/main/LICENSE) © OPHUB

