---
title: "TPM error while installing Windows 11 on ESXI or Unsupported Hardware"
seoTitle: "Windows 11 TPM Error while installing in ESXI"
seoDescription: "Windows 11 TPM Error while installing in ESXI VMware on unsupported hardware"
datePublished: Tue Aug 29 2023 19:30:10 GMT+0000 (Coordinated Universal Time)
cuid: cllwpdg1k000108ju51eb7kh6
slug: tpm-error-while-installing-windows-11-on-esxi-or-unsupported-hardware
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693233334881/618dc05d-274b-4aae-917c-6dce47954a80.png
tags: windows-10, esxi, windows-11, tpm, windows-error

---

### It's a common error while installing Windows 11 on an ESXI or an incompatible machine, Kindly follow the below solution to fix the issue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693232822836/42d9db47-be99-403c-ae4a-9d75ee62c642.png align="center")

**Error Image (Fig 1)**

# Fix for This PC can’t run Windows 11

* Step 1: Press the back icon on the top left
    
* Step 2: Press Shift + F10 to enter the command prompt windows
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693233022626/adbcf4ff-b1e5-49be-a82f-2e8313a95b40.png align="center")

* Step 3: Enter the below command to bypass the system requirement to install Windows 11
    

```bash
reg add HKLM\System\Setup\LabConfig /v BypassTPMCheck /t reg_dword /d 1
```

```bash
reg add HKLM\System\Setup\LabConfig /v BypassSecureBootCheck /t reg_dword /d 1
```

```bash
reg add HKLM\System\Setup\LabConfig /v BypassRAMCheck /t reg_dword /d 1
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693233048239/e1668525-fe7f-46d3-9060-86d7929b0ec7.png align="center")

* Step 4: Close the Command prompt and install Windows 11 without an error.