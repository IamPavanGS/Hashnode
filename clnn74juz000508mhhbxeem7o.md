---
title: "AD user offboarding GUI tool"
seoTitle: "PowerShell User Offboarding: Simplify AD Management"
seoDescription: "Simplify AD user offboarding with a PowerShell tool. Disable accounts, manage security groups, and track changes effortlessly.Powershell GUI tool,Powershell"
datePublished: Thu Oct 12 2023 13:08:51 GMT+0000 (Coordinated Universal Time)
cuid: clnn74juz000508mhhbxeem7o
slug: ad-user-offboarding-gui-tool
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697113546639/11ecf01d-27b4-4d32-bdd4-6757cfa35894.jpeg
tags: powershell-automation, user-account-management, disable-ad-account, automate-offboarding, powershell-tool

---

User offboarding is a critical process in every organization, ensuring that the departure of employees is handled securely and efficiently. To streamline this process and minimize human errors, we'll create a powerful PowerShell tool that not only disables Active Directory (AD) accounts but also removes users from all security groups, moves them to a "Disabled Users" Organizational Unit (OU), and adds an exit date timestamp to their display names.

---

### Let's break down the step-by-step process of how this PowerShell tool for user offboarding works:

Launch the application by either double-clicking it or executing the PowerShell script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697111706379/1c4590ac-6a56-4f2c-91eb-942823fa0020.png align="center")

After launching the application, enter the username of the user you wish to offboard and then click on the "Search" button. A pop-up will appear displaying matching usernames for you to select from.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697111796837/c9367986-ac87-4d69-a4bf-92a1ae76c6b6.png align="center")

As you can observe in the image below, the application will collect essential user details such as Email, Reporting Manager, Last login, Display Name, and Account Status. These details will be prominently displayed within the application for your reference.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697111897044/db68df2a-2e11-4b6f-928a-7a3cb9637dcc.png align="center")

Once you have verified that this is indeed the user you wish to offboard, you can proceed by clicking on the "Disable" button to perform the offboarding process in Active Directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697111972995/02872aa6-f584-412f-80bf-34f846fef06c.png align="center")

After the disable process is completed, a pop-up notification will inform you that the Active Directory account of the specified user has been disabled. Additionally, this notification message will be copied to your clipboard. During this process, the following actions will be performed:

1. **AD Account Disabled:** The user's Active Directory account is disabled, ensuring that they can no longer access network resources.
    
2. **User Moved to Disabled User OU:** The user will be transferred to the "Disabled User" Organizational Unit (OU) within Active Directory. This organizational unit is typically used to segregate disabled or offboarded users from the rest of the user accounts.
    
3. **Removal from Security Groups:** The tool will remove the user from all security groups to prevent any unintended access or permissions that may have been associated with their account.
    
4. **Timestamp Added to Display Name:** The current date is added as a timestamp to the user's display name, indicating when the offboarding process was executed. This can be helpful for record-keeping and tracking.
    

These actions help ensure a secure and well-documented offboarding process while minimizing the chances of errors or oversights.

Upon the completion of the offboarding process, comprehensive logs containing all the relevant details will be automatically generated and saved in a specific location for future reference. These logs will be stored in the directory:

**C:\\Users\\Public**

Having these logs readily available is invaluable for auditing, compliance, and record-keeping purposes. It provides transparency and accountability in the offboarding process, ensuring that all steps are executed correctly and in compliance with organizational policies and security protocols.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697112230345/a04f53d4-3f9b-4561-af5d-a9eb03975cd1.png align="center")

## Here is the full PowerShell code for the tool:

