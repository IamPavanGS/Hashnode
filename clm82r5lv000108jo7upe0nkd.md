---
title: "ADWiz - Active Directory User creation Tool"
seoTitle: "ADWiz: The Ultimate Active Directory User Creation Tool"
seoDescription: "Discover the Ultimate Active Directory User Creation Tool - ADWiz. Streamline account management, automate tasks, and enhance IT efficiency. Try ADWiz today"
datePublished: Wed Sep 06 2023 18:30:13 GMT+0000 (Coordinated Universal Time)
cuid: clm82r5lv000108jo7upe0nkd
slug: adwiz-active-directory-user-creation-tool
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693909449023/65220b33-4292-4ab2-88c2-b1dd1b27fd6d.png
tags: active-directory, powershell-gui, powershell-scripting, user-account-creation, it-efficiency

---

---

In the world of IT administration, efficiency and simplicity are paramount. Imagine having a powerful tool at your disposal, designed to alleviate the complexities of managing Active Directory accounts seamlessly. Say hello to our cutting-edge creation – a robust PowerShell GUI tool that empowers IT administrators to effortlessly handle the intricacies of user account management.

This exceptional tool boasts a wide array of features, each meticulously crafted to enhance the IT admin's workflow. With a user-friendly interface, it simplifies the process of creating Active Directory accounts by collecting and configuring essential attributes such as First Name, Last Name, Display Name, Username, Email address, Job Title, and Reporting Manager. But that's not all; it goes the extra mile by offering advanced functionalities that truly set it apart.

One such feature is the capability to generate random passwords with a single click, eliminating the need for manual password generation and enhancing security. What's more, this tool ensures added convenience by automatically copying the generated password to your clipboard, ready for immediate use.

The power of this tool truly shines when the create button is pressed. It seamlessly executes a series of crucial tasks behind the scenes. Not only does it create a user account with precision and accuracy, but it also intelligently moves the object to the selected organizational unit (OU) – a time-saving maneuver that simplifies account organization. Additionally, it extends its functionality by seamlessly adding the user to a designated common security group, streamlining access management and enhancing security posture.

In a world where time is of the essence, this PowerShell GUI tool emerges as a game-changer, equipping IT administrators with the means to perform their tasks efficiently and effectively. Simplify your Active Directory account management today and experience the difference this remarkable tool can make in your IT admin journey.

---

# Screenshots

*First look at the application*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693841598963/3221eb38-2302-4df1-ac37-41db11122bb3.png align="center")

*When the Random Password button is clicked the application will generate 14 characters random password and will automatically copy it to the clipboard.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693841701092/08fa4705-e129-4874-9a8f-5246a69bda61.png align="center")

*Location Drop-down list which can be modified as per your organization's locations, By selecting this the user will be moved to the selected OU*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693841615273/4b9deda1-d084-4108-aad4-a2c177f6c45c.png align="center")

---

# Source Code

