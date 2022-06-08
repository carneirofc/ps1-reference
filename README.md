# ps1-reference

Edit the file at `nvim $profile`

## $env:USERPROFILE
```powershell
# Aliases
Function GitSatatus { & 'git' status @args }
Function GitDiff { & 'git' diff @args }
Function BfgRun { & 'java' -jar (Get-Command bfg.jar).Path @args }

Set-Alias -Name gits -Value GitSatatus
Set-Alias -Name gitd -Value GitDiff
Set-Alias -Name bfg  -Value BfgRun

# Unix-like tab completion
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete

# Links, command line utilities
#
# https://github.com/BurntSushi/ripgrep/releases
# https://github.com/sharkdp/bat/releases
# https://github.com/neovide/neovide
# https://github.com/neovim/neovim

# Messing with the session path
function UpdatePath() {
    $list = New-Object Collections.Generic.List[String]
    $Env:PATH.Split(";") | ForEach-Object {
        if ($_.StartsWith("C:\Program Files (x86)\Microsoft SDKs\TypeScript\1.0")) { return; }
        $list.Add($_);
    }
    $appsPath = $env:USERPROFILE + "\apps"
    $list.Add($appsPath)
    $list.Add("$appsPath\Neovim\bin")
    $list.Add("$appsPath\ripgrep-13.0.0-x86_64-pc-windows-msvc")
    $list.Add("$appsPath\bat-v0.21.0-x86_64-pc-windows-msvc")

    $env:Path = [string]::Join(";", $list)
}
UpdatePath
```

## Utility function, remove item from `$env:Path`

```powershell
function UpdatePath() {

    $list = New-Object Collections.Generic.List[String]
    $Env:PATH.Split(";") | ForEach-Object {
        if ($_ -eq "C:\Program Files (x86)\Microsoft SDKs\TypeScript\1.0") {
            return
        }
        $list.Add($_);
    }
    # Add more things to path
    # $list.Add();
    $env:Path = [string]::Join(";", $list)    
}
```

## Aliases 
```powershell
Set-Alias -Name gits -Value 'git status'
Set-Alias -Name gitd -Value 'git diff'

Function GitSatatus { & 'git' status }
Function GitDiff { & 'git' diff }

Set-Alias -Name gits -Value GitSatatus
Set-Alias -Name gitd -Value GitSatatus
```

## Unix like tab completion:
```powershell
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
```
