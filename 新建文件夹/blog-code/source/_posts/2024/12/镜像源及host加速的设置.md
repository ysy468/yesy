---
title: 镜像源及 Host 加速的设置
tags: [conda, github, host, pip]
date: 2024-12-14 20:35:00
updated: 2024-12-14 23:01:00
author: xulong
---

## 镜像源及 Host 加速的设置

### 配置 pip 镜像源

#### 编辑 pip 配置文件

打开或新建 `~/.pip/pip.conf` 文件，加入以下内容：

```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
install.trusted-host = https://pypi.tuna.tsinghua.edu.cn
```

你还可以选择其他镜像源，例如阿里云的 PyPI 镜像：
- 镜像地址：`http://mirrors.aliyun.com/pypi/simple/`
- 配置示例：

```ini
[global]
index-url = https://mirrors.aliyun.com/pypi/simple/
install.trusted-host = https://mirrors.aliyun.com
```

#### 验证镜像源配置

运行以下命令查看当前镜像源地址：

```bash
pip3 config list
```

---

### 配置 Conda 镜像源

#### 使用命令行管理通道

1. **添加镜像源通道**  
   运行以下命令将镜像源添加为 Conda 的通道：

   ```bash
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
   conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
   conda config --add channels https://mirrors.sustech.edu.cn/anaconda/pkgs/main
   conda config --add channels https://mirrors.sustech.edu.cn/anaconda/pkgs/free
   ```

2. **移除镜像源通道**  
   如果需要移除某个通道，可以运行以下命令：

   ```bash
   conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
   ```

3. **查看当前通道配置**  
   运行以下命令查看已配置的通道列表：

   ```bash
   conda config --show channels
   ```

#### 手动修改 Conda 配置文件

编辑 `~/.condarc` 文件，加入以下内容：

```yaml
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.sustech.edu.cn/anaconda/pkgs/main
  - https://mirrors.sustech.edu.cn/anaconda/pkgs/free
show_channel_urls: true
```

#### 更新 Conda 环境

运行以下命令清理缓存并更新 Conda 环境：

```bash
conda clean -i  # 清理索引缓存
conda update -n base conda
```

---

### 配置 GitHub Host 加速

GitHub 的访问可能会因为网络限制变慢，你可以通过手动更新 Host 文件来加速。

#### 编辑 Host 文件

执行以下命令以编辑系统的 Host 文件：

```bash
sudo edit /etc/hosts
```

#### 添加 GitHub 加速 IP

在 Host 文件中添加以下内容：

```bash
# GitHub IP Hosts Start
# 更新时间: 2024-12-09 11:00:01 UTC+08:00
# 数据来源: https://github.com/ittuann/GitHub-IP-hosts

140.82.113.25   alive.github.com
140.82.113.26   alive.github.com
140.82.113.6    api.github.com
140.82.114.6    api.github.com
185.199.108.153 assets-cdn.github.com
185.199.109.153 assets-cdn.github.com
185.199.110.153 assets-cdn.github.com
185.199.111.153 assets-cdn.github.com
140.82.112.4    github.com
151.101.1.194   github.global.ssl.fastly.net
185.199.108.153 github.io
185.199.109.153 github.io
185.199.110.153 github.io
185.199.111.153 github.io
# 更多 IP 地址请参考项目仓库：https://github.com/ittuann/GitHub-IP-hosts

# GitHub IP Hosts End
```

#### 保存并更新 Host

保存文件后，执行以下命令使更改生效：

```bash
sudo systemctl restart network
```

---

### 注意事项

1. **镜像源的选择：** 根据需求选择合适的镜像源，国内用户推荐使用清华大学或阿里云的镜像源。
2. **Host 配置的更新：** GitHub 的 IP 地址可能会随时间发生变化，建议定期更新 Host 文件内容。可以通过 [ittuann 的项目仓库](https://github.com/ittuann/GitHub-IP-hosts) 获取最新的 Host 文件。
3. **使用工具自动化更新：** 考虑使用脚本或工具自动化更新 Host 文件，避免手动维护的繁琐。

---

希望这份文档能够帮助你快速配置镜像源及加速工具，提高网络访问效率！