```powershell
Add-Type -AssemblyName PresentationFramework
[xml]$xaml = @"
<Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="ADWiz" Height="425" Width="550" >
    <Grid Background="#ECEFF1">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="125"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        

        <Label Content="First Name:" Grid.Row="0" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="FirstNameTextBox" Grid.Row="0" Grid.Column="1" Margin="5"/>

        <Label Content="Last Name:" Grid.Row="1" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="LastNameTextBox" Grid.Row="1" Grid.Column="1" Margin="5"/>

                <Label Content="DisplayName:" Grid.Row="2" Grid.Column="0" Margin="5"/>
               <TextBox x:Name="DisplayNameTextBox" Grid.Row="2" Grid.Column="1" Margin="5">
            <TextBox.Text>
                <MultiBinding StringFormat="{}{0} {1}">
                    <Binding Path="Text" ElementName="FirstNameTextBox" Mode="OneWay" UpdateSourceTrigger="PropertyChanged"/>
                    <Binding Path="Text" ElementName="LastNameTextBox" Mode="OneWay" UpdateSourceTrigger="PropertyChanged"/>
                </MultiBinding>
            </TextBox.Text>
        </TextBox>

        <Label Content="Username:" Grid.Row="3" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="UsernameTextBox" Grid.Row="3" Grid.Column="1" Margin="5"/>

        <Label Content="Email:" Grid.Row="4" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="EmailTextBox" Grid.Row="4" Grid.Column="1" Margin="5"/>

        <Label Content="Password:" Grid.Row="5" Grid.Column="0" Margin="5" Visibility="Visible"/>
        <PasswordBox x:Name="PasswordBox" Grid.Row="5" Grid.Column="1" Margin="5"/>
        <CheckBox x:Name="ChangePasswordCheckBox" Grid.Row="9" Grid.Column="1" Margin="5" Content="Change password at next logon"/>

        <Button x:Name="GeneratePasswordButton" Content="Random Passwd" Grid.Row="5" Grid.Column="0" Margin="5" Background="#B0BEC5"/>

        <Label Content="Job Title:" Grid.Row="6" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="JobTitleTextBox" Grid.Row="6" Grid.Column="1" Margin="5"/>

         <Label Content="Reporting Manager:" Grid.Row="7" Grid.Column="0" Margin="5"/>
        <TextBox x:Name="ReportingManagerTextBox" Grid.Row="7" Grid.Column="1" Margin="5"/>

        <Label Content="Location:" Grid.Row="8" Grid.Column="0" Margin="5"/>
        <ComboBox x:Name="LocationComboBox" Grid.Row="8" Grid.Column="1" Margin="5">
            <ComboBoxItem Content="Bangalore"/>
            <ComboBoxItem Content="Hyderabad"/>
            <ComboBoxItem Content="Noida"/>
            <ComboBoxItem Content="Chennai"/>
            <ComboBoxItem Content="Romania"/>
            <ComboBoxItem Content="Israel"/>
            <ComboBoxItem Content="Madagascar"/>
            <ComboBoxItem Content="California"/>
            <ComboBoxItem Content="Canada"/>
            <ComboBoxItem Content="Germany"/>
            <ComboBoxItem Content="Mexico"/>
            <ComboBoxItem Content="UK"/>
            <ComboBoxItem Content="San Diego"/>
            <ComboBoxItem Content="Argentina"/>
        </ComboBox>
    
        <Button x:Name="CreateUserButton" Content="Create User" Grid.Row="9" Grid.Column="1" Margin="5" Background="#2196F3" Foreground="White" FontWeight="Bold" FontSize="16" Padding="10 5" HorizontalAlignment="Right" VerticalAlignment="Center"/>
        <TextBlock Text="Created by Pavan G S" Grid.Row="10" Grid.Column="1" Margin="5" HorizontalAlignment="Left" VerticalAlignment="Bottom"/>
        

    </Grid>
</Window>
"@

$reader = (New-Object System.Xml.XmlNodeReader $xaml)
$window = [Windows.Markup.XamlReader]::Load($reader)

$UsernameTextBox = $window.FindName("UsernameTextBox")
$PasswordBox = $window.FindName("PasswordBox")
$FirstNameTextBox = $window.FindName("FirstNameTextBox")
$LastNameTextBox = $window.FindName("LastNameTextBox")
$EmailTextBox = $window.FindName("EmailTextBox")
$LocationComboBox = $window.FindName("LocationComboBox")
$CreateButton = $window.FindName("CreateUserButton")
$GeneratePasswordButton = $window.FindName("GeneratePasswordButton")
$ReportingManagerTextBox = $window.FindName("ReportingManagerTextBox")
$DisplayNameTextBox = $window.FindName("DisplayNameTextBox")
$JobTitleTextBox = $window.FindName("JobTitleTextBox")
$ChangePasswordCheckBox = $window.FindName("ChangePasswordCheckBox")



$GeneratePasswordButton.Add_Click({
$chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()-_=+[]{};:,.<>?`~"
$passwordLength = 14
$password = -join ($chars.ToCharArray() | Get-Random -Count $passwordLength)
$PasswordBox.Password = $password
# Copy the password to the clipboard
$password | Set-Clipboard
})

