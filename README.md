# ps1-reference

Edit the file at `nvim $profile`

Utility function, remove item from `$env:Path`

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

Aliases 
```powershell
Set-Alias -Name gits -Value 'git status'
Set-Alias -Name gitd -Value 'git diff'

Function GitSatatus { & 'git' status }
Function GitDiff { & 'git' diff }

Set-Alias -Name gits -Value GitSatatus
Set-Alias -Name gitd -Value GitSatatus
```

Uunix like tab completion:
```powershell
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
```
