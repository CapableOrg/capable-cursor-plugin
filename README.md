# Capable CRM for Cursor

Connect Cursor to [Capable](https://capable.run), an MCP-native CRM for founders and small B2B teams. Prepare for meetings, inspect contacts and deals, and turn notes into proposed CRM updates that you review field by field.

## Connect

This package contains a remote MCP connection and a `capable-crm` skill. It uses Capable's hosted Streamable HTTP server:

```text
https://crm.capable.run/api/mcp
```

Use a Capable account and authorize the connection through OAuth when prompted by Cursor. Public signup is available at [Capable](https://capable.run). This package contains no access tokens or CRM data.

For manual MCP setup, add the following server in Cursor's MCP settings or merge it into your existing `.cursor/mcp.json` configuration:

```json
{
  "mcpServers": {
    "capable": {
      "url": "https://crm.capable.run/api/mcp"
    }
  }
}
```

The skill is in [`skills/capable-crm/SKILL.md`](skills/capable-crm/SKILL.md). Plugin installations can discover it alongside the MCP configuration.

## Try it

- “Prepare me for my meeting with Acme. Summarize the people, open deals, recent conversations and next steps in Capable.”
- “Show my open pipeline by stage and identify deals with overdue next steps. Keep this read-only.”
- “Turn these meeting notes into proposed Capable updates. Show me the complete field-by-field review before saving anything: …”

Capable prepares one complete review for requested changes from notes or emails. You approve the changes to save. The assistant reports the actual save outcome.

## Package contents

- `.cursor-plugin/plugin.json`: Cursor plugin metadata.
- `.mcp.json`: Cursor-native remote MCP configuration.
- `plugin.json` and `mcp.json`: Agent Plugins 1.0 metadata and MCP configuration for compatible directory tooling.
- `skills/capable-crm/SKILL.md`: meeting preparation, pipeline and reviewed-update guidance.

Both MCP files point to the same server. Use the format your client supports; do not install duplicate connections.

The manifests and skill are validated against their available schemas and format validators. The endpoint's unauthenticated OAuth challenge is checked separately. This repository does not claim a completed authenticated Cursor runtime test.

## Help and policies

- [Developer documentation](https://crm.capable.run/developers)
- [Privacy policy](https://capable.run/legal/privacy-policy)
- [Security](https://capable.run/legal/security)
- Support: [hello@capable.run](mailto:hello@capable.run)

## License

The configuration and skill text in this package are available under the [MIT License](LICENSE). The hosted Capable service is provided separately under its own terms. Capable trademarks and the logo in `assets/logo.svg` are not licensed under MIT.