$CreateButton.Add_Click({
# Get user input from the form
$username = $UsernameTextBox.Text
$password = $PasswordBox.Password
$firstname = $FirstNameTextBox.Text
$lastname = $LastNameTextBox.Text
$email = $EmailTextBox.Text
$location = $LocationComboBox.Text
$displayname = $DisplayNameTextBox.Text
$manager = $ReportingManagerTextBox.Text
$jobtitle = $JobTitleTextBox.Text
$changePassword = $ChangePasswordCheckBox.IsChecked

if ($jobtitle -eq $null) {
        $jobtitle = "Unknown"
    }

    if ($manager -eq $null) {
        $manager = "None"
    }

# Set the country and OU based on the selected location
switch ($location) {
    "Bangalore" {
        $replaceParams = @{
        c = "IN"
        co = "India"
        countrycode = 356
        }
        $ou = "OU=DELIVERY,OU=INDIA,OU=Users,DC=Test,DC=LOCAL"
         $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Bangalore_Employees"
        break
    }
    "UK" {
        $replaceParams = @{
        c = "GB"
        co = "United Kingdom"
        countrycode = 826
        }
        $ou = "OU=DELIVERY,OU=UK,OU=Users,DC=Test,DC=LOCAL"
          $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "UK_Employee"
        break
    }
    "California" {
        $replaceParams = @{
        c = "US"
        co = "United States"
        countrycode = 840
        }
        $ou = "OU=Delivery,OU=California,OU=Users,DC=Test,DC=LOCAL"
         $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "US_Employee"
        break
    }
     "Canada" {
        $replaceParams = @{
        c = "CA"
        co = "Canada"
        countrycode = 124
        }
        $ou = "OU=DELIVIRY,OU=Canada,OU=Users,DC=Test,DC=LOCAL"
      $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "US_Employee"

        break
    }
     "Chennai" {
        $replaceParams = @{
        c = "IN"
        co = "India"
        countrycode = 356
        }
        $ou = "OU=Delivery,OU=Chennai,OU=Users,DC=Test,DC=LOCAL"
        $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Chennai_Employee"
        break
    }
     "Germany" {
        $replaceParams = @{
        c = "DE"
        co = "Germany"
        countrycode = 276
        }
        $ou = "OU=Delivery,OU=GERMANY,OU=Users,DC=Test,DC=LOCAL"
       $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Germany_Employee"
        break
    }
     "Hyderabad" {
        $replaceParams = @{
        c = "IN"
        co = "India"
        countrycode = 356
        }
        $ou = "OU=Delivery,OU=Hyderabad,OU=Users,DC=Test,DC=LOCAL"
       $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Hyderabad_Employee"
        break
    }
     "Noida" {
        $replaceParams = @{
        c = "IN"
        co = "India"
        countrycode = 356
        }
        $ou = "OU=Delivery,OU=Noida,OU=Users,DC=Test,DC=LOCAL"
       $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Noida_Employees"
        break
    }
     "Israel" {
        $replaceParams = @{
        c = "IL"
        co = "Israel"
        countrycode = 376
        }
        $ou = "OU=DELIVERY,OU=ISRAEL,OU=Users,DC=Test,DC=LOCAL"
        $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Israel_Employee"
        break
    }
     "Madagascar" {
        $replaceParams = @{
        c = "MG"
        co = "Madagascar"
        countrycode = 450
        }
        $ou = "OU=Delivery,OU=Madagascar,OU=Users,DC=Test,DC=LOCAL"
      $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Madagascar_Employee"
        break
    }
    "Mexico" {
        $replaceParams = @{
        c = "MX"
        co = "Mexico"
        countrycode = 484
        }
        $ou = "OU=DELIVERY,OU=Mexico,OU=Users,DC=Test,DC=LOCAL"
        $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "US_Employee"
        break
    }
    "Romania" {
        $replaceParams = @{
        c = "RO"
        co = "Romania"
        countrycode = 642
        }
        $ou = "OU=DELIVERY,OU=ROMANIA,OU=Users,DC=Test,DC=LOCAL"
        $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Romania_Employee"
        break
    }
    "San Diego" {
        $replaceParams = @{
        c = "US"
        co = "United States"
        countrycode = 840
        }
        $ou = "OU=DELIVERY,OU=USA,OU=Users,DC=Test,DC=LOCAL"
       $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "US_Employee"
        break
    }
    "Argentina" {
        $replaceParams = @{
        c = "AR"
        co = "Argentina"
        countrycode = 32
        }
        $ou = "OU=DELIVERY,OU=USA,OU=Users,DC=Test,DC=LOCAL"
        $City = "City"
           $zipcode = "Zipcode"
           $Company = "CodeOpsHub"
           $State = "State"
           $StreetAddress = "Street Address"
           $telephone = "Telephone number"
           $group = "Argentina_Employee"
        break
    }

}

try {
    # Check if the user already exists
    if (Get-ADUser -Filter {SamAccountName -eq $username}) {
        # Show a message box indicating that the user already exists
        [System.Windows.MessageBox]::Show("User $username already exists.")
        return
    }

    # Create the user in Active Directory
    #$newUser = New-ADUser -Name "$firstname $lastname" -SamAccountName $username -AccountPassword (ConvertTo-SecureString $password -AsPlainText -Force) -GivenName $firstname -Surname $lastname -EmailAddress $email -Enabled $true -Country $country -Path $ou

    New-ADUser -SamAccountName $username -Name "$firstname $lastname"  -GivenName $firstname -Surname $lastname -Initials $initials -Enabled $True -DisplayName $displayname -Path $OU -City $city -PostalCode $zipcode -Country $country -Company $company -State $state -StreetAddress $streetaddress -OfficePhone $telephone -EmailAddress $email -Title $jobtitle -Department $department -Office $company -Manager $manager -AccountPassword (ConvertTo-secureString $password -AsPlainText -Force) -ChangePasswordAtLogon $changePassword

    Set-ADUser -Identity $username -Replace $replaceParams -add @{ProxyAddresses= "SMTP:"+$email -split ","}
    Set-ADUser -UserPrincipalName $username@qualitestgroup.com -Identity $username
    Add-ADGroupMember -Identity "Global_Radius_Group" -Members $username
    Add-ADGroupMember -Identity $group -Members $username


function global:notNullOrEmpty([object]$obj) {
    return ($obj -ne $null -and $obj -ne '')
}

if (notNullOrEmpty $telephone) {

    Set-ADUser $username -Add @{telephonenumber=$telephone}
}


    

    # Show a message box to confirm the user was created
    [System.Windows.MessageBox]::Show("User $username created in $location OU")
}
catch {
    # Show a message box indicating that an error occurred
    [System.Windows.MessageBox]::Show("An error occurred while creating the user account. Error details: $_")
}


# Clear input boxes
$UsernameTextBox.Text = ""
$PasswordBox.Password = $null
$FirstNameTextBox.Text = ""
$LastNameTextBox.Text = ""
$EmailTextBox.Text = ""
$ReportingManagerTextBox.Text = ""
$JobTitleTextBox.Text = ""
$DisplayNameTextBox.Text = ""
$LocationComboBox.SelectedIndex = -1
$ChangePasswordCheckBox.IsChecked = $false
})

$window.ShowDialog()
```

---