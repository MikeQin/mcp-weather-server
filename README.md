# MCP Server - Weather (Python)

### Set up your environment

First, let’s install uv and set up our Python project and environment:
```bash
# install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Now, let’s create and set up our project:
```sh
# Create a new directory for our project
uv init weather-server
cd weather-server

# Create virtual environment and activate it
uv venv
source .venv/Scripts/activate

# Install dependencies
uv add "mcp[cli]" httpx

# Create our server file
touch server.py

# Run
uv run server.py
```

Your server is complete! Run `uv run server.py` to confirm that everything’s working.

### Adding single weather server to Claude Desktop

```sh
code $env:AppData\Roaming\Claude\claude_desktop_config.json
```

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\dev\\mcp-projects\\weather-server",
        "run",
        "weather.py"
      ]
    }
  }
}
```

To launch the weather server:

```sh
uv --directory C:\\dev\\mcp-projects\\weather-server run server.py
```

## MCP Inspector

```sh
npx @modelcontextprotocol/inspector
# optional
npx @modelcontextprotocol/inspector uvx --directory "C:\\dev\\mcp-projects\\weather-server" run server.py
# For example
npx @modelcontextprotocol/inspector uvx mcp-server-git --repository ~/code/mcp/servers.git
```

### claude_desktop_config.json

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\dev\\mcp-projects\\weather-server",
        "run",
        "server.py"
      ]
    }
  }
}
```

For streamable HTTP servers, you might need to use an `adapter` like `mcp-remote` if Claude Desktop doesn't natively support the protocol. `mcp-remote` bridges the communication between clients and remote servers using Streamable HTTP or SSE.

```json
{
  "mcpServers": {
    "weather_server": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://localhost:8000/mcp/"
      ]
    }
  }
}
```