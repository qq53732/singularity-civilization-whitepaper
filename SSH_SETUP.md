# SSH Setup Guide for GitHub | GitHub SSH 设置指南

This guide will help you set up SSH authentication for GitHub repository access.
本指南将帮助你设置 SSH 认证以访问 GitHub 仓库。

---

## ⚠️ Important Security Notice | 重要安全提示

**SSH keys are sensitive credentials. You must generate them on your local machine.**
**SSH 密钥是敏感凭证，你必须在本地机器上生成。**

I cannot generate SSH keys for you because:
- Private keys must never be shared or transmitted
- GitHub requires your public key to be added to your account
- Only you should have access to your private key

---

## Step 1: Generate SSH Key | 生成 SSH 密钥

### On Linux/macOS | 在 Linux/macOS 上

```bash
# Generate a new SSH key using Ed25519 algorithm
# 使用 Ed25519 算法生成新的 SSH 密钥
ssh-keygen -t ed25519 -C "qq53732@gmail.com"

# When prompted, press Enter to accept default file location
# 提示时按 Enter 接受默认文件位置
# Enter passphrase (optional but recommended)
# 输入密码（可选但推荐）
```

### On Windows | 在 Windows 上

```powershell
# Using PowerShell or Git Bash
# 使用 PowerShell 或 Git Bash
ssh-keygen -t ed25519 -C "qq53732@gmail.com"
```

---

## Step 2: Add SSH Key to SSH Agent | 添加 SSH 密钥到 SSH 代理

### On Linux | 在 Linux 上

```bash
# Start the ssh-agent in the background
# 在后台启动 ssh-agent
eval "$(ssh-agent -s)"

# Add your SSH private key to the ssh-agent
# 添加 SSH 私钥到 ssh-agent
ssh-add ~/.ssh/id_ed25519
```

### On macOS | 在 macOS 上

```bash
# Start the ssh-agent
# 启动 ssh-agent
eval "$(ssh-agent -s)"

# Add SSH key to Apple Keychain (macOS specific)
# 添加 SSH 密钥到 Apple 钥匙串（macOS 特有）
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

---

## Step 3: Copy Public Key | 复制公钥

```bash
# Display your public key
# 显示你的公钥
cat ~/.ssh/id_ed25519.pub

# Copy the entire output (starts with ssh-ed25519)
# 复制整个输出（以 ssh-ed25519 开头）
```

Example output | 示例输出：
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDIhz2GK/XCUj4i6Q5yQJNL1MXMY0RxzPV2QrBqfHrDqq53732@gmail.com
```

---

## Step 4: Add to GitHub | 添加到 GitHub

1. **Login to GitHub** as `qq53732`
   **登录 GitHub** 账号 `qq53732`

2. Go to **Settings** → **SSH and GPG keys** → **New SSH key**
   前往 **设置** → **SSH 和 GPG 密钥** → **新建 SSH 密钥**

3. **Title**: My Laptop (or any descriptive name)
   **标题**：我的笔记本（或任何描述性名称）

4. **Key type**: Authentication Key
   **密钥类型**：认证密钥

5. **Key**: Paste your public key from Step 3
   **密钥**：粘贴第 3 步的公钥

6. Click **Add SSH key**
   点击 **添加 SSH 密钥**

---

## Step 5: Test SSH Connection | 测试 SSH 连接

```bash
# Test connection to GitHub
# 测试与 GitHub 的连接
ssh -T git@github.com

# You should see:
# 你应该看到：
# Hi qq53732! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Step 6: Clone Repository via SSH | 通过 SSH 克隆仓库

```bash
# Navigate to your workspace
# 导航到你的工作区
cd /root/.openclaw/workspace

# Extract the whitepaper package
# 解压白皮书包
tar -xzvf singularity-civilization-whitepaper.tar.gz

# Navigate to the directory
# 进入目录
cd singularity-civilization-whitepaper

# Initialize git
# 初始化 git
git init

# Add all files
# 添加所有文件
git add .

# Commit
# 提交
git commit -m "Initial commit: V1.0 Genesis Edition"

# Add remote using SSH (NOT HTTPS)
# 使用 SSH 添加远程仓库（不是 HTTPS）
git remote add origin git@github.com:qq53732/singularity-civilization-whitepaper.git

# Push to main branch
# 推送到 main 分支
git branch -M main
git push -u origin main
```

---

## SSH vs HTTPS Comparison | SSH 与 HTTPS 对比

| Feature | SSH | HTTPS |
|---------|-----|-------|
| Authentication | Key-based | Password/Token-based |
| Security | Higher | Standard |
| Convenience | No password needed after setup | Token may expire |
| GitHub Push | ✅ Yes | ⚠️ Requires token |

**Recommendation**: Use SSH for development machines you control.
**推荐**：对于你控制的开发机器，使用 SSH。

---

## Troubleshooting | 故障排除

### Permission denied (publickey)

```bash
# Check if ssh-agent is running
# 检查 ssh-agent 是否运行
eval "$(ssh-agent -s)"

# Add key again
# 重新添加密钥
ssh-add ~/.ssh/id_ed25519

# Test again
# 再次测试
ssh -T git@github.com
```

### Could not resolve hostname

```bash
# Check internet connection
# 检查网络连接
ping github.com

# Check SSH config
# 检查 SSH 配置
cat ~/.ssh/config
```

---

## Your SSH URL | 你的 SSH 地址

Once set up, your repository SSH URL is:
设置完成后，你的仓库 SSH 地址是：

```
git@github.com:qq53732/singularity-civilization-whitepaper.git
```

This is the URL you'll use for `git clone`, `git remote add`, etc.
这是你将用于 `git clone`、`git remote add` 等的 URL。

---

## Next Steps | 下一步

1. ✅ Generate SSH key on your local machine
   在本地机器上生成 SSH 密钥

2. ✅ Add public key to GitHub account
   添加公钥到 GitHub 账号

3. ✅ Test SSH connection
   测试 SSH 连接

4. ✅ Clone/push repository using SSH
   使用 SSH 克隆/推送仓库

5. ➡️ Follow GITHUB_SETUP.md for full repository configuration
   按照 GITHUB_SETUP.md 进行完整的仓库配置

---

**Need Help? | 需要帮助？**

- GitHub Docs: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
- Email: qq53732@gmail.com