# Animate Old Photos Plugin

Animate old photos into 5-second AI videos through the hosted Animate Old Photos MCP server.

This repository is the distributable plugin package for the hosted endpoint at `https://animateoldphotos.org/api/mcp`. It includes:

- a Cursor-compatible plugin manifest in `.cursor-plugin/plugin.json`
- MCP connection metadata in `mcp.json`
- a bundled skill in `skills/animate-old-photos/SKILL.md` that teaches the agent how to use the MCP tools well

## What You Can Do

After installation, your AI agent can:

- check your Animate Old Photos credit balance
- submit an old photo for animation
- poll task status until the video is ready

Available MCP tools:

- `check_credits`
- `animate_photo`
- `get_task_status`

## Requirements

This is a paid service.

- Official site: [animateoldphotos.org](https://animateoldphotos.org/)
- Get an API key: [Profile > API Key](https://animateoldphotos.org/profile/interface-key)
- Buy credits: [Pricing](https://animateoldphotos.org/stripe)

Usage limits:

- 3 credits per animation
- input image must be JPEG or PNG
- max file size: 10 MB
- minimum size: 300 x 300 px
- `animate_photo` expects a publicly accessible image URL

## Install As a Cursor Plugin

### Option 1: Install from Marketplace

Once this package is published in the Cursor Marketplace, install `animate-old-photos` from the Marketplace UI.

### Option 2: Install from GitHub for Local Testing

Clone this repository and place it under Cursor's local plugins directory.

#### macOS / Linux

```bash
git clone <your-public-repo-url> ~/.cursor/plugins/local/animate-old-photos
```

#### Windows PowerShell

```powershell
git clone <your-public-repo-url> "$HOME\.cursor\plugins\local\animate-old-photos"
```

Restart Cursor after installation.

## Use the MCP Server Directly

The MCP server itself is not Cursor-specific. Any MCP client that supports Streamable HTTP can connect to:

```text
https://animateoldphotos.org/api/mcp
```

Example configuration:

```json
{
  "mcpServers": {
    "animate-old-photos": {
      "type": "http",
      "url": "https://animateoldphotos.org/api/mcp"
    }
  }
}
```

## Typical Workflow

1. Create an API key at [animateoldphotos.org/profile/interface-key](https://animateoldphotos.org/profile/interface-key)
2. Make sure you have at least 3 credits
3. Provide a public image URL
4. Call `check_credits`
5. Call `animate_photo`
6. Poll with `get_task_status` every 30 seconds until the result is complete
7. Download the returned video URL

## Example Prompt

The `prompt` field is optional. Short motion instructions work best.

- `grandmother smiling and waving`
- `gentle head turn with a warm smile`
- `eyes blinking slowly while looking at the camera`

## Repository Structure

```text
animate-old-photos-plugin/
├── .cursor-plugin/
│   └── plugin.json
├── mcp.json
├── README.md
└── skills/
    └── animate-old-photos/
        └── SKILL.md
```

## Notes

- This repository packages access to the hosted Animate Old Photos MCP service.
- The actual MCP endpoint is operated at `animateoldphotos.org`.
- Tool-level authentication is done with your API key; no transport-level auth is required.

## License

MIT
