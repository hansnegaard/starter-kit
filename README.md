# Windows Quick Setup

## Open PowerShell
Press `Win`, type `powershell`, and hit `Enter`.

## Allow npm scripts to run (one-time)
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
```

## Discord
```powershell
winget install -e --id Discord.Discord
```

## Slack
```powershell
winget install -e --id SlackTechnologies.Slack
```

## Git
```powershell
winget install -e --id Git.Git
```

## GitHub CLI
```powershell
winget install -e --id GitHub.cli
gh auth login
```

## Visual Studio Code
```powershell
winget install -e --id Microsoft.VisualStudioCode
```

## Node (portable, into your user folder)
Works in the current window — no reopen needed.
```powershell
$v="v22.11.0"; iwr "https://nodejs.org/dist/$v/node-$v-win-x64.zip" -OutFile "$env:TEMP\node.zip"; Expand-Archive "$env:TEMP\node.zip" "$env:USERPROFILE" -Force; $nd="$env:USERPROFILE\node-$v-win-x64"; [Environment]::SetEnvironmentVariable("Path","$nd;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$nd;$env:Path"; node -v
```

## Verify (open a new PowerShell)
```powershell
git --version
gh --version
node --version
npm --version
```

## Claude Code
```powershell
npm install -g @anthropic-ai/claude-code
claude
```

## Codex
```powershell
npm install -g @openai/codex
codex
```

## oh-my-claudecode (Claude Code plugin)
Run these inside Claude Code:
```text
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc
```

## oh-my-codex
```powershell
npm install -g oh-my-codex
omcx
```
