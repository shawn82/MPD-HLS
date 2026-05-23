<div align="center">

# MPD2HLS

**MPD/DASH → HLS 转换服务 · 一键安装 · 自动管理**

![Platform](https://img.shields.io/badge/平台-Linux%20x86__64%20%7C%20aarch64%20%7C%20armv7-blue)
![License](https://img.shields.io/badge/许可-MIT-green)
[![Telegram](https://img.shields.io/badge/TG交流群-@GPT__858-26A5E4?logo=telegram)](https://t.me/GPT_858)

</div>


![image.png](https://img.111451444.xyz/files/QWdBREZ3Y0FBbThMR0VROgAzodnW-XKJmhFdhfhC7traxIErDTau3D7kH6g6Ogxw.png)
![image.png](https://img.111451444.xyz/files/QWdBRDV3WUFBaVVfR0VROnhDrm2M3NAY7nK1sIj80G1hyKkveFhna7ng-b7Ur0or.png)
![image.png](https://img.111451444.xyz/files/QWdBRGNBY0FBckNuR1VROpnF2jNRQgiZD67VUUybwI9Sg49TKaxHmPWT4rgdDzd6.png)
![image.png](https://img.111451444.xyz/files/QWdBRGJnY0FBckNuR1VROk9gapnpudyymkSl6vaPOH3HNPemWxKsOYoSOjcgX47T.png)
![image.png](https://img.111451444.xyz/files/QWdBREdBY0FBbThMR0VROnHXIHS2Ma1ArSt67xv8539Fij600jfOLWe8G7od14_z.png)
![image.png](https://img.111451444.xyz/files/QWdBREdnY0FBbThMR0VROrCuANfwaPuxxj5ZCeAuZg2a8kJw2Pa2jIFzPJE-OUIC.png)
![image.png](https://img.111451444.xyz/files/QWdBRDZBWUFBaVVfR0VROpwMIqCgzqAPDoPiVXlQ1wTEE8LWUH31cEU9CdeZSPuF.png)
![image.png](https://img.111451444.xyz/files/QWdBRGJ3Y0FBckNuR1VROo_dV1vLs97uYEM4Omftwo2T8CYNSIbHFiT_opgzB0bF.png)
![image.png](https://img.111451444.xyz/files/QWdBREdRY0FBbThMR0VROqN18wGaNaHGm8HwK_5dSIQuiRsI0Gw-kwZQljJpDFES.png)
![image.png](https://img.111451444.xyz/files/QWdBRDZRWUFBaVVfR0VROmIPgo4J5b_T2q2RQqBXw6F0GuAZU9XxIqh9GJtZ-FQ_.png)


---

## 快速安装

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/judy-gotv/MPD-HLS/main/install.sh)
```

或下载后执行：

```bash
curl -fsSL https://raw.githubusercontent.com/judy-gotv/MPD-HLS/main/install.sh -o install.sh
bash install.sh
```

非交互一键模式：

```bash
# 直接安装 + 启动（自动识别架构）
curl -fsSL https://raw.githubusercontent.com/judy-gotv/MPD-HLS/main/install.sh | bash -s install

# 直接卸载
curl -fsSL https://raw.githubusercontent.com/judy-gotv/MPD-HLS/main/install.sh | bash -s uninstall
```

---

## 默认信息

| 项目 | 值 |
|---|---|
| 面板端口 | `9527` |
| 管理路径 | `/admin` |
| 默认账号 | `admin` |
| 默认密码 | **首次启动随机生成**，自动打印到日志 |
| 安装目录 | `/opt/mpd2hls` |
| 配置文件 | `/opt/mpd2hls/mpd2hls.env` |
| 服务文件 | `/etc/systemd/system/mpd2hls-panel.service` |

> 出于安全考虑，默认密码不再使用固定值，而是首次启动时由程序随机生成并打印到系统日志，登录后请立即在面板中修改。

### 如何查看首次随机密码

安装脚本会在安装完成时自动打印密码。如果你错过了，可以随时用以下命令查看：

```bash
# 方法一：使用脚本快捷命令
bash install.sh password

# 方法二：直接查 journal
journalctl -u mpd2hls-panel | grep -i "temporary password"
```

---

## 管理命令

```bash
# 交互菜单（推荐）
bash install.sh

# 启动 / 停止 / 重启
bash install.sh start
bash install.sh stop
bash install.sh restart

# 查看运行状态
bash install.sh status

# 实时日志
bash install.sh logs

# 查看首次随机密码
bash install.sh password

# 升级到最新版
bash install.sh update

# 卸载
bash install.sh uninstall
```

也可以直接用 systemctl 管理：

```bash
systemctl start   mpd2hls-panel
systemctl stop    mpd2hls-panel
systemctl restart mpd2hls-panel
systemctl status  mpd2hls-panel
systemctl enable  mpd2hls-panel   # 开机自启
systemctl disable mpd2hls-panel
journalctl -u mpd2hls-panel -f    # 实时日志
```

---

## 自定义参数安装

通过环境变量在安装前自定义：

```bash
# 自定义端口
PANEL_PORT=18080 bash install.sh install

# 安装指定版本
GH_RELEASE_TAG=0.2.33 bash install.sh install

# 自定义安装目录
INSTALL_DIR=/data/mpd2hls bash install.sh install

# 自定义管理路径
PANEL_ADMIN_PATH=/manager bash install.sh install
```

| 环境变量 | 默认值 | 说明 |
|---|---|---|
| `INSTALL_DIR` | `/opt/mpd2hls` | 安装目录 |
| `PANEL_PORT` | `9527` | 面板监听端口 |
| `PANEL_ADMIN_PATH` | `/admin` | 管理面板路径 |
| `GH_REPO` | `judy-gotv/MPD-HLS` | GitHub 仓库 |
| `GH_RELEASE_TAG` | `latest` | 版本号 |

---

## 访问地址

安装完成后通过浏览器访问：

```
http://服务器IP:端口/admin
```

例如使用默认端口 `9527`：

```
http://1.2.3.4:9527/admin
```

> ⚠️ 默认配置 (`PANEL_ADDR=127.0.0.1:9527`) 只监听本机，需要通过反向代理（推荐 nginx + HTTPS）或修改 `mpd2hls.env` 中的 `PANEL_ADDR` 来开放外部访问。

---

## 修改密码 / 重置密码

### 方法一：在面板中修改（推荐）

登录后点击右上角「账号设置」即可修改。

### 方法二：手动重置

```bash
# 1. 停止服务
systemctl stop mpd2hls-panel

# 2. 删除认证文件
rm -f /opt/mpd2hls/panel_auth.json

# 3. 编辑配置文件
nano /opt/mpd2hls/mpd2hls.env
# 把 PANEL_ADMIN_PASS=你想要的密码  (留空则随机生成)

# 4. 启动服务
systemctl start mpd2hls-panel

# 5. 查看密码
bash install.sh password
```

---

## 支持的系统架构

| 架构 | 二进制文件 | 适用设备 |
|---|---|---|
| `x86_64` | `mpd2hls` | 标准服务器 / VPS |
| `aarch64` | `mpd2hls-aarch64` | ARM64 服务器 / 树莓派 4 / 5 |
| `armv7l` | `mpd2hls-armv7` | 32位 ARM 设备 / 树莓派 3 |

---

## 目录结构

```
/opt/mpd2hls/
├── mpd2hls              # 主程序
├── mpd2hls.env          # 环境变量配置（编辑后需重启服务）
├── panel_auth.json      # 账号认证文件（密码哈希）
├── channels.json        # 频道配置
├── panel_api_token      # API 令牌
└── audit.log            # 审计日志

/etc/systemd/system/
└── mpd2hls-panel.service  # 系统服务文件
```

---

## 排查问题

**面板无法访问？**

```bash
# 1. 检查服务状态
systemctl status mpd2hls-panel --no-pager -l

# 2. 查看错误日志
journalctl -u mpd2hls-panel -n 100 --no-pager

# 3. 确认端口监听
ss -lntp | grep 9527

# 4. 检查防火墙
# 云服务器还需在安全组中放行对应 TCP 端口
```

**服务无法启动？**

```bash
# 重启后查看详细日志
systemctl restart mpd2hls-panel
journalctl -u mpd2hls-panel -n 50 --no-pager
```

**忘记密码 / 找不到密码？**

```bash
# 查找首次启动生成的随机密码
bash install.sh password

# 或直接从 journal 检索
journalctl -u mpd2hls-panel --since "1 hour ago" | grep -i "temporary password"
```

如果 `panel_auth.json` 已存在且你忘记了密码，请按上面【修改密码 / 重置密码】中的「方法二」操作。

**端口被占用？**

```bash
# 查看端口占用情况
ss -lntp | grep 9527
```

重新安装时通过 `PANEL_PORT=新端口 bash install.sh install` 指定一个未占用的端口。

---

## 注意事项

1. 需要在支持 `systemd` 的 Linux 系统上运行（Debian 8+ / Ubuntu 16.04+ / CentOS 7+ / Alpine 等）
2. 需要 root 权限执行
3. 安装前确保服务器网络正常，可访问 GitHub
4. 安装前确认所选端口未被占用
5. 默认仅监听 `127.0.0.1`，对外暴露请配置反向代理（推荐 nginx + HTTPS）
6. 卸载将永久删除 `/opt/mpd2hls` 目录，请提前备份重要数据
7. 如使用云服务器，需在安全组中放行面板端口（TCP）

---

<div align="center">

作者：**Go-iptv**　·　TG 交流群：[t.me/GPT_858](https://t.me/GPT_858)

</div>
