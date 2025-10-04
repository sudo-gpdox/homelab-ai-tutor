# Installation Guide - Homelab AI Tutor

## Prerequisites
- Debian-based Linux (Ubuntu, Debian)
- 16GB RAM minimum
- 20GB free disk space
- Internet connection

---

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

Install Cline via VS Code CLI:

```bash
# Install Cline extension
code --install-extension saoudrizwan.claude-dev

# Verify installation (extension ID still uses old name)
code --list-extensions | grep claude
```

---

## Step 5: Configure Cline for Ollama

Create VS Code settings for Cline:

```bash
# Create settings directory
mkdir -p ~/.config/Code/User

# Create settings file
nano ~/.config/Code/User/settings.json
```

Add this configuration:

```json
{
  "cline.apiProvider": "ollama",
  "cline.ollamaBaseUrl": "http://127.0.0.1:11434",
  "cline.ollamaModelId": "llama3.2:3b",
  "cline.autoApprove": false,
  "cline.alwaysAllowReadOnly": true
}
```

---

## Step 6: Install Node.js and MCP Server

Install Node.js for MCP server:

```bash
# Install Node.js 20.x
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Verify installation
node --version  # Should show v20.x
npm --version   # Should show v10.x

# Install MCP filesystem server globally
sudo npm install -g @modelcontextprotocol/server-filesystem

# Verify MCP server
which mcp-server-filesystem
```

---

## Step 7: Configure MCP for Obsidian

Configure MCP to access Obsidian vault:

```bash
# Create MCP config directory
mkdir -p ~/.config/cline/mcp

# Create config file
nano ~/.config/cline/mcp/config.json
```

Add this configuration:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "mcp-server-filesystem",
      "args": ["/home/gp-admin/Documents/ClaudeVault"],
      "env": {}
    }
  }
}
```

Test the MCP server:

```bash
# Test MCP server (press Ctrl+C to stop)
mcp-server-filesystem /home/gp-admin/Documents/ClaudeVault
```

---

## Testing the Complete Setup

Verify all components are working:

```bash
# Test Ollama
ollama run llama3.2:3b "Hello, test"

# Verify all components
code --version                        # VS Code
node --version                        # Node.js
which mcp-server-filesystem           # MCP server
cat ~/.config/cline/mcp/config.json   # MCP config
cat ~/.config/Code/User/settings.json # Cline config
```

---

## Next Steps

### From Your Laptop

1. Install VS Code a  laptop
2. Install "Remote - SSH" extension
3. Connect to: `gp-admin@100.93.10.44` (via Tailscale)
4. Open Cline in VS Code
5. Start using AI tutor with Obsidian integration!

### Migration to P520

When ready to deploy on P520:

```bash
git clone https://github.com/sudo-gpdox/homelab-ai-tutor.git
cd homelab-ai-tutor
# Follow this guide from Step 1
```

---

