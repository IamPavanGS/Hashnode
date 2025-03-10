---
title: "KeyGuardian"
seoTitle: "PowerShell Password Generator and Secure Sharing Tool"
seoDescription: "Generate, share, and secure passwords with ease using our PowerShell GUI tool. Enhance your online security effortlessly."
datePublished: Mon Sep 25 2023 11:08:30 GMT+0000 (Coordinated Universal Time)
cuid: clmyscauj000p09mk4f3k9orl
slug: keyguardian
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695639459533/4cc9efc1-8acf-4083-8835-b97d3b98728b.png
tags: secure-password-sharing, password-management-tool, password-security-solution, powershell-scripting-for-passwords, password-sharing-via-weblink

---

---

## What is KeyGuardian

In the contemporary digital landscape, the act of sharing passwords with end users or colleagues has become an increasingly complex and security-sensitive task. The risk of compromise is ever-present. However, there exists a cutting-edge solution: a tool capable of generating random passwords and facilitating their secure sharing via web links. This tool empowers users with the freedom to set password expiration parameters based on views or days, all while upholding stringent security standards. With this tool, sharing passwords with end users becomes a streamlined and secure process.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695638459348/0e5d9916-9a02-4049-9e29-d043973ec8bc.gif align="center")

---

### The application operates in a straightforward yet highly effective manner. Here's a step-by-step breakdown of how it works:

### ***First Look at the application***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695636390220/b2f6fdf5-cae6-4a3f-a7c7-71df89c4cd94.png align="center")

**Password Generation**: The user initiates the process by accessing the application's interface. They can specify their password requirements, such as length, complexity, and any special characters they want to include. Alternatively, the application can generate a completely random password for them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695637046107/9f399784-791b-4add-8b44-d8bd05b452a6.png align="center")

**Setting Expiration Rules**: *The user can configure the parameters for the shared password. They can choose to set an expiration date, after which the link becomes inactive. Alternatively, they can opt for a view-based expiration, where the link becomes invalid after a specified number of views. This adds an extra layer of security by limiting access to the password.*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695637238271/cb9093c0-3458-49a0-8a20-995b8c65126d.png align="center")

**Creating a Shareable Link**: After the Push password button is clicked the application generates a unique web link that corresponds to the password. This link is what the user will share with the intended recipient(s). The link is typically time-limited and/or view-limited, depending on the user's preferences.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695637409659/1644b99f-10a8-49ac-ab95-09b5cf10fb57.png align="center")

**Sharing the Link**: With the web link ready, the user can easily share it with their intended recipient(s) through various communication channels, such as email, messaging apps, or even through the application itself. The recipient(s) receive the link and can access the password.

**Recipient Access**: When the recipient clicks on the shared link, they are directed to a secure web page hosted by the application. Here, they can view the password, provided it hasn't expired based on the rules set by the sender.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695637504956/19a8bf26-abe6-430c-a67c-75e01332aed9.png align="center")

**Password Expiry**: As per the rules set by the sender, the password link will eventually expire, either after a specific period or after a certain number of views. Once expired, the link becomes useless, adding an extra layer of security to the shared password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695637541370/25cf1add-3419-40c6-a56e-629f2f15e4ae.png align="center")

---

### Complied .exe application can be found at the below link:

