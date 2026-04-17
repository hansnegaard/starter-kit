# Windows Quick Setup

Three commands, then hand off to Claude.

Open PowerShell: press `Win`, type `powershell`, hit `Enter`.

## 1. Git
```powershell
winget install -e --id Git.Git
```
Close and reopen PowerShell.

## 2. Node
```powershell
winget install -e --id OpenJS.NodeJS.LTS
```
Close and reopen PowerShell.

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
