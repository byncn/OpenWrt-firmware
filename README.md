**English** | [中文](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

<h1 align="center">
  <br>
  <b>Actions-OpenWrt</b>
  <br>
</h1>
<p align="center">
    <a href="https://github.com/byncn/OpenWrt-firmware/actions/workflows/build-openwrt.yml">
        <img src="https://github.com/byncn/OpenWrt-firmware/actions/workflows/build-openwrt.yml/badge.svg?branch=main"
            alt="">
    </a>
    <a href="https://github.com/byncn/OpenWrt-firmware/releases">
        <img src="https://img.shields.io/github/release/byncn/OpenWrt-firmware?color=blue"
            alt="">
    </a>
</p>


##### 使用GitHub Actions构建OpenWrt的模板

## 使用方法

- 点击 [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) 按钮，创建一个新的资源库。
- 填写仓库名称，然后点击Create repository from template（从模版创建储存库）按钮。
- 然后点击Create new file（创建新文件）按钮，文件名填写为.config，把生成的.config 文件的内容复制粘贴到下面的文本框中。
- 在 Actions 页面选择Build OpenWrt，然后点击Run Workflow按钮，即可开始编译。（如果需要 SSH 连接则把SSH connection to Actions的值改为true。
- 最后经过一两个小时的等待，不出意外你就可以在 Actions 页面看到已经打包好的固件目录压缩包。

## 提示

- 创建一个".config "文件和构建OpenWrt固件可能需要很长时间。因此，在创建库来构建自己的固件之前，你可以搜索一下其他人是否已经构建了它[search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).

  

## 进阶使用

#### 自定义环境变量与功能

work­flow 文件（`.github/workflows/build-openwrt.yml`）下有一些环境变量，可按照自己的需求对这些变量进行定义。

| 环境变量             | 功能                                                        |
| :------------------- | :---------------------------------------------------------- |
| `REPO_URL`           | 源码仓库地址                                                |
| `REPO_BRANCH`        | 源码分支                                                    |
| `FEEDS_CONF`         | 自定义`feeds.conf.default`文件名                            |
| `CONFIG_FILE`        | 自定义`.config`文件名                                       |
| `DIY_P1_SH`          | 自定义`diy-part1.sh`文件名                                  |
| `DIY_P2_SH`          | 自定义`diy-part2.sh`文件名                                  |
| `UPLOAD_BIN_DIR`     | 上传 bin 目录。即包含所有 ipk 文件和固件的目录。默认`false` |
| `UPLOAD_FIRMWARE`    | 上传固件目录。默认`true`                                    |
| `UPLOAD_COWTRANSFER` | 上传固件到奶牛快传。默认`false`                             |
| `UPLOAD_WERANSFER`   | 上传固件到 WeTransfer 。默认`false`                         |
| `UPLOAD_RELEASE`     | 上传固件到 releases 。默认`false`                           |
| PUSHPLUS_TOKEN       | 开启PUSHPLUS通知。默认false                                 |
| `TZ`                 | 时区设置                                                    |

#### DIY 脚本

仓库根目录目前有两个 DIY 脚本：`diy-part1.sh` 和 `diy-part2.sh`，它们分别在更新与安装 feeds 的前后执行，可以把对源码修改的指令写到脚本中，比如修改默认 IP、主机名、主题、添加 / 删除软件包等操作。

- diy-part1.sh添加自定义源

```
sed -i '$a src-git smpackage https://github.com/kenzok78/small-package' feeds.conf.default
```

- diy-part2.sh修改默认 IP、主机名、密码

```
# 设置默认IP为10.0.0.1
sed -i 's/192.168.1.1/10.0.0.1/g' package/base-files/files/bin/config_generate

# 设置密码为空（安装固件时无需密码登陆，然后自己修改想要的密码）
sed -i 's@.*CYXluq4wUazHjmCDBCqXF*@#&@g' package/lean/default-settings/files/zzz-default-settings

# 修改主机名字，把OpenWrt修改你喜欢的就行（不能使用中文）
sed -i '/uci commit system/i\uci set system.@system[0].hostname='OpenWrt'' package/lean/default-settings/files/zzz-default-settings
```

#### 自定义源码

默认引用的是 Lean 的源码，如果你有编译其它源码的需求可以进行替换。

- 编辑 work­flow 文件（`.github/workflows/build-openwrt.yml`），修改下面的相关环境变量字段。

```
REPO_URL: https://github.com/coolsnowwolf/lede
REPO_BRANCH: master
```

- 修改为 Open­Wrt 官方源码 19.07 分支

```
REPO_URL: https://github.com/openwrt/openwrt
REPO_BRANCH: openwrt-19.07
```

#### PUSHPLUS通知

自己仓库的`Settings`选项卡，点击`Secrets`。添加名为`PUSHPLUS_TOKEN`的加密环境变量，为你的PUSHPLUS token。

编辑 work­flow 文件（`.github/workflows/build-openwrt.yml`），添加

```
- name: 开始编译通知-PUSHPLUS
      if: env.PUSHPLUS_TOKEN == 'true'
      continue-on-error: true
      run: |
        curl -k --data token="${{ secrets.PUSH_PLUS_TOKEN }}" --data title="OpenWrt-firmware开始编译Redmi-AC2100" --data "content=🎉 主人：您正在使用OpenWrt-firmware仓库编译固件中,请耐心等待...... 😋💐" --data channel="cp" --data webhook="cp" "http://www.pushplus.plus/send"

```

#### 自定义 feeds 配置文件

把 `feeds.conf.default` 文件放入仓库根目录即可，它会覆盖 Open­Wrt 源码目录下的相关文件。



## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
