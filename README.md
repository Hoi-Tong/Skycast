# 🌤️ Skycast

A full **Model Context Protocol (MCP)** project containing:

- A custom **MCP Weather Server** *(Python, FastMCP, NWS API)*
- A custom **MCP Client** *(Python, Anthropic API, Claude tool-use)*
- Fully interactive tool-calling between Claude ↔ Server
- Built following Anthropic's tutorials: *Build an MCP Server* + *Build an MCP Client*

---

## ✨ Features

### **MCP Weather Server**
- Provides two MCP tools:
  - `get_alerts(state)` — fetch active NWS alerts  
  - `get_forecast(latitude, longitude)` — fetch 5-period weather forecast
- Uses:
  - `FastMCP`
  - `httpx` async HTTP requests
- Safe for STDIO (no `print()`, uses `logging`)

### **MCP Client**
- Connects to any MCP server (`.py` or `.js`)
- Sends queries to Claude using the Anthropic API
- Automatically executes tool calls requested by Claude
- Maintains full interactive chat loop

---



## 💬 Example Usage

```
Query: What's the weather in Sacramento?
→ Claude → MCP Tool → Server → Forecast → Claude → You
```

```
Query: Show me alerts in TX
→ get_alerts("TX")
```

---

## 🛠️ Technologies Used

- Python 3.10+
- MCP Python SDK
- FastMCP
- Anthropic API
- httpx
- uv
- python-dotenv

---

## 🧩 How It Works

> Claude analyzes the query  
> → chooses tools  
> → client executes the tool  
> → server returns data  
> → client sends result back  
> → Claude produces final text

---

## ⚠️ Notes

- Do **not** use `print()` in STDIO servers
- Use `logging` so output goes to stderr
- Keep API keys in `.env`
- Claude Desktop requires absolute paths
- NWS API only supports U.S. weather data

---

## 📌 Example Claude Desktop Config (Windows)

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\ABSOLUTE\\PATH\\TO\\weather",
        "run",
        "weather.py"
      ]
    }
  }
}
```

---

## 📜 License

MIT License (modify as needed)

