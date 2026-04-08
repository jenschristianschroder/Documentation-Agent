# Documentation-Agent

This repository contains the instructions for a **Copilot Studio agent** that helps write technical documentation about **Microsoft Power Platform solutions**.

## What the agent does

The Documentation Agent produces accurate, structured, implementation-ready technical documentation for Power Platform solutions. Given a solution name or identifier, it:

- Identifies the target solution in Dataverse and establishes a strict documentation boundary
- Generates separate documents covering architecture, data model, component inventory, process flows, security, deployment, and more
- Persists each document to Dataverse so documentation is versioned, traceable, and environment-aware
- Manages its own context window by dropping persisted content after saving

## Dataverse MCP Server

The agent uses the **Dataverse MCP server** for all Dataverse access. This allows it to:

- Query solutions and their component lists directly from Dataverse
- Store generated documentation in the designated documentation tables within the **Power Platform Solution Vault** solution
- Ensure traceability between documentation and the Power Platform solution it describes

## Repository structure

| File | Description |
|------|-------------|
| `instructions.md` | Full system prompt / instructions loaded into the Copilot Studio agent |
| `examples/` | Example outputs and reference documentation |

## Getting started

1. Import or reference the `instructions.md` content as the system prompt for your Copilot Studio agent.
2. Connect the agent to a Dataverse MCP server configured for your Power Platform environment.
3. Invoke the agent with a Power Platform solution name or unique identifier to generate documentation.
