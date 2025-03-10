---
title: "Automating Active Directory Host Movement with PowerShell"
seoTitle: "Automating Active Directory Host Movement with PowerShell"
seoDescription: "Automate Active Directory host movement with PowerShell script. Streamline server admin tasks and save time"
datePublished: Tue Sep 26 2023 18:30:09 GMT+0000 (Coordinated Universal Time)
cuid: cln0nk4c1000f09i80xepe0hm
slug: automating-active-directory-host-movement-with-powershell
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695645364393/b2c9def9-9b3d-4481-a926-7819f7c13703.png
tags: powershell-automation, powershell-scripting, powershell-activedirectory, auto-host-movement, activedirectory-automation

---

---

Managing and organizing computer objects within Active Directory can be a time-consuming task for server administrators, especially when there is no OS deployment tool in place. To streamline this process and improve efficiency, we've created a PowerShell script that automates the movement of computer objects to their respective Organizational Units (OUs) based on their hostnames. In this blog post, we'll walk you through the script's functionality and how it can save valuable time for IT engineers.

### **The Challenge**

Server administrators often find themselves faced with the challenge of manually moving computer objects within Active Directory to different OUs. This task can be particularly daunting in large environments with numerous computers, each requiring placement in a specific OU based on naming conventions. Without automation, this process can be time-consuming and prone to errors.

### **The Solution: Auto AD Host Movement Script**

Our PowerShell script is designed to address this challenge by automating the process of moving computer objects in Active Directory. Here's how it works:

* **Hostname Matching**: The script starts by searching the default Computer Organization Unit (OU) for computer objects whose hostnames match specific patterns (e.g., "Test-INBG\*"). It's crucial to note that the script excludes objects containing "*VDI*" in their names to prevent unintended movements.
    
* **Organizational Unit Assignment**: Once a matching computer object is found, the script moves it to the appropriate OU based on predefined rules. For example, computers with hostnames matching "Test-INBG\*" are moved to "OU=DELIVERY,OU=INDIA,OU=QT\_Computers,DC=test,DC=LOCAL."
    
* **Logging**: The script logs all its actions to a designated log file, making it easy to track and review the operations it performs.
    
* **Automation Loop**: To ensure continuous monitoring and automation, the script runs in an infinite loop, checking for matching hostnames and moving objects to their respective OUs every 5 minutes. This hands-off approach significantly reduces the manual effort required from IT engineers.
    

### **Benefits**

Implementing the Auto AD Host Movement script offers several key benefits:

* **Time Efficiency**: By automating the process of moving computer objects within Active Directory, IT engineers can focus on more critical tasks, saving valuable time.
    
* **Error Reduction**: Automation reduces the risk of human errors that can occur during manual operations.
    
* **Consistency**: The script ensures that computer objects are consistently placed in the correct OUs, aligning with established naming conventions.
    
* **Easy Monitoring**: Logging operations to a log file enables easy tracking and auditing of changes made by the script.
    

### **Conclusion**

Automating routine tasks in Active Directory can greatly improve operational efficiency and reduce the workload of IT engineers. Our Auto AD Host Movement script simplifies the process of moving computer objects to their respective OUs based on hostnames, allowing server administrators to manage their environment more effectively. Whether you're dealing with a small or large Active Directory infrastructure, this script can help streamline your operations and ensure consistency in your organization's structure.

---

```powershell
do
{
$download_path="C:\Program Files\test\test\test.exe";


$INBGADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-INBG*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($INBG in $INBGADComps){

Get-ADComputer $INBG |Move-ADObject -TargetPath "OU=DELIVERY,OU=INDIA,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$INNOADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-INNO*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($INNO in $INNOADComps){

Get-ADComputer $INNO |Move-ADObject -TargetPath "OU=Delivery,OU=Noida,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$DEADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-DE*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($DE in $DEADComps){

Get-ADComputer $DE |Move-ADObject -TargetPath "OU=Delivery,OU=GERMANY,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$ILADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-IL*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($IL in $ILADComps){

Get-ADComputer $IL |Move-ADObject -TargetPath "OU=DELIVERY,OU=ISRAEL,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$USADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-US*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($US in $USADComps){

Get-ADComputer $US |Move-ADObject -TargetPath "OU=DELIVERY,OU=USA,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}
 
$ROADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-RO*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($RO in $ROADComps){

Get-ADComputer $RO |Move-ADObject -TargetPath "OU=DELIVERY,OU=Rwanda,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$UKADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-UK*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($UK in $UKADComps){

Get-ADComputer $UK |Move-ADObject -TargetPath "OU=Delivery,OU=United Kingdom,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}
 
$INHDADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-INHD*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($INHD in $INHDADComps){

Get-ADComputer $INHD |Move-ADObject -TargetPath "OU=DELIVERY,OU=Hyderabad,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$INCHADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-INCH*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($INCH in $INCHADComps){

Get-ADComputer $INCH |Move-ADObject -TargetPath "OU=Delivery,OU=CHENNAI,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$CAComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-CA*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($CA in $CAComps){

Get-ADComputer $CA |Move-ADObject -TargetPath "OU=DELIVERY,OU=Combodia,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}


$ARADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-AR*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($AR in $ARADComps){

Get-ADComputer $AR |Move-ADObject -TargetPath "OU=DELIVERY,OU=America,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$MXADComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object {($_.Name -Like "Test-MX*") -and ($_.Name -notlike "*VDI*")} | Select-Object -ExpandProperty Name
foreach($MX in $MXADComps){

Get-ADComputer $MX |Move-ADObject -TargetPath "OU=DELIVERY,OU=USA,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}

$VDIComps= Get-ADComputer -Filter * -SearchBase "CN=Computers,DC=test,DC=LOCAL"| Select-Object -Property Name | Where-Object Name -Like "*VDI*" | Select-Object -ExpandProperty Name
foreach($VDI in $VDIComps){

Get-ADComputer $VDI |Move-ADObject -TargetPath "OU=VDI,OU=INDIA,OU=QT_Computers,DC=test,DC=LOCAL" -Verbose 4>&1 | Tee-Object -Append -FilePath "C:\Users\Public\HostMovement\Hostmovement.txt"

}


[System.GC]::Collect()
Start-Sleep -Seconds 300

} while($true)


<#
_________                                ________    _________
\______   \_____ ___  _______    ____    /  _____/   /   _____/
 |     ___/\__  \\  \/ /\__  \  /    \  /   \  ___   \_____  \ 
 |    |     / __ \\   /  / __ \|   |  \ \    \_\  \  /        \
 |____|    (____  /\_/  (____  /___|  /  \______  / /_______  /
                \/           \/     \/          \/          \/ 
#>
```

---