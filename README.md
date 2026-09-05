# Agent Supply Trust API

Evaluate packages, containers, MCP servers, agent skills and plugins for provenance, permissions and runtime risk.

- [Product and pricing](https://agentsupplytrust-api.com/?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme#pricing)
- [Developer documentation](https://agentsupplytrust-api.com/docs?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme)
- [Create a free account](https://agentsupplytrust-api.com/signup?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme)
- [OpenAPI contract](https://agentsupplytrust-api.com/openapi.json)
- [Postman collection](./postman_collection.json)

## Quickstart

### 1. Request a free-key verification email

```bash
curl -X POST https://agentsupplytrust-api.com/v1/keys \
  -H 'content-type: application/json' \
  -d '{"email":"you@example.com","source":{"source":"github","medium":"developer","campaign":"agent-supply-trust-github","content":"readme"}}'
```

The service returns `202 Accepted` and sends a one-time claim link. Follow the
email, or exchange its token with `POST /v1/keys/claim`. The API key is shown
once after verification; store it securely. No card is required for the free
sandbox. Current free allowance: **100 component scans/month**.

### 2. Make the first product call

```bash
curl -X POST https://agentsupplytrust-api.com/v1/scans \
  -H "Authorization: Bearer $KEY" \
  -H 'content-type: application/json' \
  -d '{"components":[{"kind":"mcp_server","name":"acme-mcp","version":"1.4.0"}]}'
```

## SDKs

The repository includes dependency-light client files that point to the current
contract and canonical product domain:

- [Python SDK](./sdk/python/supply_chain_trust.py) — reads `SUPPLY_CHAIN_TRUST_API_KEY`
- [TypeScript SDK](./sdk/typescript/index.ts)

Copy the file you need into your project. The OpenAPI document remains the
authoritative operation and schema contract.

## Authentication and errors

API operations use `Authorization: Bearer <API_KEY>` (or `x-api-key` where
documented). Dashboard-session operations and signed service webhooks are not
callable with a customer API key. Public demo and health operations require no
credential. Errors use a stable `error.code` plus a request ID for support.

## Distribution attribution

The key request above identifies this README with the stable tuple
`github / developer / agent-supply-trust-github / readme`. The Postman collection and both
SDKs carry their own source metadata. Attribution is used to compare qualified
activation and retained use; it is not evidence that this channel already
performs.

## License

[MIT](./LICENSE)
