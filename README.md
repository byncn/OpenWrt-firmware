**English** | [中文](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
[![构建OpenWrt-lede](https://github.com/byncn/OpenWrt-firmware/actions/workflows/build-openwrt.yml/badge.svg?branch=main&event=status)](https://github.com/byncn/OpenWrt-firmware/actions/workflows/build-openwrt.yml)
[![Release](https://img.shields.io/github/release/RealKiro/Actions-OpenWrt?color=blue)](https://github.com/byncn/OpenWrt-firmware/releases)

使用GitHub Actions构建OpenWrt的模板

## 使用方法

- 点击 [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) 按钮，创建一个新的资源库。
- 填写仓库名称，然后点击Create repository from template（从模版创建储存库）按钮。
- 然后点击Create new file（创建新文件）按钮，文件名填写为.config，把生成的.config 文件的内容复制粘贴到下面的文本框中。
- 在 Actions 页面选择Build OpenWrt，然后点击Run Workflow按钮，即可开始编译。（如果需要 SSH 连接则把SSH connection to Actions的值改为true。
- 最后经过一两个小时的等待，不出意外你就可以在 Actions 页面看到已经打包好的固件目录压缩包。

## 提示

- 创建一个".config "文件和构建OpenWrt固件可能需要很长时间。因此，在创建库来构建自己的固件之前，你可以搜索一下其他人是否已经构建了它[search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).
- Add some meta info of your built firmware (such as firmware architecture and installed packages) to your repository introduction, this will save others' time.

## 进阶使用
###自定义环境变量与功能

## Credits

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
