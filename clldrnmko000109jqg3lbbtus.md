---
title: "Reuse of Hostname error while re-joining to domain in windows 10 & 11"
seoTitle: "Active Directory blocked by security policy domain rejoin"
seoDescription: "An account with the same name exists in Active Directory. Re-using the account was blocked by security policy."
datePublished: Wed Aug 16 2023 13:26:27 GMT+0000 (Coordinated Universal Time)
cuid: clldrnmko000109jqg3lbbtus
slug: reuse-of-hostname-error-while-re-joining-to-domain-in-windows-10-11
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693232560469/ee34058f-4c83-4b93-b8a8-1e6f2b86c9f1.png
tags: windows-10, hostname, windows-11, domain-rejoin, reuse-of-hostname

---

### Error Message: An account with the same name exists in Active Directory. Re-using the account was blocked by security policy.

### Error Image:

![This is the error message - Account-Reuse-Blocked-By-Policy](https://windowstechno.com/wp-content/uploads/2022/11/Error.jpg align="center")

## Resolution

Evaluate the computer account provisioning procedures to see if any changes are necessary.

* Use the same account that set up the computer account in the target domain to perform the join operation.
    
* Before attempting to rejoin the domain once again, remove the existing account if it is stale (unused).
    
* Join with a different account that doesn’t already exist and rename the computer.
    

**Workaround that is tested and working fine on several server objects.**

The following registry entry can be temporarily set at the level of each client machine if the current account is controlled by a trusted security principal and the administrator wants to reuse the account.

Once the join process is finished, delete the registry setting right away. The registry key may be changed without attempting to restart the computer.

| Path | HKLM\\System\\CurrentControlSet\\Control\\LSA |
| --- | --- |
| **Type** | **REG\_DWORD** |
| **Name** | **NetJoinLegacyAccountReuse** |
| **Value** | **1 Other values are ignored.** |

Command to add it via command prompt

```bash
reg add HKLM\System\CurrentControlSet\Control\LSA /v NetJoinLegacyAccountReuse /t REG_DWORD /d 1 /f
```