```powershell
[void][System.Reflection.Assembly]::LoadWithPartialName("System.Windows.Forms")
[void][System.Reflection.Assembly]::LoadWithPartialName("System.Drawing")

#~~< User Offboarding >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$User_Offboarding = New-Object System.Windows.Forms.Form
$User_Offboarding.ClientSize = New-Object System.Drawing.Size(705, 325)
$User_Offboarding.Text = "User Offboarding"
$User_Offboarding.FormBorderStyle = [System.Windows.Forms.FormBorderStyle]::FixedSingle
$User_Offboarding.MaximizeBox = $false

$base64Icon = "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"
$iconBytes = [System.Convert]::FromBase64String($base64Icon)
$iconStream = New-Object System.IO.MemoryStream
$iconStream.Write($iconBytes, 0, $iconBytes.Length)
$User_Offboarding.Icon = [System.Drawing.Icon]::FromHandle((New-Object System.Drawing.Bitmap $iconStream).GetHicon())

# Set form background color and font
$User_Offboarding.BackColor = [System.Drawing.Color]::White
$User_Offboarding.Font = New-Object System.Drawing.Font("Tahoma", 10, [System.Drawing.FontStyle]::Regular)

#~~< disable_btn >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$disable_btn = New-Object System.Windows.Forms.Button
$disable_btn.Font = New-Object System.Drawing.Font("Tahoma", 8.25, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$disable_btn.Location = New-Object System.Drawing.Point(565, 278)
$disable_btn.Size = New-Object System.Drawing.Size(113, 23)
$disable_btn.TabIndex = 11
$disable_btn.Text = "Disable"
$disable_btn.UseVisualStyleBackColor = $true
$disable_btn.add_Click({Disable_btnClick($disable_btn)})
#~~< Display_Name_lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Display_Name_lbl = New-Object System.Windows.Forms.Label
$Display_Name_lbl.Location = New-Object System.Drawing.Point(195, 223)
$Display_Name_lbl.Size = New-Object System.Drawing.Size(305, 23)
$Display_Name_lbl.TabIndex = 10
$Display_Name_lbl.Text = ""
$Display_Name_lbl.add_Click({Display_Name_lblClick($Display_Name_lbl)})
#~~< Label4 >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Label4 = New-Object System.Windows.Forms.Label
$Label4.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Label4.Location = New-Object System.Drawing.Point(27, 223)
$Label4.Size = New-Object System.Drawing.Size(148, 23)
$Label4.TabIndex = 9
$Label4.Text = "Display Name:"
#~~< Last_Loggedon_lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Last_Loggedon_lbl = New-Object System.Windows.Forms.Label
$Last_Loggedon_lbl.Location = New-Object System.Drawing.Point(195, 173)
$Last_Loggedon_lbl.Size = New-Object System.Drawing.Size(305, 23)
$Last_Loggedon_lbl.TabIndex = 8
$Last_Loggedon_lbl.Text = ""
$Last_Loggedon_lbl.add_Click({Last_Loggedon_lblClick($Last_Loggedon_lbl)})
#~~< Label3 >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Label3 = New-Object System.Windows.Forms.Label
$Label3.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Label3.Location = New-Object System.Drawing.Point(27, 173)
$Label3.Size = New-Object System.Drawing.Size(148, 23)
$Label3.TabIndex = 7
$Label3.Text = "Last LoggedOn:"
#~~< Reporting_mgr_lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Reporting_mgr_lbl = New-Object System.Windows.Forms.Label
$Reporting_mgr_lbl.Location = New-Object System.Drawing.Point(195, 126)
$Reporting_mgr_lbl.Size = New-Object System.Drawing.Size(305, 23)
$Reporting_mgr_lbl.TabIndex = 6
$Reporting_mgr_lbl.Text = ""
#~~< Label2 >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Label2 = New-Object System.Windows.Forms.Label
$Label2.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Label2.Location = New-Object System.Drawing.Point(27, 126)
$Label2.Size = New-Object System.Drawing.Size(148, 23)
$Label2.TabIndex = 5
$Label2.Text = "Reporting Manager:"
#~~< Email_Lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Email_Lbl = New-Object System.Windows.Forms.Label
$Email_Lbl.Location = New-Object System.Drawing.Point(195, 80)
$Email_Lbl.Size = New-Object System.Drawing.Size(305, 23)
$Email_Lbl.TabIndex = 4
$Email_Lbl.Text = ""
$Email_Lbl.add_Click({Email_LblClick($Email_Lbl)})
#~~< Status_Lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

$Enabled_lbl = New-Object System.Windows.Forms.Label
$Enabled_lbl.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Enabled_lbl.Location = New-Object System.Drawing.Point(27, 270)
$Enabled_lbl.Size = New-Object System.Drawing.Size(130, 23)
$Enabled_lbl.TabIndex = 12
$Enabled_lbl.Text = "Account Enabled:"


$Check_Enabled_lbl = New-Object System.Windows.Forms.Label
#$Check_Enabled_lbl.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Check_Enabled_lbl.Location = New-Object System.Drawing.Point(195, 270)
$Check_Enabled_lbl.Size = New-Object System.Drawing.Size(200, 23)
$Check_Enabled_lbl.TabIndex = 13
$Check_Enabled_lbl.Text = ""


#~~< Label1 >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Label1 = New-Object System.Windows.Forms.Label
$Label1.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Label1.Location = New-Object System.Drawing.Point(27, 80)
$Label1.Size = New-Object System.Drawing.Size(100, 23)
$Label1.TabIndex = 3
$Label1.Text = "Email:"
#~~< Search_btn >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Search_btn = New-Object System.Windows.Forms.Button
$Search_btn.Location = New-Object System.Drawing.Point(565, 25)
$Search_btn.Size = New-Object System.Drawing.Size(113, 23)
$Search_btn.TabIndex = 2
$Search_btn.Text = "Search"
$Search_btn.UseVisualStyleBackColor = $true
$Search_btn.add_Click({Search_btnClick($Search_btn)})
#~~< username_textbox >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$username_textbox = New-Object System.Windows.Forms.RichTextBox
$username_textbox.Location = New-Object System.Drawing.Point(195, 26)
$username_textbox.Size = New-Object System.Drawing.Size(305, 22)
$username_textbox.TabIndex = 1
$username_textbox.Text = ""
#$username_textbox.add_TextChanged({Username_textboxTextChanged($username_textbox)})
#~~< Username_lbl >~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$Username_lbl = New-Object System.Windows.Forms.Label
$Username_lbl.Font = New-Object System.Drawing.Font("Tahoma", 10.0, [System.Drawing.FontStyle]::Bold, [System.Drawing.GraphicsUnit]::Point, ([System.Byte](0)))
$Username_lbl.Location = New-Object System.Drawing.Point(27, 25)
$Username_lbl.Size = New-Object System.Drawing.Size(100, 23)
$Username_lbl.TabIndex = 0
$Username_lbl.Text = "Username:"
$User_Offboarding.Controls.Add($disable_btn)
$User_Offboarding.Controls.Add($Display_Name_lbl)
$User_Offboarding.Controls.Add($Label4)
$User_Offboarding.Controls.Add($Last_Loggedon_lbl)
$User_Offboarding.Controls.Add($Label3)
$User_Offboarding.Controls.Add($Reporting_mgr_lbl)
$User_Offboarding.Controls.Add($Label2)
$User_Offboarding.Controls.Add($Email_Lbl)
$User_Offboarding.Controls.Add($Label1)
$User_Offboarding.Controls.Add($Search_btn)
$User_Offboarding.Controls.Add($username_textbox)
$User_Offboarding.Controls.Add($Username_lbl)
$User_Offboarding.Controls.Add($Enabled_lbl)
$User_Offboarding.Controls.Add($Check_Enabled_lbl)

function Main{
	[System.Windows.Forms.Application]::EnableVisualStyles()
	[System.Windows.Forms.Application]::Run($User_Offboarding)
}



function Disable_btnClick( $object ){


function Write-Log {
    param (
        [string]$Message,
        [string]$LogPath
    )
    
    $LogEntry = "$(Get-Date -Format 'yyyy-MM-dd HH:mm:ss') - $Message"
    $LogEntry | Out-File -Append -FilePath $LogPath
}



 $LogPath = "C:\Users\Public\Userooffboard.log"  # Update with the actual path

    # Assuming $username_textbox.Text contains the username of the account to disable
    
    # Log the start of the process
    Write-Log "Starting the account removal process for $($username_textbox.Text)" -LogPath $LogPath
    
    # Disable the user account in Active Directory
    Disable-ADAccount -Identity $username_textbox.Text
    Write-Log "Disabled user account: $($username_textbox.Text)" -LogPath $LogPath
    
    # Move the disabled user account to the specified organizational unit (OU)
    Get-ADUser $username_textbox.Text | Move-ADObject -TargetPath 'OU=Disabled users, OU=Users, DC=Test.local'
    Write-Log "Moved user account: $($username_textbox.Text) to OU=Disabled users, OU=Users, DC=Test.local" -LogPath $LogPath
    
    # Get the user's current group memberships and remove them from those groups
    $userGroups = Get-ADUser -Identity $username_textbox.Text -Properties MemberOf |
                  Select-Object -ExpandProperty MemberOf

    foreach ($group in $userGroups) {
        # Get the group's information
        $groupInfo = Get-ADGroup $group

        # Remove the user from the group
        Remove-ADGroupMember -Identity $group -Members $username_textbox.Text -Confirm:$false

        # Log the removal
        Write-Log "Removed $($username_textbox.Text) from group: $($groupInfo.Name)" -LogPath $LogPath
    }

$todayDate = Get-Date -Format "dd-MM-yy"

$identity = $username_textbox.Text

$newDisplayName = "[Exited on_$todayDate]"

$currentUser = Get-ADUser -Identity $identity
$currentDisplayName = $currentUser.Name

$combinedDisplayName = "$currentDisplayName $newDisplayName"

Set-ADUser -Identity $identity -DisplayName $combinedDisplayName


[string]$user = $username_textbox.Text


[System.Windows.Forms.MessageBox]::Show("User $user account has been disabled ", "Information", [System.Windows.Forms.MessageBoxButtons]::OK, [System.Windows.Forms.MessageBoxIcon]::Information)
Set-Clipboard -Value "AD account disabled for the user $user and removed from all the security groups."

}


function Search_btnClick( $object ){
    # Get the entered username from the textbox
    $enteredUsername = $username_textbox.Text

    # Simulate fetching matching usernames from Active Directory
    # Replace this with your actual logic to query Active Directory
    $matchingUsernames = Get-ADUser -Filter "SamAccountName -like '$enteredUsername*'" |
                         Select-Object -ExpandProperty SamAccountName

    # Create a new form for selecting from matching usernames
    $Username_Select = New-Object System.Windows.Forms.Form
    $Username_Select.ClientSize = New-Object System.Drawing.Size(300, 200)
    $Username_Select.Text = "Select Username"
    $Username_Select.FormBorderStyle = [System.Windows.Forms.FormBorderStyle]::FixedSingle
$Username_Select.MaximizeBox = $false

    # Set form background color and font
$Username_Select.BackColor = [System.Drawing.Color]::White
$Username_Select.Font = New-Object System.Drawing.Font("Tahoma", 10, [System.Drawing.FontStyle]::Regular)

    $ListBox = New-Object System.Windows.Forms.ListBox
    $ListBox.Location = New-Object System.Drawing.Point(50, 50)
    $ListBox.Size = New-Object System.Drawing.Size(200, 100)

    # Populate the list box with matching usernames
    $ListBox.Items.AddRange($matchingUsernames)

    $Select_Button = New-Object System.Windows.Forms.Button
    $Select_Button.Location = New-Object System.Drawing.Point(100, 160)
    $Select_Button.Size = New-Object System.Drawing.Size(100, 25)
    $Select_Button.Text = "Select"
    $Select_Button.Add_Click({
        $selectedUsername = $ListBox.SelectedItem
        $username_textbox.Text = $selectedUsername
        $Username_Select.Close()

        # Retrieve user information based on the selected username
        $aduser = Get-AdUser -Identity $selectedUsername -Properties Manager
        $manager = Get-AdUser $aduser.Manager -Properties DisplayName

        $aduser_email = Get-ADUser -Identity $selectedUsername -properties mail | Select -ExpandProperty mail

        $aduser_lastlogon = Get-ADUser -Identity $selectedUsername -Properties "LastLogonDate" | Select-Object -ExpandProperty LastLogonDate

        $aduser_enabled = Get-ADUser $selectedUsername -properties enabled,PasswordExpired | select -ExpandProperty enabled

        $aduser_displayname = Get-AdUser -Identity $selectedUsername -Properties * | Select -ExpandProperty DisplayName

        #$aduser_displayname = $aduser.Name
        #$aduser_email = $aduser.mail
        #$aduser_lastlogon = $aduser.LastLogonDate

        # Populate labels with retrieved user information
        $Display_Name_lbl.Text = $aduser_displayname
        $Last_Loggedon_lbl.Text = $aduser_lastlogon
        $Reporting_mgr_lbl.Text = $manager.DisplayName
        $Email_Lbl.Text = $aduser_email
        $Check_Enabled_lbl.Text = $aduser_enabled

        # Set the text color of the Enabled label based on the account status
if ($aduser_enabled -eq "True") {
    $Check_Enabled_lbl.ForeColor = [System.Drawing.Color]::Green
} else {
    $Check_Enabled_lbl.ForeColor = [System.Drawing.Color]::Red
}
    })

    $Username_Select.Controls.Add($ListBox)
    $Username_Select.Controls.Add($Select_Button)

    # Show the username selection form
    $Username_Select.ShowDialog()
}



Main 
```

Here is the PowerShell code for your reference, and you can modify the following line to tailor it to your specific environment:

```powershell
Get-ADUser $username_textbox.Text | Move-ADObject -TargetPath 'OU=Disabled users, OU=Users, DC=Test.local'
Write-Log "Moved user account: $($username_textbox.Text) to OU=Disabled users, OU=Users, DC=Test.local" -LogPath $LogPath
```

---