[https://github.com/IamPavanGS/KeyGuardian/blob/main/KeyGuardian.exe](https://github.com/IamPavanGS/KeyGuardian/blob/main/KeyGuardian.exe)

### Source Code:

```powershell

try {

[void][System.Reflection.Assembly]::LoadWithPartialName('presentationframework')

function TextBox_TextChanged {
try{
    $value = [int]$Length_txt_box.Text  # Convert the text to an integer (assuming it's a valid number)

    # Ensure the value is within the slider's range (0 to 100)
    if ($value -lt 0) {
        $value = 0  # Set the value to the minimum (0) if it's less than 0
    }
    elseif ($value -gt 100) {
        $value = 100  # Set the value to the maximum (100) if it's greater than 100
    }

    # Update the text box with the corrected value
    $Length_txt_box.Text = $value

    # Update the slider's value
    $Slide.Value = $value
    }
        catch {
            $output_box.Text = "Error in TextBox_TextChanged: $_"
        }
}

$input = @’
<Window x:Name="Pass_push"  x:Class="WpfApp2.MainWindow"
         xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp1"
        mc:Ignorable="d"
        Title="KeyGuardian" Height="644" Width="744" WindowStyle="ThreeDBorderWindow" BorderBrush="#FF00EFFF" WindowStartupLocation="CenterScreen" ResizeMode="CanMinimize">
    <Grid>
        <Grid.FocusVisualStyle>
            <Style />
        </Grid.FocusVisualStyle>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="13*"/>
            <ColumnDefinition Width="7*"/>
        </Grid.ColumnDefinitions>
        <Slider x:Name="Slide" HorizontalAlignment="Left" Margin="230,110,0,0" VerticalAlignment="Top" Width="365" Height="22" Grid.ColumnSpan="2" Maximum="100" ToolTip="increase to change the password length"/>
        <Label x:Name="Length_txt" Content="Length:" HorizontalAlignment="Left" Margin="33,103,0,0" VerticalAlignment="Top" Width="80" Background="White" FontWeight="Bold" FontSize="16"/>
        <TextBox x:Name="Length_txt_box" HorizontalAlignment="Left" Margin="138,108,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47" Height="22" Grid.Column="1" FontSize="16" Text="12" ToolTip="Enter the number to increase the password length"/>
        <TextBlock Grid.Column="1" HorizontalAlignment="Left" Margin="192,108,0,0" TextWrapping="Wrap" Text="/100" VerticalAlignment="Top" Width="40" Height="31" FontSize="16"/>
        <Label x:Name="options_txt" Content="Options:" HorizontalAlignment="Left" Margin="33,163,0,0" VerticalAlignment="Top" Width="80" Background="White" FontWeight="Bold" FontSize="16"/>
        <CheckBox x:Name="Uppercase_checkbox" Content="A-Z" HorizontalAlignment="Left" Margin="230,173,0,0" VerticalAlignment="Top" FontWeight="Bold" Width="50" IsChecked="True"/>
        <CheckBox x:Name="numeric_checkbox" Content="0-9" HorizontalAlignment="Left" Margin="230,202,0,0" VerticalAlignment="Top" FontWeight="Bold" Width="50" IsChecked="True"/>
        <CheckBox x:Name="lowercase_checkbox" Content="a-z" HorizontalAlignment="Left" Margin="230,231,0,0" VerticalAlignment="Top" FontWeight="Bold" Width="44" IsChecked="True"/>
        <CheckBox x:Name="specialcase_checkbox" Content="!@#$%&amp;" HorizontalAlignment="Left" Margin="230,260,0,0" VerticalAlignment="Top" FontWeight="Bold" Width="87" IsChecked="True"/>
        <Label x:Name="password_txt" Content="Password:" HorizontalAlignment="Left" Margin="33,297,0,0" VerticalAlignment="Top" Width="89" Background="White" FontWeight="Bold" FontSize="16"/>
        <TextBox x:Name="password_textbox" HorizontalAlignment="Left" Margin="230,299,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="389" Grid.ColumnSpan="2" Height="31" FontSize="14"/>
        <Label x:Name="password_txt_Copy" Content="Password Link:" HorizontalAlignment="Left" Margin="33,357,0,0" VerticalAlignment="Top" Width="126" Background="White" FontWeight="Bold" FontSize="16"/>
        <TextBox x:Name="password_link_textbox" HorizontalAlignment="Left" Margin="230,357,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="389" Grid.ColumnSpan="2" Height="31" FontSize="14"/>
        <Button x:Name="pwd_push_btn" Content="Push Password" HorizontalAlignment="Left" Margin="206,471,0,0" VerticalAlignment="Top" RenderTransformOrigin="0.816,0.289" Height="28" Width="99" FontWeight="Bold">
            <Button.Effect>
                <DropShadowEffect/>
            </Button.Effect>
        </Button>
        <Button x:Name="gen_pwd_btn" Content="Generate Password" HorizontalAlignment="Left" Margin="346,471,0,0" VerticalAlignment="Top" RenderTransformOrigin="0.816,0.289" Height="28" Width="119" FontWeight="Bold">
            <Button.Effect>
                <DropShadowEffect/>
            </Button.Effect>
        </Button>
        <Button x:Name="resetform_btn" Content="Reset Form" HorizontalAlignment="Left" Margin="24,471,0,0" VerticalAlignment="Top" RenderTransformOrigin="0.816,0.289" Height="28" Width="103" FontWeight="Bold" Grid.Column="1">
            <Button.Effect>
                <DropShadowEffect/>
            </Button.Effect>
        </Button>
        <RichTextBox x:Name="output_box" Grid.ColumnSpan="2" Margin="10,556,10,10" FontSize="10">
            <FlowDocument>
                <Paragraph>
                    <Run Text=""/>
                </Paragraph>
            </FlowDocument>
        </RichTextBox>
          <Label Content="KeyGuardian" HorizontalAlignment="Left" Margin="310,26,0,0" VerticalAlignment="Top" Width="214" Height="61" Foreground="#FFC7D7E2" FontSize="36" Grid.ColumnSpan="2"/>
        <Label x:Name="push_option_textbox" Content="Password push option:" HorizontalAlignment="Left" Margin="33,411,0,0" VerticalAlignment="Top" Width="184" Background="White" FontWeight="Bold" FontSize="16"/>
        <TextBox x:Name="expiryafterdays_txtbox" HorizontalAlignment="Left" Margin="334,416,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47" Height="22" FontSize="16" Text="1" ToolTip=""/>
        <TextBox x:Name="expiryafterviews_txtbox" HorizontalAlignment="Left" Margin="88,416,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47" Height="22" FontSize="16" Text="2" Grid.Column="1"/>
        <TextBlock x:Name="expiryafterdays_lbl" HorizontalAlignment="Left" Margin="242,419,0,0" TextWrapping="Wrap" Text="Expiry after days:" VerticalAlignment="Top" FontStyle="Italic" ToolTip="The password will be expired in the weblink in the provided days"/>
        <TextBlock x:Name="expiryafterview_lbl" HorizontalAlignment="Left" Margin="472,419,0,0" TextWrapping="Wrap" Text="Expiry after views:" VerticalAlignment="Top" FontStyle="Italic" ToolTip="The password will be expired in the weblink in the provided views" Grid.ColumnSpan="2" Width="93"/>
        <TextBlock x:Name="website_lbl" Grid.Column="1" HorizontalAlignment="Left" Margin="198,10,0,0" TextWrapping="Wrap" Text="Website" VerticalAlignment="Top" TextDecorations="Underline" FontFamily="Bodoni MT" FontSize="14" Cursor="Hand"/>
        <TextBlock x:Name="Github_lbl" Grid.Column="1" HorizontalAlignment="Left" Margin="126,10,0,0" TextWrapping="Wrap" Text="GitHub" VerticalAlignment="Top" TextDecorations="Underline" FontSize="14" FontFamily="Bodoni MT" Cursor="Hand"/>
        <Image x:Name="website_icon" Grid.Column="1" HorizontalAlignment="Left" Margin="180,10,0,0" VerticalAlignment="Top" Width="16" Height="16" Cursor="Hand"/>
        <Image x:Name="github_icon" Grid.Column="1" HorizontalAlignment="Left" Margin="108,10,0,0" VerticalAlignment="Top" Width="16" Height="16" Cursor="Hand"/>
        <Image x:Name="Title_image" HorizontalAlignment="Left" Margin="262,22,0,0" VerticalAlignment="Top" Width="79" Height="56"/>
        <Menu Margin="0,0,429,586" Background="White">
    <MenuItem x:Name="File_menu" Header="File">
        <MenuItem x:Name="Export_menuitem" Header="Export Logs" Background="White"/>
        <MenuItem x:Name="Exit_menuitem" Header="Exit" Background="White"/>
    </MenuItem>
</Menu>
<Menu Margin="33,0,371,586" Background="White">
    <MenuItem x:Name="Help_Menu" Header="Help">
        <MenuItem x:Name="About_menuitem" Header="About" Background="White"/>
    </MenuItem>
</Menu>
    </Grid>
</Window>
'@

$input = $input -replace '^<Window.*', '<Window' -replace 'mc:Ignorable="d"','' -replace "x:N",'N' 
[xml]$xaml = $input
$xmlreader=(New-Object System.Xml.XmlNodeReader $xaml)
$xamlForm=[Windows.Markup.XamlReader]::Load( $xmlreader )

$xaml.SelectNodes("//*[@Name]") | ForEach-Object -Process {
    Set-Variable -Name ($_.Name) -Value $xamlForm.FindName($_.Name)
    }

$Slide.Value = 12 

$logFilePath = "C:\Users\Public\Keyguardian_log.txt"

# Function to write a log entry
function Write-LogEntry {
    param (
        [string]$message
    )
    $timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    $logEntry = "$timestamp - $message"
    $logEntry | Out-File -Append -FilePath $logFilePath
}


function Export-Log {
    # Prompt the user to select a location to save the log file
    $saveFileDialog = New-Object Microsoft.Win32.SaveFileDialog
    $saveFileDialog.Filter = "Text Files (*.txt)|*.txt"
    $saveFileDialog.Title = "Export Log File"
    
    if ($saveFileDialog.ShowDialog() -eq $true) {
        $destinationPath = $saveFileDialog.FileName
        Copy-Item -Path $logFilePath -Destination $destinationPath
    }
}


$Export_menuitem.add_Click({
    Export-Log
    [System.Windows.MessageBox]::Show("Log exported successfully!", "Export Logs", [System.Windows.MessageBoxButton]::OK, [System.Windows.MessageBoxImage]::Information)
})

$Exit_menuitem.add_Click({

  $xamlForm.Close()


})

$About_menuitem.add_Click({

[System.Windows.MessageBox]::Show("Version: 1.0.0 `nAuthor : Pavan G S `nBuild Date: 22nd Sep 2023", "Information", [System.Windows.MessageBoxButton]::OK, [System.Windows.MessageBoxImage]::Information)

# After displaying the message box, get its window handle
$mbWindow = [System.Windows.Interop.HwndSource]::FromHwnd((Get-Process -Id $pid).MainWindowHandle)

# Calculate the screen dimensions
$screen = [System.Windows.Forms.Screen]::PrimaryScreen.Bounds

# Calculate the position for the message box to be in the center
$left = [math]::Round(($screen.Width - $mbWindow.RootVisual.ActualWidth) / 2)
$top = [math]::Round(($screen.Height - $mbWindow.RootVisual.ActualHeight) / 2)

})

Write-LogEntry "Application started"


# Define your base64-encoded icon data here
$base64IconData = "iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAACXBIWXMAAAsTAAALEwEAmpwYAAAD+klEQVR4nO1X3WtUVxDf+JSk3XtXRUxK4ydCa6xRY61gk1WDu+w9M+fsChdCqfZB/KSl2i+qIkJSrC8FEQs2DbQvhT6ZflAolCAUDfUjK3vvbqz1oU/+HT+Z3bN6Xfa6iTGFggMH7jlz5sxv5syZmZtIvKD/G/k+OpTCGiJs0Rq7ZMi3rAlvgd
SiLZvFKiIc0xoTRKg0G8yYUApHPQ8rRea5qE6nkfI8HGPGTWZME+EbpfCx1thqDFbJkG9ZE57skb1a44jIzks5EVYQYZwZd4nwuVhmDA4zY8rz0FXfl82iW9aMwQHZw4xTIqMUvjUGPc+snBm/MOM6M3acPYtFvo8umWuNEZnX98o3Ec4RYXJoCEtlbgwGrOzPmcwcQaTTSIk7iXBNa6yvrzNjt1jGjN5GGa2xmQh/E+HtyP5e8Yx4cQ7XgTYJJOvC
gSjHGHzBjN99Hy83ShmDFDOuMuOzhvUBASZXN6vANKYa7beYcTLqZnlizPhNXB0HnAgXiXAlnUZ7fVXOUAonmXGj9jpaEFE14iXaR4jwfX0w410iFAsFfMKMsSjP8sfEeiLczuerex/xcjmMiqx49qnKfR8dWuMna8lH0UNs9M8ohf1xALTGfskHSuFQA/8EM75mxhUidMYCULUMV8nnkWvimS0WQF+cPDM2WgDbGnnGwCNCWXTEAsjlsFUOMAZvND
l8uwDI5/F6KwOIkG7C67Pg+mMB6Fpel5S6uglv0AJY2yKAxYCdTQxYzdyc94iEOR8ANnOKkqFGnpxpPRAPQCn0WwAbn+UKMhksyWlc3nkAO54SH/0LFoTuv0gtnsYFN8QfbgkHl5UfJyw50wKID0K/lmwmmHFJ67k/w95L2OcG+McNcN4NcM+5g/FkBeuAana9KGe37BmUwlFJGp73ZCLyvNaJ6LVxHHQCVBaH6EmVMOiUMOkEKC7/E8NK4wciHEm0
Iq9WTm8S4XSzVKwUvoyTdUJkBUDnDLpl3n6/CuQrN8D9rkmcf/MclrYEkKjl9MNSQCTyoxxmjMYVoyiAjmm8Ul/rfoBOiQcnwD23jE2zLsfMuKw1rkVLr+SJuHJsAWScAOUqAGDRq1PoSBXxnhvilhPgans4h77AGPRIM2EbkEG5juFhLJceQSmMRq+nAUCYCtGXDDHihJhIlvChU8b7ySLWzVp5FIS0VbbROC2NqX0N16MtWZ2cO9jmhLjrlDBlrf
7ODfBXe2UWZbhFdyRKb9gyPVZvSiW77d2LlYUCNsg7VwWcWfsjPkiW8OmSIta7Ada4AW4nSziemB+hTV6H7ZSkpJYb2vEZ+/3rE1kUaEuF2OeU8E5ioX5MmLFba7wl3tizBy89N0UvKPEf0UOHIk3UqkXQEAAAAABJRU5ErkJggg=="

# Convert the base64 data to an ImageSource
$iconImageSource = [System.Windows.Media.Imaging.BitmapImage]::new()
$iconImageSource.BeginInit()
$iconImageSource.StreamSource = [System.IO.MemoryStream]::new([System.Convert]::FromBase64String($base64IconData))
$iconImageSource.EndInit()

# Set the Image control's Source
$website_icon.Source = $iconImageSource

$base64IconData2 = "iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAACXBIWXMAAAsTAAALEwEAmpwYAAAE5ElEQVR4nO2VbUxTdxTGK7IPi4ruLcuyZGPTUmQgxmJUTAo6BRVFIiJDfBlOivgyMEolYOwYbswPikLdouwDxCiLkdKXS21vC7eF3uqEuMnikGWZUepiZvbBuX1Yluy33M0OxqxStmRZ4pP8c+9z7nnOc+65//yvSvUY/yfEbkMTW8q+2FI8sa
UMxJby4/018PJ23LGlGF7ZQdy/bqzRk6LR06nRczNOT2OcnmVxeuJnbWCSspT7uGKWa0owaUoY0pTgiS9F+4+NtXqeSCzGlFjMUJKerXl5THyUJs1IdNJWihO3EkwqpkHh4zJPKuWplCK6tEVYU7cwJVK9otEWYdMW4UnezLSI33zBZroWbKJBZSRKNV4YiVqwmcbUTXjS0iKYxKJCTOkbsBqNROWdZWK5zMUyGX9ZgPLdAZ4MK4QJZRfILwvQUSYz
uMvPdKVGeiG2RYUcG5P5kjdIyShgKPv+2Cv8pBhkru71k2HwYzfI3DT4aTfIfG3wc7fCz08GP8EKGdEg02uQ+azCT75B5pN9MjuUGssKickoIJhZyJxHNrByHZ2r8nkrxKt6WLW/B0uIV/vQVfvJr+wmzniRmD0uJhl7eKnKR9b+btYa+eOTVXdTVd3DwZBuVT76lfm4H2qel4cmN5ebI3f7QT8ptd30qyJEbTdNNT52hriyB3JzCa5ZgzqsqCCHyv
U5NIyMHfLSeMjLqUgb+MDHzkM+LgETQrH1ORwvyKEirOjN1biLclge4o1unqmX+P6wk6cjbUAxru/i8hGJJaHYlmyyilYjhhXpV/JVSdbwiEydrDjeiVM1Thzv4l1TJzUhvi0bjT6La2EFby/n3vY0Jod4k5v8Jjet423gpIfyJjdHQ1yprXiEFexZyg8V2cOnXrOLjBY3rvE20CJS2yJyIMR3LSNm71LuhhVULWaw8vXhv9mp87zQ6uSOcpiMp4Ez
TlynneSE+P4lzKxazEBYQc0i3DWLhzehArOTC+bz5EVqfk5EbXbyncNBzJ/108mqSX/IRN/TYXhfh2lkTBDQ2R18a3Uwa6zmDgfP2c9zWXCwe2S8TsdHdTr2hBXWp6I5vJAhYxrRLgGdS6DJ5WCtKLDO1cEdUcAk2smUbDz7ANOY3zUd1Lg6uK1cRz5Xah5ZSPCo7iEHkYLGeXhM8yiWBDZKdn6VBH6W7Bz0WHnea8cgCXR7BZDswwZegTVeO79Idq
4quZKNeNUomOZT0jh/DBu6aR7ak3MJfpzKFNnGRtnGbdnKUMBKuXSWyUosYCUwWidbORKwUvugmie0TD0xl1sn5zJbNRY0z6GhWYvNqCKq14Knz8KHvVZ8vVbu9Vm5dslG7mjNJQvZfZbhn1YISo0WLUKzlnrVWCGlEX0mGc+Z2TT2tTL9Sjs3+i3Y+i1UXmmn7vP2vzfwhZmMK5a/jlgxb52NqTUZUampigTtyUxrS8TTloQ9UMKLA2a2DLZRN2jG
f82McXT+wDkyB83Dx/ZZLVPNSQjmJESllmo8kNKItidwTEggKCSgV/j1Nt5R1ujcb86Reb0Np5IjJFAivMYtIYH6iN/8QfDEM0fU4BbjCcor6O0v57SoZqaUwGRlKfd9GznwaR43lBxRg+hKGOOGiwTeV1H71FT41Ii+GQz4ZnDv/vrSq8blU7NXms6MiIo+huo/xm/5lRjIlLv2EgAAAABJRU5ErkJggg=="


$iconImageSource2 = [System.Windows.Media.Imaging.BitmapImage]::new()
$iconImageSource2.BeginInit()
$iconImageSource2.StreamSource = [System.IO.MemoryStream]::new([System.Convert]::FromBase64String($base64IconData2))
$iconImageSource2.EndInit()

$github_icon.source = $iconImageSource2

$base64IconData3 = "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"

# Convert the base64 data to an ImageSource
$iconImageSource3 = [System.Windows.Media.Imaging.BitmapImage]::new()
$iconImageSource3.BeginInit()
$iconImageSource3.StreamSource = [System.IO.MemoryStream]::new([System.Convert]::FromBase64String($base64IconData3))
$iconImageSource3.EndInit()

# Set the Image control's Source
$Title_image.Source = $iconImageSource3



$Slide.add_ValueChanged({
    $Length_txt_box.Text = [math]::Round($Slide.Value)  
})


$website_lbl.add_MouseLeftButtonUp({
   
    $url = "http://www.pavansridhar.co.in"

    
    Start-Process $url
    Write-LogEntry "Website has been opened"
})


$Github_lbl.add_MouseLeftButtonUp({
   
    $url = "https://github.com/IamPavanGS"

 
    Start-Process $url
     Write-LogEntry "Github has been opened"
})


$website_icon.add_MouseLeftButtonUp({
   
    $url = "http://www.pavansridhar.co.in"

  
    Start-Process $url
})


$github_icon.add_MouseLeftButtonUp({
   
    $url = "https://github.com/IamPavanGS"

  
    Start-Process $url
})




$Length_txt_box.add_TextChanged({
    TextBox_TextChanged
})


function ResetFormButton_Click {
    # Clear text in text boxes
    $Length_txt_box.Text = "12"
    $password_textbox.Text = ""
    $password_link_textbox.Text = ""
    $expiryafterdays_txtbox.Text = "1"
    $expiryafterviews_txtbox.Text = "2"
    # Uncheck checkboxes
    $Uppercase_checkbox.IsChecked = $false
    $numeric_checkbox.IsChecked = $false
    $lowercase_checkbox.IsChecked = $false
    $specialcase_checkbox.IsChecked = $false
    #clear the richtextbox
    $output_box.Document.Blocks.Clear()
}



function Test-InternetConnection {
    try {
        $null = Test-Connection -ComputerName "www.google.com" -Count 1 -ErrorAction Stop
        return $true
    } catch {
        return $false
    }
}


$run = New-Object Windows.Documents.Run
if (Test-InternetConnection) {
    $run.Text = "Connected to Internet"
    $run.Foreground = [System.Windows.Media.Brushes]::Green
} else {
    $run.Text = "No Internet Connection"
    $run.Foreground = [System.Windows.Media.Brushes]::Red
}


$paragraph = $output_box.Document.Blocks.FirstBlock
$paragraph.Inlines.Clear()
$paragraph.Inlines.Add($run)

function Get-RandomPassword
{
    #Script by: https://arminreiter.com/2021/07/3-ways-to-generate-passwords-in-powershell/
    param (
        [Parameter(Mandatory)]
        [ValidateRange(6, [int]::MaxValue)]
        [int] $length,
        [int] $upper = 0,
        [int] $lower = 0,
        [int] $numeric = 0,
        [int] $special = 0
    )
    if ($upper + $lower + $numeric + $special -gt $length)
    {
        throw "number of upper/lower/numeric/special char must be lower or equal to length"
    }
    $uCharSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    $lCharSet = "abcdefghijklmnopqrstuvwxyz"
    $nCharSet = "0123456789"
    $sCharSet = "/*-+,!?=()@;:._"
    $charSet = ""
    if ($upper -gt 0) { $charSet += $uCharSet }
    if ($lower -gt 0) { $charSet += $lCharSet }
    if ($numeric -gt 0) { $charSet += $nCharSet }
    if ($special -gt 0) { $charSet += $sCharSet }
    
    $charSet = $charSet.ToCharArray()
    $rng = New-Object System.Security.Cryptography.RNGCryptoServiceProvider
    $bytes = New-Object byte[]($length)
    $rng.GetBytes($bytes)
 
    $result = New-Object char[]($length)
    for ($i = 0 ; $i -lt $length ; $i++)
    {
        $result[$i] = $charSet[$bytes[$i] % $charSet.Length]
    }
    $password = (-join $result)
    $valid = $true
    if ($upper -gt ($password.ToCharArray() | Where-Object { $_ -cin $uCharSet.ToCharArray() }).Count) { $valid = $false }
    if ($lower -gt ($password.ToCharArray() | Where-Object { $_ -cin $lCharSet.ToCharArray() }).Count) { $valid = $false }
    if ($numeric -gt ($password.ToCharArray() | Where-Object { $_ -cin $nCharSet.ToCharArray() }).Count) { $valid = $false }
    if ($special -gt ($password.ToCharArray() | Where-Object { $_ -cin $sCharSet.ToCharArray() }).Count) { $valid = $false }
 
    if (!$valid)
    {
        $password = Get-RandomPassword $length $upper $lower $numeric $special
    }
    return $password
}

function GeneratePasswordButton_Click {
    # Check if any checkboxes are selected
    $checkboxesChecked = $Uppercase_checkbox.IsChecked -or $lowercase_checkbox.IsChecked -or $numeric_checkbox.IsChecked -or $specialcase_checkbox.IsChecked
    
    if ($checkboxesChecked) {
        $password = Get-RandomPassword -length $Length_txt_box.Text -upper ($Uppercase_checkbox.IsChecked -eq $true) -lower ($lowercase_checkbox.IsChecked -eq $true) -numeric ($numeric_checkbox.IsChecked -eq $true) -special ($specialcase_checkbox.IsChecked -eq $true)
        $password_textbox.Text = $password
    } else {
        # Display a message box if no checkboxes are selected
        [System.Windows.MessageBox]::Show("Kindly select at least one option (A-Z, a-z, 0-9, or special characters).", "No Options Selected", [System.Windows.MessageBoxButton]::OK, [System.Windows.MessageBoxImage]::Warning)
    }
}


$password_link_textbox.IsReadOnly = $true

$resetform_btn.add_Click({
    ResetFormButton_Click
})


$gen_pwd_btn.add_Click({
    GeneratePasswordButton_Click
})


function Submit-Password
{
    $url = "https://pwpush.com/p.json"
    $body = @{
        password = @{
            "payload" = $password_textbox.Text
            "expire_after_days" = $expiryafterdays_txtbox.Text
            "expire_after_views" = $expiryafterviews_txtbox.Text
            "note" = ""
            "retrieval_step" = "true"
            "deletable_by_viewer" = "false"
        }
    } | ConvertTo-Json

    $response = Invoke-RestMethod -Method Post -Uri $url -Body $body -ContentType "application/json"
    return "https://pwpush.com/p/$($response.url_token)" 
}

function PushPasswordButton_Click {

    if($password_textbox.Text -eq ""){

     [System.Windows.MessageBox]::Show("Kindly generate the password by clicking on Generate password button).", "No password generated", [System.Windows.MessageBoxButton]::OK, [System.Windows.MessageBoxImage]::Warning)
    
    }else{

    $passwordLink = Submit-Password
    $password_link_textbox.Text = $passwordLink

    }
}

$pwd_push_btn.add_Click({
    try {
            PushPasswordButton_Click
        }
        catch {
            $output_box.Text = "Error in PushPasswordButton_Click: $_"
        }
})

$xamlForm.ShowDialog() | out-null

}
catch {
    $output_box.Text = "Error in the main code block: $_"
}
```

For more information about the Password Pusher web service, visit this link: [https://pwpush.com/](https://pwpush.com/)

---