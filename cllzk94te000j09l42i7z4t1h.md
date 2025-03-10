---
title: "Making Wallpaper as default without GPO and giving user freedom to change the wallpaper"
seoTitle: "Making Wallpaper as default without GPO"
seoDescription: "Making Wallpaper as default without GPO and giving user freedom to change the wallpaper"
datePublished: Thu Aug 31 2023 19:30:09 GMT+0000 (Coordinated Universal Time)
cuid: cllzk94te000j09l42i7z4t1h
slug: making-wallpaper-as-default-without-gpo-and-giving-user-freedom-to-change-the-wallpaper
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693300925832/8f85f580-fd6d-4c77-b93f-cad121663063.jpeg
tags: server, windows, powershell, wallpapers, group-policy

---

---

### As we know we can change the wallpaper in the user system by 2 methods, one is via manual way which only makes changes to the profile and one more method is to use the GPO.

But in these 2 methods, the wallpaper gets changed in a user profile or the wallpaper will be hardcoded to the system and the user will not be able to make any changes. But if you require to make a specific wallpaper as default and give the user the freedom to change the wallpaper then try out the below method, this method plays with Windows 11 default wallpaper it comes with, the Windows 11 default wallpaper is stored in the location “C:\\Windows\\Web\\Wallpaper\\Windows\\img0.jpg”

![Pic1: Image location](https://cdn.hashnode.com/res/hashnode/image/upload/v1693301054371/1d9ffe33-6c93-4130-9554-faec2ed1e9a5.png align="center")

Pic 1: Image location

![Pic 2: This is the wallpaper which is named img0.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1693300538669/b70c07cc-59b6-420b-b275-5912f2ee984f.jpeg align="center")

Pic 2: This is the wallpaper which is named img0.jpg

Now our goal is to replace this img0.jpg with the custom image that we have, If we try to replace the image without out custom image we get an error.

To fix this error we will execute the below script. This script will take Ownership & Grant Permissions & Delete files igmo.jpg and 4K Folder

```powershell
takeown /f C:\Windows\Web\wallpaper\Windows\img0.jpg
takeown /f C:\Windows\Web\4K\Wallpaper\Windows\*.*
icacls C:\windows\Web\Wallpaper\Windows\img0.jpg /Grant 'System:(F)'
icacls C:\Windows\Web\4K\Wallpaper\Windows\*.* /Grant 'System:(F)'
Remove-Item C:\windows\Web\Wallpaper\Windows\img0.jpg
Remove-Item C:\Windows\Web\4K\Wallpaper\Windows\*.*
```

After running the above command with PowerShell (admin) we can see the img0.jpg file is deleted, Now you can paste the custom image that you have and name it img0.jpg.

---

## If the img0.jpg file doesn't get deleted try the below method.

* **Step 1: Right-click on img0.jpg and click on properties.**
    
* **Step 2: Click on the security tab, select the Administrator user and click on Edit**
    
* **Step 3: Select Administrator user give full control and click on apply**
    

**Now we have full control over the img0.jpg, now we can delete the file and add our custom image.**

**Note: Paste the custom image to the path “C:\\Windows\\Web\\Wallpaper\\Windows\\” and rename the image to img0.jpg**

---