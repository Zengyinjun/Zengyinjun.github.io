+++
date = '2025-12-15T01:20:50+08:00'
title = 'My First Post'
+++

 
# 修复 WSL 网络配置错误 0x8007054f

当 WSL 报错 `createinstance/createvm/configurenetworking/0x8007054f` 并提示无法配置网络时，通常是由于网络服务或系统配置问题导致的。

---

## 错误信息
```
wsl: 出现了内部错误。
错误代码: createinstance/createvm/configurenetworking/0x8007054f
wsl: 无法配置网络 (networkingmode mirrored)，回退到 networkingmode none。
```

---

## 解决方案

### 1. 重启 HNS 服务
在管理员模式下运行 PowerShell，重启 Host Network Service (HNS) 服务：

```powershell
wsl --shutdown
net stop hns
net start hns
```

---

### 2. 重置 WSL 网络配置
如果问题仍然存在，可以尝试重置网络堆栈：

```powershell
netsh winsock reset
netsh int ip reset
```

执行后需要 **重启电脑**。

---

### 3. 完全关闭并重启 WSL
关闭所有 WSL 实例并重新启动服务：

```powershell
wsl --shutdown
wsl -d <你的发行版名称>
```

---

### 4. 检查 Hyper-V 和相关功能
确保 Windows 功能中的 **Hyper-V** 和 **Virtual Machine Platform** 已启用。

操作步骤：
1. 打开 **控制面板** → **程序** → **启用或关闭 Windows 功能**  
2. 勾选 **Hyper-V** 和 **虚拟机平台**  
3. 重启系统

---

## 参考
来源：https://www.vhcffh.com/2025/brc5Auzq


