# Brazil CNPJ Company Data MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-brazil-cnpj-company-data/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-brazil-cnpj-company-data) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-brazil-cnpj-company-data%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-brazil-cnpj-company-data&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-brazil-cnpj-company-data)](https://www.npmjs.com/package/@mambalabsdev/mcp-brazil-cnpj-company-data) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-brazil-cnpj-company-data)](https://www.npmjs.com/package/@mambalabsdev/mcp-brazil-cnpj-company-data) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-brazil-cnpj-company-data)](https://github.com/mambalabsdev/mcp-brazil-cnpj-company-data/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-brazil-cnpj-company-data)

An MCP server for the Mamba Labs Brazil CNPJ Company Data actor on Apify. Brazil CNPJ registry data as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes CNPJs and returns one row per company with status, size, capital, CNAE activities, address, phones, Simples and MEI, and tax regime. Partners add one row per partner or administrator.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-brazil-cnpj-company-data": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-brazil-cnpj-company-data"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `lookup_brazil_cnpj` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Look up CNPJ 07.526.557/0001-00 and list its partners."
- "Is the Brazilian company with CNPJ 33000167000101 active, and what is its main activity?"

## Tool

`lookup_brazil_cnpj`. One tool. Example arguments:

```json
{
  "cnpjs": [
    "07.526.557/0001-00"
  ],
  "include_partners": true,
  "max_partners_per_company": 5
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `cnpjs` | array | no | CNPJs to look up, 14 digits with or without punctuation (07.526.557/0001-00 or 07526557000100). An 8 digit root reads the head office. Up to 10,000 per run. In Clay, put the column inside a one item list. |
| `include_partners` | boolean | no | true adds one row per partner or administrator (QSA), charged per partner. Default false. |
| `max_partners_per_company` | number | no | Most partner rows per company, 1 to 1000. Default 100. |
| `dedupe` | boolean | no | true (default) reads a CNPJ once per run even when it appears twice. The repeat is not charged. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `company-row`, one company read from the CNPJ registry | $0.0035 | $0.003325 | $0.00315 | $0.002975 |
| `partner-row`, one partner (QSA) of a company | $0.001 | $0.00095 | $0.0009 | $0.00085 |
| `apify-actor-start`, per run start | $0.005 | $0.005 | $0.005 | $0.005 |

Repeats, CNPJs not found, invalid values, summaries, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/brazil-cnpj-company-data](https://apify.com/mambalabs/brazil-cnpj-company-data)

## License

MIT. See [LICENSE](LICENSE).
