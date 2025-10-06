# OpenWrt UU加速器服务脚本

## 安装与使用

> [!NOTE]
>
> OpenWrt 系统需要安装以下软件包：
>
> *   `curl`: 用于发起 API 请求。
> *   `jq`: 用于解析 API 返回的 JSON 数据。
> *   `wget`: 用于下载插件文件。
> *   `tar`: 用于解压插件压缩包。
> *   `ca-bundle`: HTTPS 根证书。
>
> 可以通过以下命令安装它们：
>
> ```sh
> opkg update && opkg install curl jq wget tar ca-bundle
> ```

### 1. 安装脚本

**方法一：从 GitHub 直接下载**

通过 SSH 登录到 OpenWrt，然后执行以下命令：

```sh
wget -O /etc/init.d/uu https://raw.githubusercontent.com/PKC278/openwrt-uuplugin/main/uu.init
```

**方法二：手动上传**

将 `uu.init` 脚本文件复制到 OpenWrt 的 `/etc/init.d/uu` 路径。例如，在电脑上使用 `scp` 命令：
```sh
scp uu.init root@<OpenWrt IP>:/etc/init.d/uu
```

### 2. 授予执行权限

通过 SSH 登录到 OpenWrt，并为脚本设置执行权限。
```sh
chmod +x /etc/init.d/uu
```

### 3. 启用并启动服务
```sh
# 设置开机自启 (可选)
service uu enable

# 启动服务 (初次启动，脚本会从官方API接口下载最新版本uu加速器可执行文件)
service uu start
```
然后通过手机APP **UU主机加速** 绑定账户

> [!WARNING]
>
> 请不要在 OpenWrt 防火墙设置中启用 **硬件流量卸载** ，否则可能会导致加速器无法正常工作。

## 服务命令

-   **启动**: `service uu start`
-   **停止**: `service uu stop`
-   **重启**: `service uu restart`
-   **安装/更新**: `service uu install`
-   **卸载**: `service uu uninstall` (完全删除UU加速器，执行后如重新启动UU加速器需重新绑定)
-   **重装**: `service uu reinstall` (先执行卸载，然后重新安装)
-   **更新脚本**: `service uu update_script` (更新服务脚本本身到最新版本)
