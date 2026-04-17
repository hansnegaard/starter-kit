# Windows Quick Setup

Get to Claude in 3 steps. Claude handles the rest.

Open PowerShell: press `Win`, type `powershell`, hit `Enter`.

## 1. Git (portable, no admin)
Required for Claude Code's bash shell.
```powershell
$u=(iwr "https://api.github.com/repos/git-for-windows/git/releases/latest" -UseBasicParsing | ConvertFrom-Json).assets | ?{ $_.name -like "PortableGit-*-64-bit.7z.exe" } | select -First 1 -Expand browser_download_url; iwr $u -OutFile "$env:TEMPpg.exe"; & "$env:TEMPpg.exe" -o"C:UsersPublicGit" -y | Out-Null; $gb="C:UsersPublicGitcmd"; [Environment]::SetEnvironmentVariable("Path","$gb;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$gb;$env:Path"; git --version
```

## 2. Node (portable, no admin)
```powershell
$v="v22.11.0"; iwr "https://nodejs.org/dist/$v/node-$v-win-x64.zip" -OutFile "$env:TEMP
ode.zip"; Expand-Archive "$env:TEMP
ode.zip" "$env:USERPROFILE" -Force; $nd="$env:USERPROFILE
ode-$v-win-x64"; [Environment]::SetEnvironmentVariable("Path","$nd;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$nd;$env:Path"; node -v
```

## 3. Claude Code
```powershell
npm install -g @anthropic-ai/claude-code
[Environment]::SetEnvironmentVariable("CLAUDE_CODE_GIT_BASH_PATH","C:UsersPublicGitinash.exe","User")
$env:CLAUDE_CODE_GIT_BASH_PATH="C:UsersPublicGitinash.exe"
claude
```

---

## Hand off to Claude

Once Claude Code is running, paste this and let it finish the setup:

```
Finish my dev setup. Install and authenticate gh CLI (use device OAuth flow so I don't have to leave the terminal), install VS Code, Discord, and Slack via winget, then install and configure the oh-my-claudecode plugin. Verify everything works when done.
```

Claude will handle authentication, app installs, and plugin setup without you needing to copy-paste anything else.
