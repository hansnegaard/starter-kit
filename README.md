# Windows Quick Setup

Three commands, then hand off to Claude.

Open PowerShell: press `Win`, type `powershell`, hit `Enter`.

## 1. Git
```powershell
winget install -e --id Git.Git
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
