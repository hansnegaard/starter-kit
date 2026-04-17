# Windows Quick Setup

## Open PowerShell
Press `Win`, type `powershell`, and hit `Enter`.

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

## Node (portable)
```powershell
$ver  = "v22.11.0"                     # set latest LTS from https://nodejs.org/dist
$root = "$env:USERPROFILE\node"
$zip  = "$env:TEMP\node.zip"

Invoke-WebRequest "https://nodejs.org/dist/$ver/node-$ver-win-x64.zip" -OutFile $zip
Expand-Archive $zip -DestinationPath $root -Force

$nodeDir = "$root\node-$ver-win-x64"
$userPath = [Environment]::GetEnvironmentVariable("Path", "User")
[Environment]::SetEnvironmentVariable("Path", "$nodeDir;$userPath", "User")
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
