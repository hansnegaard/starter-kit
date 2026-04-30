# Windows Quick Setup (No Admin)

Portable install — nothing touches Program Files, no UAC prompts.

Open PowerShell: press `Win`, type `powershell`, hit `Enter`.

## 1. Git (portable)
```powershell
$asset = (Invoke-RestMethod 'https://api.github.com/repos/git-for-windows/git/releases/latest').assets | Where-Object { $_.name -like 'PortableGit-*-64-bit.7z.exe' } | Select-Object -First 1
$dst = "$env:USERPROFILE\git"
Invoke-WebRequest $asset.browser_download_url -OutFile "$env:TEMP\git.7z.exe"
if (Test-Path $dst) { Remove-Item $dst -Recurse -Force }
& "$env:TEMP\git.7z.exe" -y "-o$dst" | Out-Null
[Environment]::SetEnvironmentVariable('Path', "$([Environment]::GetEnvironmentVariable('Path','User'));$dst\cmd", 'User')
$env:Path = "$env:Path;$dst\cmd"
```
Close and reopen PowerShell.

## 2. Node (portable)
```powershell
$v = ((Invoke-RestMethod 'https://nodejs.org/dist/index.json') | Where-Object { $_.lts } | Select-Object -First 1).version
$dst = "$env:USERPROFILE\node"
Invoke-WebRequest "https://nodejs.org/dist/$v/node-$v-win-x64.zip" -OutFile "$env:TEMP\node.zip"
if (Test-Path $dst) { Remove-Item $dst -Recurse -Force }
Expand-Archive "$env:TEMP\node.zip" -DestinationPath $env:USERPROFILE -Force
Move-Item "$env:USERPROFILE\node-$v-win-x64" $dst
[Environment]::SetEnvironmentVariable('Path', "$([Environment]::GetEnvironmentVariable('Path','User'));$dst", 'User')
$env:Path = "$env:Path;$dst"
```
Close and reopen PowerShell.

> Global npm packages land in `%USERPROFILE%\node` (next to `node.exe`), so `npm install -g` works without admin and is already on PATH.

## 3. Claude Code
```powershell
npm install -g @anthropic-ai/claude-code
claude
```

---

## Hand off to Claude

Once Claude is running, paste this single prompt and walk away:

```
Complete my Windows dev setup by following the instructions at https://raw.githubusercontent.com/hansnegaard/starter-kit/main/CLAUDE.md
```
