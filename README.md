# ps1-reference

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
    $env:Path = [string]::Join(";", $list)    
}
```
