# Linux 教程：开发者必备技能指南

Linux 是现代开发者的必备工具，广泛用于服务器、云计算、容器化（如 Docker）、DevOps 和 AI 等领域。以下是面向开发者的 **Linux 快速上手教程**，涵盖核心命令、文件管理、Shell 编程和实战技巧。

---

## 目录

1. [Linux 简介与发行版](#linux-简介与发行版)  
2. [基础命令速查表](#基础命令速查表)  
3. [文件与目录操作](#文件与目录操作)  
4. [权限管理](#权限管理)  
5. [进程与系统监控](#进程与系统监控)  
6. [软件包管理](#软件包管理)  
7. [Shell 脚本入门](#shell-脚本入门)  
8. [网络与远程连接](#网络与远程连接)  
9. [开发环境配置](#开发环境配置)  
10. [实战案例](#实战案例)  
11. [注意事项](#注意事项)  

---

## Linux 简介与发行版

### 常见发行版对比

| 发行版       | 适用场景               | 包管理器   | 特点                           |
|--------------|------------------------|------------|--------------------------------|
| Ubuntu       | 开发、桌面、云环境     | `apt`      | 社区活跃，文档丰富             |
| CentOS       | 服务器、企业级应用     | `yum/dnf`  | 稳定性强，兼容 RHEL            |
| Arch Linux   | 高级用户、定制化       | `pacman`   | 滚动更新，轻量级               |
| Fedora       | 开发者实验、新技术     | `dnf`      | 创新前沿，Red Hat 支持         |

---

## 基础命令速查表

```bash
# 系统信息
uname -a                # 查看内核/系统信息
top                     # 实时监控进程
df -h                   # 查看磁盘空间
free -h                 # 查看内存使用

# 文件操作
ls -la                  # 列出目录内容（含隐藏文件）
cd /path/to/dir         # 切换目录
mkdir -p dir1/dir2      # 创建多级目录
cp file1 file2          # 复制文件
mv file1 file2          # 移动/重命名
rm -rf dir              # 删除目录及内容

# 文本处理
cat file.txt            # 查看文件内容
grep "pattern" file     # 搜索文本
head -n 10 file         # 查看前 10 行
tail -f file            # 实时查看日志
sed 's/old/new/g' file  # 替换文本
awk '{print $1}' file   # 提取列

# 权限管理
chmod 755 file          # 修改权限
chown user:group file   # 修改所有者

# 网络
ping google.com         # 测试网络
ifconfig/ip a           # 查看 IP 地址
ssh user@host           # 远程登录
scp file user@host:/path # 传输文件
```

---

## 文件与目录操作

### 1. 文件查找

```bash
# 查找文件
find /path/to/search -name "*.log" -mtime -7  # 7 天内修改的日志文件

# 查找并删除
find . -type f -name "*.tmp" -exec rm {} \;

# 快速定位
locate filename       # 需先执行 updatedb
```

### 2. 文件压缩与解压

```bash
# 压缩
tar -czvf archive.tar.gz dir/    # gzip 压缩
zip -r archive.zip dir/          # zip 压缩

# 解压
tar -xzvf archive.tar.gz         # 解压 gzip
unzip archive.zip                # 解压 zip
```

---

## 权限管理

### 1. 权限表示

```bash
-rw-r--r-- 1 user group 1234 Jan 1 00:00 file.txt
# 第一组：rw- (所有者可读写)
# 第二组：r-- (组用户只读)
# 第三组：r-- (其他用户只读)
```

### 2. 修改权限

```bash
chmod u+x script.sh      # 所有者添加执行权限
chmod 755 script.sh      # rwxr-xr-x
```

### 3. 特殊权限

```bash
chmod +s file            # SUID (运行时以文件所有者身份执行)
chmod +t dir             # Sticky Bit (防止非所有者删除文件)
```

---

## 进程与系统监控

### 1. 进程管理

```bash
ps aux                  # 查看所有进程
top                     # 实时监控
htop                    # 可视化进程监控（需安装）
kill -9 PID             # 强制终止进程
nohup command &         # 后台运行并忽略挂断信号
```

### 2. 系统资源监控

```bash
vmstat 1                # 每秒报告内存/CPU 使用
iostat -x 1             # 磁盘 I/O 监控
sar -u 1 5              # CPU 使用率统计（需 sysstat）
```

---

## 软件包管理

### 1. Debian/Ubuntu (apt)

```bash
sudo apt update          # 更新源
sudo apt install package # 安装
sudo apt remove package  # 卸载
sudo apt upgrade         # 升级
```

### 2. Red Hat/CentOS (yum/dnf)

```bash
sudo dnf install package
sudo dnf update
sudo dnf remove package
```

### 3. Arch Linux (pacman)

```bash
sudo pacman -Sy package   # 安装
sudo pacman -Syu          # 升级系统
sudo pacman -R package    # 卸载
```

---

## Shell 脚本入门

### 1. 基本结构

```bash
#!/bin/bash
# 计算两个数之和
num1=10
num2=20
sum=$((num1 + num2))
echo "Sum: $sum"
```

### 2. 条件判断

```bash
if [ -f "file.txt" ]; then
    echo "File exists"
elif [ -d "dir" ]; then
    echo "Directory exists"
else
    echo "Does not exist"
fi
```

### 3. 循环

```bash
# for 循环
for i in {1..5}; do
    echo "Iteration $i"
done

# while 循环
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

### 4. 函数

```bash
function greet() {
    echo "Hello, $1!"
}
greet "Alice"
```

---

## 网络与远程连接

### 1. SSH 密钥管理

```bash
ssh-keygen -t rsa -b 4096  # 生成密钥
ssh-copy-id user@host      # 上传公钥
```

### 2. 端口转发

```bash
# 本地转发（将本地 8080 映射到远程 80）
ssh -L 8080:localhost:80 user@remote_host

# 动态转发（创建 SOCKS 代理）
ssh -D 1080 user@remote_host
```

### 3. 网络调试

```bash
curl -I http://example.com  # 查看 HTTP 头
tcpdump -i eth0 port 80     # 抓包分析
nmap -p 1-100 192.168.1.1   # 端口扫描
```

---

## 开发环境配置

### 1. 环境变量

```bash
export PATH=$PATH:/new/path     # 临时添加路径
echo $HOME                      # 查看环境变量
```

### 2. 多版本管理

```bash
# 使用 pyenv 管理 Python 版本
curl https://pyenv.run | bash
pyenv install 3.9.12
pyenv global 3.9.12

# 使用 nvm 管理 Node.js
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install 18
```

---

## 实战案例

### 1. 自动化日志清理脚本

```bash
#!/bin/bash
LOG_DIR="/var/log/app"
MAX_AGE=7

find $LOG_DIR -type f -name "*.log" -mtime +$MAX_AGE -exec rm {} \;
echo "Logs older than $MAX_AGE days deleted."
```

### 2. 监控网站可用性

```bash
#!/bin/bash
URL="http://example.com"
STATUS=$(curl -s -o /dev/null -w "%{http_code}" $URL)

if [ $STATUS -ne 200 ]; then
    echo "Website down! Status: $STATUS" | mail -s "Site Down" admin@example.com
fi
```

---

## 注意事项

1. **权限安全**：
   - 避免随意使用 `sudo`，最小化权限。
   - 修改系统文件前备份：`sudo cp /etc/file /etc/file.bak`

2. **路径问题**：
   - 绝对路径（`/home/user/file`）与相对路径（`./file`）。
   - 使用 `~` 表示当前用户目录。

3. **文本编码**：
   - 使用 `file file.txt` 检查文件编码。
   - 转换编码：`iconv -f UTF-8 -t ISO-8859-1 input.txt > output.txt`

4. **历史命令**：
   - `history` 查看命令历史。
   - `!123` 执行第 123 条历史命令。

5. **调试技巧**：
   - 使用 `strace` 跟踪系统调用：`strace -f -o debug.log ./script.sh`
   - 使用 `ltrace` 跟踪库函数调用。

---

## 总结

Linux 是开发者的核心工具，掌握以下技能可显著提升效率：

- **命令行操作**：高效完成文件管理、文本处理、进程监控。
- **Shell 脚本**：自动化重复任务，简化运维。
- **网络与远程管理**：安全连接、调试和部署应用。
- **环境配置**：灵活管理开发工具链和依赖。

**进一步学习**:
- [Linux 命令行大全（TLDP）](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Linux From Scratch](https://www.linuxfromscratch.org/)（构建自定义系统）
- 推荐书籍：《鸟哥的 Linux 私房菜》《The Linux Command Line》
