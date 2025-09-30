# Project Overview

This project is a Model Context Protocol (MCP) server for WhatsApp. It allows an AI agent, such as Claude, to interact with a user's personal WhatsApp account. The agent can search and read messages (including media), search contacts, and send messages to individuals or groups.

The project consists of two main components:

1.  **Go WhatsApp Bridge (`whatsapp-bridge/`):** A Go application that connects to WhatsApp's web API using the `whatsmeow` library. It handles authentication, stores message history in a SQLite database, and exposes a REST API for sending messages and downloading media.

2.  **Python MCP Server (`whatsapp-mcp-server/`):** A Python server that implements the Model Context Protocol (MCP). It provides a set of tools that an AI agent can use to interact with WhatsApp. The server communicates with the Go bridge via its REST API and also directly queries the SQLite database for reading data.

## Building and Running

### Prerequisites

*   Go
*   Python 3.6+
*   [uv](https://github.com/astral-sh/uv) (Python package manager)
*   FFmpeg (optional, for sending audio messages)

### Steps

1.  **Run the WhatsApp bridge:**
    ```bash
    cd whatsapp-bridge
    go run main.go
    ```
    The first time you run this, you will need to scan a QR code with your WhatsApp mobile app to authenticate.

2.  **Run the Python MCP server:**
    ```bash
    cd whatsapp-mcp-server
    uv run main.py
    ```

## Development Conventions

The project is split into two separate components, each with its own language and conventions.

*   **Go WhatsApp Bridge:**
    *   Uses the standard Go project structure.
    *   Dependencies are managed with Go modules (`go.mod`, `go.sum`).
    *   The code is well-structured and includes comments explaining the purpose of functions and data structures.

*   **Python MCP Server:**
    *   Uses `uv` for package management.
    *   The main application logic is in `main.py`, which uses the `FastMCP` library to create the MCP server.
    *   The `whatsapp.py` module contains the logic for interacting with the Go bridge and the SQLite database.
    *   The code is typed using Python's type hinting system.
