# OS Cheat Sheet

Same task across shells.

| Task | Linux (bash) | Windows CMD | PowerShell |
|---|---|---|---|
| Current dir | `pwd` | `cd` | `Get-Location` |
| List files | `ls -la` | `dir` | `Get-ChildItem` (`ls`) |
| Change dir | `cd path` | `cd path` | `cd path` |
| Make dir | `mkdir -p a/b` | `mkdir a\b` | `New-Item -ItemType Directory a\b` |
| Copy | `cp -r src dst` | `xcopy src dst /E /I` | `Copy-Item src dst -Recurse` |
| Move/rename | `mv a b` | `move a b` | `Move-Item a b` |
| Delete file | `rm f` | `del f` | `Remove-Item f` |
| Delete dir | `rm -rf d` | `rmdir /S /Q d` | `Remove-Item d -Recurse -Force` |
| Show file | `cat f` | `type f` | `Get-Content f` |
| Search text | `grep -rn "x" .` | `findstr /S /N "x" *` | `Select-String -Pattern x -Path *` |
| Find file | `find . -name "*.md"` | `dir /S *.md` | `Get-ChildItem -Recurse -Filter *.md` |
| Clear | `clear` | `cls` | `cls` |
| Env var | `echo $HOME` | `echo %USERPROFILE%` | `$env:USERPROFILE` |
| Set env (session) | `export X=1` | `set X=1` | `$env:X = "1"` |
| Command path | `which python` | `where python` | `Get-Command python` |
| Processes | `ps aux` | `tasklist` | `Get-Process` |
| Kill | `kill -9 PID` | `taskkill /PID PID /F` | `Stop-Process -Id PID -Force` |
| IP info | `ip a` | `ipconfig` | `Get-NetIPAddress` |
| Ports | `ss -tulpn` | `netstat -ano` | `Get-NetTCPConnection` |
| Install pkg | `sudo apt install x` | `winget install x` | `winget install x` |
| Path separator | `/` | `\` | `\` (also `/`) |
