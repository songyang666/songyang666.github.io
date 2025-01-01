---
date:
  created: 2025-01-01
categories:
  - Windows
  - mkdocs
readtime: 1
authors:
  - charlie
---
# Windows install mkdocs
## install winget
WinGet 命令行工具仅在 Windows 10 1709（版本 16299）或更高版本上受支持。 在首次以用户身份登录 Windows 之前，WinGet 将不可用，  
触发 Microsoft 应用商店将Windows 程序包管理器注册为异步进程的一部分。   
如果最近已经以用户身份进行了首次登录，但发现 WinGet 尚不可用，则可以打开 PowerShell 并输入以下命令来请求此 WinGet   
注册：Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe  
<https://learn.microsoft.com/zh-cn/windows/package-manager/winget/>

## install python
- check python exists
```bash
 python -V
```

- install python
```bash
winget search --id Python.Python
winget install -e --id Python.Python.3.11 --scope machine
python -V
```

## install mkdocs
```bash
pip install mkdocs
pip install mkdocs-material
mkdocs -V
```
## powershell 验证
- 安装powershell
  [install](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4)
- Set-ExecutionPolicy  
  <https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.4>
- try in powershell
```bash
mkdocc -V
```

- if failed  
    1. 在cmd 中运行where mkdocs  
    2. 将mkdocs的路径添加到系统环境变量path中
    3. 重启机器
    4. powershell verify  
```bash
gcm mkdocs 
Get-Command mkdocs
mkdocc -V
```
- powershell check path
```bash
Get-ChildItem env: 
```


