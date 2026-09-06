# Agent Supply Trust API

Evaluate packages, containers, MCP servers, agent skills and plugins for
provenance, permissions and runtime risk.

- [Product and pricing](https://agentsupplytrust-api.com/?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme#pricing)
- [Developer documentation](https://agentsupplytrust-api.com/docs?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme)
- [Create a free account](https://agentsupplytrust-api.com/signup?utm_source=github&utm_medium=developer&utm_campaign=agent-supply-trust-github&utm_content=readme)
- [OpenAPI contract](https://agentsupplytrust-api.com/openapi.json)
- [Postman collection](./postman_collection.json)

## Quickstart: inspect an agent component without an account

The public demo statically analyzes the supplied metadata with the production
scanner and policy engine. It never installs or executes the component.

```bash
curl -sS -X POST https://agentsupplytrust-api.com/v1/demo/scan \
  -H 'content-type: application/json' \
  -d '{"kind":"mcp_server","name":"acme-mcp","version":"2.1.0","provenance":{"signed":true,"publisherVerified":true,"sourceRepo":"https://github.com/acme/mcp"},"permissions":["tool.invoke"]}'
```

The response explains the policy decision and quotes the observed evidence:

```json
{
  "verdict": {
    "decision": "allow",
    "reasons": [],
    "policyVersion": "default-v1",
    "componentDigest": "sha256:30c6a33c07624b0d65e26610f34752553d12ae5355154fb089d94e1223a8c448",
    "riskScore": 0
  },
  "scan": {
    "riskScore": 0,
    "severityCounts": {"critical": 0, "high": 0, "medium": 0, "low": 0},
    "findings": []
  },
  "requestId": "req_example"
}
```

That is the first useful result: `verdict.decision` is the enforcement answer;
`scan.findings` provides the auditable reasons and exact observed evidence.

## Create and use a free API key

```bash
curl -sS -X POST https://agentsupplytrust-api.com/v1/keys \
  -H 'content-type: application/json' \
  -d '{"email":"you@example.com","source":{"source":"github","medium":"developer","campaign":"agent-supply-trust-github","content":"readme"}}'

curl -sS -X POST https://agentsupplytrust-api.com/v1/keys/claim \
  -H 'content-type: application/json' \
  -d '{"token":"PASTE_ONE_TIME_TOKEN_FROM_EMAIL"}'

export KEY='PASTE_API_KEY_FROM_CLAIM_RESPONSE'
```

Ask for an authenticated, auditable policy verdict:

```bash
curl -sS -X POST https://agentsupplytrust-api.com/v1/verdicts \
  -H "Authorization: Bearer $KEY" \
  -H 'content-type: application/json' \
  -d '{"component":{"kind":"mcp_server","name":"acme-mcp","version":"2.1.0","provenance":{"signed":true,"publisherVerified":true,"sourceRepo":"https://github.com/acme/mcp"},"permissions":["tool.invoke"]}}'
```

## SDKs

- [Python SDK](./sdk/python/supply_chain_trust.py) — currently reads the legacy
  compatibility variable `SUPPLY_CHAIN_TRUST_API_KEY`
- [TypeScript SDK](./sdk/typescript/index.ts)

The legacy filename and environment variable remain supported so existing
integrations do not break; the public product name is Agent Supply Trust. The
OpenAPI document is the authoritative operation and schema contract.

## Collection scope

The runnable Postman collection includes the public demo, the no-key checkout
path, key bootstrap, and API-key product operations. It intentionally excludes
the provider-only billing webhook and browser-session subscription, invoice,
and payment routes: those require a signed hub request or the dashboard's
HttpOnly session and CSRF controls, and a bearer API key cannot run them. The
OpenAPI document linked above remains the reference for those operations.

## Authentication and troubleshooting

- `401`: set `KEY` to the value returned once by `/v1/keys/claim`.
- `400 invalid_request`: provide a supported `kind` plus non-empty `name` and
  `version`; permissions must use the documented enum. A client-side schema
  tool may label the same input problem `422` before send.
- `429`: wait for `Retry-After` when present, then retry with backoff.

Errors use a stable `error.code` and request ID. Share only the request ID with
support, never private component instructions, an API key or claim token.

## Distribution attribution

The key request above uses the stable tuple
`github / developer / agent-supply-trust-github / readme`. The Postman
collection and SDKs carry their own source metadata. Attribution compares
qualified activation and retained use; it does not claim that this channel
already performs.

## License

[MIT](./LICENSE)
