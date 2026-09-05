# Agent Supply Trust API Python SDK

Evaluate packages, containers, MCP servers, agent skills and plugins for provenance, permissions and runtime risk.

This package is the standard-library-only Python client from the audited public
integration repository. It supports Python 3.10 or newer. Import and
construction perform no network request.

## Install

```sh
python -m pip install agent-supply-trust
```

## Authenticated client

```python
import os
from supply_chain_trust import SupplyChainTrust

client = SupplyChainTrust(os.environ["SUPPLY_CHAIN_TRUST_API_KEY"])
```

Never place an API key in source control, logs, or examples. Requesting a
sandbox key is an email-verification and claim flow; it does not return a key
in the initial response.

- [Product, docs, demo, pricing, privacy, and terms](https://agentsupplytrust-api.com/?utm_source=pypi&utm_medium=project&utm_campaign=agent-supply-trust&utm_content=readme)
- [Source and changelog](https://github.com/API-Disk-Integrations/agent-supply-trust)
- [Issues](https://github.com/API-Disk-Integrations/agent-supply-trust/issues)

Security reports must not be filed in a public issue. Use the repository's
private security-reporting path after the owner confirms it is enabled.

MIT licensed. The API service remains governed by the product site's terms.
