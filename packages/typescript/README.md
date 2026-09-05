# Agent Supply Trust API TypeScript SDK

Evaluate packages, containers, MCP servers, agent skills and plugins for provenance, permissions and runtime risk.

This package is the zero-runtime-dependency TypeScript/JavaScript client from
the audited public integration repository. It supports ESM and CommonJS on
Node.js 18 or newer. Import and construction perform no network request.

## Install

```sh
npm install agent-supply-trust
```

## Authenticated client

```ts
import { SupplyChainTrust } from 'agent-supply-trust'

const client = new SupplyChainTrust({
  apiKey: process.env.SUPPLY_CHAIN_TRUST_API_KEY,
})
```

Never place an API key in browser code, source control, logs, or examples.
Requesting a sandbox key is an email-verification and claim flow; it does not
return a key in the initial response.

- [Product, docs, demo, pricing, privacy, and terms](https://agentsupplytrust-api.com/?utm_source=npm&utm_medium=package&utm_campaign=agent-supply-trust&utm_content=readme)
- [Source and changelog](https://github.com/API-Disk-Integrations/agent-supply-trust)
- [Issues](https://github.com/API-Disk-Integrations/agent-supply-trust/issues)

Security reports must not be filed in a public issue. Use the repository's
private security-reporting path after the owner confirms it is enabled.

MIT licensed. The API service remains governed by the product site's terms.
