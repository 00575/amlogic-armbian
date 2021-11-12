# 可以安装在 Amlogic S9xxx 系列盒子中使用的 Armbian 系统

查看英文说明 | [View English description](README.md)

为 Amlogic S9xxx 系列盒子编译 Armbian 系统。支持写入 EMMC 中使用，支持更新内核等功能。支持的 Amlogic S9xxx 系列型号有 ***`s922x, s905x3, s905x2, s912, s905d, s905x, s905w`*** 等，例如 ***`Belink GT-King, Belink GT-King Pro, UGOOS AM6 Plus, X96-Max+, HK1-Box, H96-Max-X3, Phicomm-N1, Octopus-Planet, Fiberhome HG680P, ZTE B860H`*** 等盒子。

最新的 Armbian 固件可以在 [Releases](https://github.com/ophub/amlogic-s9xxx-armbian/releases) 中下载。欢迎 `Fork` 并进行个性化定制。如果对你有用，可以点仓库右上角的 `Star` 表示支持。

## Armbian 固件说明

| 型号  | 盒子 | [可选内核](https://github.com/ophub/kernel/tree/main/pub/stable) | Armbian 固件 |
| ---- | ---- | ---- | ---- |
| s922x | [Belink](https://tokopedia.link/RAgZmOM41db), [Belink-Pro](https://tokopedia.link/sfTHlfS41db), [Ugoos-AM6-Plus](https://tokopedia.link/pHGKXuV41db), [ODROID-N2](https://www.tokopedia.com/search?st=product&q=ODROID-N2) | 全部 | armbian_aml_s922x_buster_*.img |
| s905x3 | [X96-Max+](https://tokopedia.link/uMaH09s41db), [HK1-Box](https://tokopedia.link/xhWeQgTuwfb), [H96-Max-X3](https://tokopedia.link/KuWvwoYuwfb), [Ugoos-X3](https://tokopedia.link/duoIXZpdGgb), [X96-Air](https://tokopedia.link/5WHiETbdGgb), [A95XF3-Air](https://tokopedia.link/ByBL45jdGgb) | 全部 | armbian_aml_s905x3_buster_*.img |
| s905x2 | [X96Max-4G](https://tokopedia.link/HcfLaRzjqeb), [X96Max-2G](https://tokopedia.link/HcfLaRzjqeb) | 全部 | armbian_aml_s905x2_buster_*.img |
| s912 | [H96-Pro-Plus](https://tokopedia.link/jb42fsBdGgb), Octopus-Planet | 全部 | armbian_aml_s912_buster_*.img |
| s905d | Phicomm-N1 | 全部 | armbian_aml_s905d_buster_*.img |
| s905x | [HG680P](https://tokopedia.link/HbrIbqQcGgb), [B860H](https://tokopedia.link/LC4DiTXtEib) | 5.4.* | armbian_aml_s905x_buster_*.img |
| s905w | [X96-Mini](https://tokopedia.link/ro207Hsjqeb), [TX3-Mini](https://www.tokopedia.com/beststereo/tanix-tx3-mini-2gb-16gb-android-7-1-kodi-17-3-amlogic-s905w-4k-tv-box) | 5.4.* | armbian_aml_s905w_buster_*.img |

## 安装及升级 Armbian 的相关说明

选择和你的盒子型号对应的 Armbian 固件，使用 [Rufus](https://rufus.ie/) 或者 [balenaEtcher](https://www.balena.io/etcher/) 等工具将固件写入 USB 里，然后把写好固件的 USB 插入盒子。

- ### 安装 Armbian 到 EMMC

登录 Armbian 系统 (默认用户: root, 默认密码: 1234) → 输入命令：

```yaml
armbian-install
```

- ### 更新 Armbian 内核

查询 [可选内核](https://github.com/ophub/kernel/tree/main/pub/stable) 版本，登录 Armbian 系统 → 输入命令：

```yaml
# 使用 root 用户运行 (sudo -i), 输入命令: armbian-update <内核版本>
armbian-update 5.10.66
```

默认从 [stable](https://github.com/ophub/kernel/tree/main/pub/stable) 内核版本分支下载，如果下载其他 [版本分支](https://github.com/ophub/kernel/tree/main/pub) 的内核，请在第 `2` 个参数中根据分支文件夹名称指定，如 `armbian-update 5.7.2 beta`

默认自动安装主线 u-boot，可以更好的支持 5.10 及以上内核系列的使用。如果选择不安装，请在第 `3` 个输入参数中指定，如 `armbian-update 5.10.66 stable no`

- ### 安装 Docker 服务

登录 Armbian 系统 → 输入命令：

```yaml
armbian-docker
```

- ### 修改 Armbian 配置

登录 Armbian 系统 → 输入命令：

```yaml
armbian-config
```

- ### 为 Armbian 创建 swap

如果你在使用 `docker` 等内存占用较大的应用时，觉得当前盒子的内存不够使用，可以创建 `swap` 虚拟内存分区，将磁盘空间的一定容量虚拟成内存来使用。下面命令输入参数的单位是 `GB`，默认为 `1`。

登录 Armbian 系统 → 输入命令：

```yaml
armbian-swap 1
```

- ### 在 TF/USB 中使用 Armbian

激活 TF/USB 的剩余空间，请登录 Armbian 系统 → 输入命令：

```yaml
armbian-tf
```

<details>
  <summary>或者手动分配剩余空间 </summary>

#### 查看 [操作截图](https://user-images.githubusercontent.com/68696949/137860992-fbd4e2fa-e90c-4bbb-8985-7f5db9f49927.jpg)

```yaml
# 1. 根据空间大小确认 TF/USB 的名称，TF卡为 [ mmcblk ]，USB 为[ sd ]
在命令行中: 输入 [ fdisk -l | grep "sd" ] 查看卡的名称

# 2. 获取剩余空间的起始值，复制并保存，下面使用（例如：5382144）
在命令行中: 输入 [ fdisk -l | grep "sd" | sed -n '$p' | awk '{print $3}' | xargs -i expr {} + 1 ] 得到剩余空间起始值

# 3. 开始分配未使用的空间（例如：sda、mmcblk0 或 mmcblk1）
在命令行中: 输入 [ fdisk /dev/sda ] 开始分配剩余空间
在命令行中: 输入 [ n ] 创建新分区
在命令行中: 输入 [ p ] 指定分区类型为主分区
在命令行中: 将分区号设置为 [ 3 ]
在命令行中: 分区的起始值，输入第二步得到的值 [ 5382144 ]
在命令行中: 分区的结束值，按 [ 回车 ] 使用默认值
在命令行中: 如果提示是否删除签名？[Y]es/[N]o: 输入 [ Y ]
在命令行中: 输入 [ t ] 指定分区类型
在命令行中: 输入分区编号 [ 3 ]
在命令行中: 指定分区类型为 Linux，输入代码 [ 83 ]
在命令行中: 输入 [ w ] 保存结果
在命令行中: 输入 [ reboot ] 重启

# 4. 重新启动后，格式化新分区
在命令行中: 输入 [ mkfs.ext4 -F -L SHARED /dev/sda3 ] 格式新分区

# 5. 为新分区设置挂载目录
在命令行中: 输入 [ mkdir -p /mnt/share ] 创建新分区的挂载目录
在命令行中: 输入 [ mount -t ext4 /dev/sda3 /mnt/share ] 进行挂载

# 6. 添加开机自动挂载
在命令行中: [ vi /etc/fstab ]
# 按 [ i ] 进入编译模式，将下面的代码复制，黏贴到文件的末尾处
/dev/sda3 /mnt/share ext4 defaults 0 0
# 按 [ esc ] 键退出，输入 [ :wq! ] 后按 [ 回车 ] 保存退出，结束设置。
```
</details>

## 打包命令的相关参数说明

- `sudo ./make -d -b s905x3 -k 5.4.150` : 推荐使用. 使用默认配置进行相关内核打包。
- `sudo ./make -d -b s905x3_s905d -k 5.10.70_5.4.150` : 使用默认配置，进行多个内核同时打包。使用 `_` 进行多内核参数连接。
- `sudo ./make -d` : 使用默认配置，对全部型号的机顶盒进行打包。
- `sudo ./make -d -b s905x3 -k 5.4.150 -s 1024` : 使用默认配置，指定一个内核，一个型号进行打包，固件大小设定为1024M。
- `sudo ./make -d -b s905x3 -v beta -k 5.7.2` : 使用默认配置，指定型号，指定版本分支，指定内核进行打包。
- `sudo ./make -d -b s905x3_s905d`  使用默认配置，对多个型号的机顶盒进行全部内核打包, 使用 `_` 进行多型号连接。
- `sudo ./make -d -k 5.10.70_5.4.150` : 使用默认配置，指定多个内核，进行全部型号机顶盒进行打包, 内核包使用 `_` 进行连接。
- `sudo ./make -d -k 5.10.70_5.4.150 -a true` : 使用默认配置，指定多个内核，进行全部型号机顶盒进行打包, 内核包使用 `_` 进行连接。自动升级到同系列最新内核。
- `sudo ./make -d -s 1024 -k 5.4.150` : 使用默认配置，设置固件大小为 1024M, 并指定内核为 5.4.150 ，对全部型号机顶盒进行打包。

| 参数 | 含义 | 说明 |
| ---- | ---- | ---- |
| -d | Defaults | 使用默认配置 |
| -b | Build | 指定机顶盒型号，如 `-b s905x3` . 多个型号使用 `_` 进行连接，如 `-b s905x3_s905d` . 可以指定的型号有: `s905x3`, `s905x2`, `s905x`, `s905w`, `s905d`, `s922x`, `s922x-n2`, `s912`。说明：`s922x-n2` 是 `s922x-odroid-n2` |
| -v | Version | 指定内核 [版本分支](https://github.com/ophub/kernel/tree/main/pub) 名称，如 `-v stable` 。指定的名称须与分支目录名称相同。默认使用 `stable` 分支版本。 |
| -k | Kernel | 指定 [kernel](https://github.com/ophub/kernel/tree/main/pub/stable) 名称，如 `-k 5.4.150` . 多个内核使用 `_` 进行连接，如 `-k 5.10.70_5.4.150` |
| -a | AutoKernel | 设置是否自动采用同系列最新版本内核。当为 `true` 时，将自动在内核库中查找在 `-k` 中指定的内核如 5.4.150 的 5.4 同系列是否有更新的版本，如有 5.4.150 之后的最新版本时，将自动更换为最新版。设置为 `false` 时将编译指定版本内核。默认值：`true` |
| -s | Size | 对固件的大小进行设置，默认大小为 1024M, 固件大小必须大于 256M. 例如： `-s 1024` |

💡提示：当前 ***`s905x`*** 和 ***`s905w`*** 系列的盒子只支持使用 `5.4.*` 内核，不能使用 5.10.* 或更高版本，请在编译时指定替换内核。其他型号的盒子可任选内核版本使用。

- ### 使用 GitHub Action 进行编译

1. 关于 Workflows 文件的配置在 [.yml](.github/workflows) 文件里。可以设置需要编译的盒子的 `soc` 等参数，具体详见 `Make Armbian for amlogic s9xxx` 节点。

2. 全新编译：在 [Action](https://github.com/ophub/amlogic-s9xxx-armbian/actions) 页面里选择 ***`Build Armbian For Amlogic`*** ，点击 ***`Run workflow`*** 按钮即可编译。

3. 再次编译：如果 [Releases](https://github.com/ophub/amlogic-s9xxx-armbian/releases) 中有已经编译好的 `Armbian_.*-trunk_.*.img.gz` 文件，你只是想再次制作其他不同 soc 的盒子，可以跳过 Armbian 源文件的编译，直接进行二次制作。在 [Action](https://github.com/ophub/amlogic-s9xxx-armbian/actions) 页面中选择  ***`Use Releases file to build`*** ，点击 ***`Run workflow`*** 按钮即可二次编译。

- ### 本地化打包

1. 安装必要的软件包（如 Ubuntu 20.04 LTS 用户）

```yaml
sudo apt-get update -y
sudo apt-get full-upgrade -y
sudo apt-get install -y $(curl -fsSL git.io/ubuntu-2004-server)
```

2. 克隆仓库到本地 `git clone --depth 1 https://github.com/ophub/amlogic-s9xxx-armbian.git`
3. 在根目录下创建文件夹 `build/output/images` ，并上传采用 `lepotato` 分支生成的 Armbian 镜像文件 ( 如：`Armbian_21.11.0-trunk_Lepotato_buster_current_5.10.67.img` ) 到 `~/amlogic-s9xxx-armbian/build/output/images` 目录里。
4. 进入 `~/amlogic-s9xxx-armbian` 根目录，然后运行 `sudo ./make s905x3` 命令即可生成指定 soc 的 Armbian 镜像文件。生成的文件保存在 `build/output/images` 目录里。

## 借鉴

编译的 [armbian](https://github.com/armbian/build) 系统直接使用了官方当前的最新源码进行实时编译。为不同的盒子制作专用的 Armbian 系统时采用了 [flippy](https://github.com/unifreq/openwrt_packit) 为 `amlogic s9xxx openwrt` 制作的内核、脚本及 `u-boot` 等资源。程序的开发思路来自 [ebkso](https://www.kflyo.com/howto-compile-armbian-for-n1-box) 等作者的教程。感谢各位的奉献和分享，让我们可以在 Amlogic s9xxx 盒子里使用 Armbian 系统。

## 鸣谢

- [armbian/build](https://github.com/armbian/build)
- [flippy/openwrt](https://github.com/unifreq)
- [ebkso/compile](https://www.kflyo.com/howto-compile-armbian-for-n1-box)

## License

[LICENSE](https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/LICENSE) © OPHUB

