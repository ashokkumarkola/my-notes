# Windows Cheat Sheet

CMD = `cmd.exe`. PowerShell = `pwsh` / `powershell`. Prefer PowerShell.

## Files (CMD)

```bat
cd C:\path
dir /a
mkdir folder
copy a.txt b.txt
xcopy src dst /E /I
move a.txt dir\
ren old.txt new.txt
del file.txt
rmdir /S /Q folder
type file.txt
cls
```

## Files (PowerShell)

```powershell
Get-ChildItem -Force              # ls
Set-Location C:\path              # cd
New-Item -ItemType File a.txt
New-Item -ItemType Directory dir
Copy-Item src dst -Recurse
Move-Item a.txt dir\
Rename-Item old.txt new.txt
Remove-Item dir -Recurse -Force
Get-Content log.txt -Tail 20 -Wait   # tail -f
Select-String -Path *.txt -Pattern "error"
```

## System

```bat
systeminfo
hostname
whoami
tasklist
taskkill /IM notepad.exe /F
taskkill /PID 1234 /F
shutdown /r /t 0          :: restart now
shutdown /s /t 0          :: shutdown now
sfc /scannow              :: repair system files (admin)
```

## Network

```bat
ipconfig
ipconfig /all
ipconfig /flushdns
ping google.com
tracert google.com
nslookup google.com
netstat -ano | findstr :8000      :: who uses port
curl -I https://example.com
```

## Packages (winget)

```powershell
winget search git
winget install --id Git.Git -e
winget upgrade --all
winget uninstall --id Git.Git
winget list
```

## Environment

```powershell
$env:Path -split ';'                 # show PATH
$env:MY_VAR = "1"                    # session only
[Environment]::SetEnvironmentVariable("MY_VAR","1","User")   # persist
```

```bat
echo %PATH%
set MY_VAR=1                         :: session only
setx MY_VAR 1                        :: persist (new terminals)
```

## PowerShell basics

```powershell
Get-Help Get-ChildItem -Examples
Get-Command *process*
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned   # allow local scripts
```

## Shortcuts

| Key | Action |
|---|---|
| `Win+R` | Run dialog (`cmd`, `powershell`) |
| `Win+X` | Power menu (Terminal admin) |
| `Ctrl+Shift+Esc` | Task Manager |
| `Win+E` | File Explorer |
| `Win+V` | Clipboard history |
| `Win+Shift+S` | Screenshot |
