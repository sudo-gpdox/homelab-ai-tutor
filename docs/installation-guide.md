
# Installation Guide - Homelab AI Tutor

## Prerequisites
- Debian-based Linux (Ubuntu, Debian)
- 16GB RAM minimum
- 20GB free disk space
- Internet connection

---
## Git Commit

- git add docs/installation-guide.md
- git commit -m "Clean up installation guide with proper step numbering"
- git push origin main

## Step 1: Install Ollama

Install Ollama AI engine:

```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Start and enable service
sudo systemctl start ollama
sudo systemctl enable ollama

# Verify installation
ollama --version
```

---

## Step 2: Download AI Model

Pull the Llama 3.2 3B model (recommended for tutoring):

```bash
# Download model
ollama pull llama3.2:3b

# Test the model
ollama run llama3.2:3b "What is Docker?"

# Exit chat by typing: /bye
```

**Expected Performance (CPU):**
- Speed: ~15-25 tokens/second
- Quality: Excellent for technical explanations
- Memory: ~2GB RAM usage

---

## Step 3: Install VS Code

VS Code is used for remote development with Cline extension.

```bash
# Verify VS Code installation
code --version
```

**Access Method:** VS Code Remote SSH from laptop
- Connect via Tailscale IP: `100.93.10.44`
- User: `gp-admin`
- Extensions install automatically on server

---

## Step 4: Install Cline Extension


---

## Step 5: Configure MCP for Obsidian
