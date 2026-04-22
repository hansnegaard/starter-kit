# macOS Quick Setup

Three commands, then hand off to Claude.

Open Terminal: press `Cmd`+`Space`, type `terminal`, hit `Enter`.

## 1. Homebrew (includes Git)
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
When prompted, allow Xcode Command Line Tools to install. After it finishes, follow the "Next steps" Homebrew prints to add `brew` to your `PATH`, then close and reopen Terminal.

## 2. Node
```bash
brew install node
```

## 3. Claude Code
```bash
npm install -g @anthropic-ai/claude-code
claude
```

---

## Hand off to Claude

Once Claude is running, paste this single prompt and walk away:

```
Complete my macOS dev setup by following the instructions at https://raw.githubusercontent.com/hansnegaard/starter-kit/main/CLAUDE-macos.md
```
