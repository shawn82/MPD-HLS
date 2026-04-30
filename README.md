# MPD2HLS 一键安装脚本

MPD2HLS 一键安装脚本用于快速部署 `mpd2hls` 服务，安装完成后会自动创建系统服务，并提供 `mpd2hls` 管理命令，方便后续安装、启动、停止、重启、查看日志、更新和卸载。

---

## 功能说明

- 一键安装 `mpd2hls`
- 自动创建安装目录
- 自动下载程序文件
- 自动配置 `systemd` 服务
- 自动启动服务
- 提供命令行管理面板
- 支持查看日志、重启、停止、启动、更新
- 支持完整卸载，删除服务文件、程序目录和管理命令

---

## 默认信息

| 项目 | 默认值 |
|---|---|
| 默认面板端口 | `9527` |
| 默认账号 | `admin` |
| 默认密码 | `admin123` |
| 安装目录 | `/opt/mpd2hls` |
| 服务文件 | `/etc/systemd/system/mpd2hls.service` |
| 管理命令 | `/usr/local/bin/mpd2hls` |
| 管理面板路径 | `/admin` |

---

## 安装方式

执行安装脚本后，会提示输入面板端口：

```bash
bash install.sh
```

示例：

```text
================================================
         MPD2HLS 一键安装脚本
================================================

请输入面板端口 [默认: 9527]
端口 > 8080

  端口: 8080

确认以上配置，按回车开始安装...

[+] 开始安装 mpd2hls...
[+] 创建安装目录 /opt/mpd2hls
[+] 正在下载程序...
████████████████ 100%
[+] 下载完成
[+] 配置系统服务...
[+] 启动服务...

================================================
              安装成功！
================================================

  访问地址: http://1.2.3.4:8080/admin
  默认账号: admin
  默认密码: admin123
```

安装完成后，即可通过浏览器访问：

```text
http://服务器IP:端口/admin
```

例如：

```text
http://1.2.3.4:8080/admin
```

---

## 管理命令

安装完成后，输入以下命令即可打开管理面板：

```bash
mpd2hls
```

管理面板示例：

```text
================================================
         MPD2HLS 管理面板
================================================

  状态: 运行中
  访问: http://1.2.3.4:9527/admin

  1. 安装
  2. 重启服务
  3. 停止服务
  4. 启动服务
  5. 查看日志
  6. 更新程序
  7. 卸载（删除所有安装的文件）
  0. 退出
```

---

## 管理功能说明

### 1. 安装

重新执行安装流程。

如果检测到已存在程序文件、服务文件或安装目录，脚本会提示用户选择：

- 删除旧文件后重新安装
- 保留配置文件并覆盖安装
- 取消安装

---

### 2. 重启服务

重启 `mpd2hls` 服务。

等同于执行：

```bash
systemctl restart mpd2hls.service
```

---

### 3. 停止服务

停止 `mpd2hls` 服务。

等同于执行：

```bash
systemctl stop mpd2hls.service
```

---

### 4. 启动服务

启动 `mpd2hls` 服务。

等同于执行：

```bash
systemctl start mpd2hls.service
```

---

### 5. 查看日志

查看 `mpd2hls` 服务运行日志。

等同于执行：

```bash
journalctl -u mpd2hls.service -f
```

---

### 6. 更新程序

更新 `mpd2hls` 主程序文件。

更新过程通常会：

1. 停止当前服务
2. 下载新版程序
3. 替换旧程序
4. 重新启动服务

---

### 7. 卸载

卸载会删除所有安装相关文件。

选择 `7` 后，脚本会提示二次确认，必须输入：

```text
yes
```

才会真正执行删除操作。

卸载会删除以下内容：

```text
/etc/systemd/system/mpd2hls.service
/opt/mpd2hls
/usr/local/bin/mpd2hls
```

其中：

| 路径 | 说明 |
|---|---|
| `/etc/systemd/system/mpd2hls.service` | systemd 服务文件 |
| `/opt/mpd2hls` | 程序目录，包含所有配置数据 |
| `/usr/local/bin/mpd2hls` | 管理命令 |

> 注意：卸载会删除 `/opt/mpd2hls` 目录，里面的配置文件、缓存文件和数据都会被删除。执行卸载前请确认已经备份重要数据。

---

## 常用命令

### 查看服务状态

```bash
systemctl status mpd2hls.service --no-pager -l
```

### 启动服务

```bash
systemctl start mpd2hls.service
```

### 停止服务

```bash
systemctl stop mpd2hls.service
```

### 重启服务

```bash
systemctl restart mpd2hls.service
```

### 查看实时日志

```bash
journalctl -u mpd2hls.service -f
```

### 设置开机自启

```bash
systemctl enable mpd2hls.service
```

### 取消开机自启

```bash
systemctl disable mpd2hls.service
```

---

## 访问地址

安装完成后，访问地址格式为：

```text
http://服务器IP:端口/admin
```

默认端口为 `9527`：

```text
http://服务器IP:9527/admin
```

如果安装时输入了自定义端口，例如 `8080`，则访问：

```text
http://服务器IP:8080/admin
```

---

## 防火墙放行端口

如果服务器无法访问面板，请检查端口是否已放行。

例如安装时使用端口 `9527`，需要确保服务器安全组或防火墙已放行：

```text
TCP 9527
```

如果使用的是云服务器，还需要在云服务商后台安全组中放行对应端口。

---

## 目录结构

安装后主要文件如下：

```text
/opt/mpd2hls
├── mpd2hls
└── 其他配置和数据文件
```

服务文件：

```text
/etc/systemd/system/mpd2hls.service
```

管理命令：

```text
/usr/local/bin/mpd2hls
```

---

## 注意事项

1. 安装脚本需要在 Linux 系统中运行。
2. 建议使用 Debian、Ubuntu 或其他支持 `systemd` 的系统。
3. 安装前请确认服务器网络正常，可以下载程序文件。
4. 安装前请确认端口没有被其他程序占用。
5. 卸载会删除 `/opt/mpd2hls` 目录，执行前请备份重要配置。
6. 如果面板打不开，请优先检查服务状态、日志、防火墙和云服务器安全组。

---

## 排查问题

### 面板打不开

请依次检查：

```bash
systemctl status mpd2hls.service --no-pager -l
```

```bash
journalctl -u mpd2hls.service -n 100 --no-pager
```

```bash
ss -lntp | grep 9527
```

如果使用的是自定义端口，请把 `9527` 改成实际端口。

---

### 服务没有运行

可以尝试重启服务：

```bash
systemctl restart mpd2hls.service
```

然后查看状态：

```bash
systemctl status mpd2hls.service --no-pager -l
```

---

### 端口被占用

检查端口占用：

```bash
ss -lntp | grep 9527
```

如果端口已被占用，请重新安装时换一个端口，或者停止占用该端口的程序。

---

## 卸载说明

执行：

```bash
mpd2hls
```

然后选择：

```text
7. 卸载（删除所有安装的文件）
```

输入 `yes` 二次确认后，会删除：

```text
/etc/systemd/system/mpd2hls.service
/opt/mpd2hls
/usr/local/bin/mpd2hls
```

卸载完成后，`mpd2hls` 管理命令也会被删除。

---

## 登录信息

默认登录信息：

```text
账号：admin
密码：admin123
```

安装完成后建议尽快修改默认密码。

---

## 免责声明

本脚本仅用于快速部署和管理 `mpd2hls` 服务。请确保你部署和使用的内容符合当地法律法规以及相关服务条款。
