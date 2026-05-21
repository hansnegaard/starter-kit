# Dev Machine Setup

Set up a new machine for development. Follow the section for your OS top to bottom. **Windows is first; macOS is at the bottom.**

You only strictly need steps 1–3 (Git, Node, Claude Code) to get going — once Claude Code is running you can ask it to do the rest. The remaining steps install the standard toolset.

---

## Windows

Open PowerShell: press `Win`, type `powershell`, hit `Enter`.

### 1. Git
```powershell
winget install -e --id Git.Git
```
Close and reopen PowerShell.

### 2. Node (portable, no admin)
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
Close and reopen PowerShell. (Global npm packages land in `%USERPROFILE%\node`, so `npm install -g` works without admin and is already on PATH.)

### 3. Claude Code
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
npm install -g @anthropic-ai/claude-code
claude
```
(The first line lets PowerShell run `npm.ps1` — fixes "running scripts is disabled on this system". Scoped to your user, no admin.)

### 4. Configure Claude Code defaults (optional)
```powershell
node -e "const fs=require('fs'),p=require('os').homedir()+'/.claude/settings.json';const s=fs.existsSync(p)?JSON.parse(fs.readFileSync(p,'utf8')):{};s.permissions=Object.assign(s.permissions||{},{defaultMode:'bypassPermissions'});s.effortLevel='xhigh';fs.writeFileSync(p,JSON.stringify(s,null,2))"
```
Sets bypass-permissions mode and max effort level globally.

### 5. GitHub CLI
```powershell
winget install -e --id GitHub.cli --scope user
gh auth login
```
Follow the prompts: GitHub.com → HTTPS → "Login with a web browser".

### 6. VS Code
```powershell
winget install -e --id Microsoft.VisualStudioCode --scope user
```

### 7. Slack
```powershell
winget install -e --id SlackTechnologies.Slack --scope user
```

### 8. oh-my-claudecode
Inside Claude Code, run:
```
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc
```

### 9. Star the repo
```powershell
gh api --method PUT /user/starred/hansnegaard/starter-kit
```

---

## macOS

Open Terminal: press `Cmd`+`Space`, type `terminal`, hit `Enter`.

### 1. Homebrew (includes Git)
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Allow Xcode Command Line Tools when prompted. After it finishes, follow the "Next steps" Homebrew prints to add `brew` to your `PATH`, then close and reopen Terminal.

### 2. Node
```bash
brew install node
```

### 3. Claude Code
```bash
npm install -g @anthropic-ai/claude-code
claude
```

### 4. Configure Claude Code defaults (optional)
```bash
node -e "const fs=require('fs'),p=require('os').homedir()+'/.claude/settings.json';const s=fs.existsSync(p)?JSON.parse(fs.readFileSync(p,'utf8')):{};s.permissions=Object.assign(s.permissions||{},{defaultMode:'bypassPermissions'});s.effortLevel='xhigh';fs.writeFileSync(p,JSON.stringify(s,null,2))"
```
Sets bypass-permissions mode and max effort level globally.

### 5. GitHub CLI
```bash
brew install gh
gh auth login
```
Follow the prompts: GitHub.com → HTTPS → "Login with a web browser".

### 6. VS Code
```bash
brew install --cask visual-studio-code
```

### 7. Slack
```bash
brew install --cask slack
```

### 8. oh-my-claudecode
Inside Claude Code, run:
```
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc
```

### 9. Star the repo
```bash
gh api --method PUT /user/starred/hansnegaard/starter-kit
```
