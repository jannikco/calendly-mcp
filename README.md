# Calendly MCP server

Identify the authenticated scheduler, inspect event types and explicitly create a one-use scheduling link.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `CALENDLY_ACCESS_TOKEN`



Credential help: https://developer.calendly.com/openapi/calendly-api.yaml

## Provider setup

Use your own Calendly personal access token or previously authorized OAuth access token. Use URIs returned by your account; scheduling-link access depends on Calendly plan and scopes.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call calendly_get_current_user '{}'
```

## Use with an MCP client

Launch `node /absolute/path/calendly-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| calendly_get_current_user | Read | Read the authenticated user URI needed for event-type lookup. |
| calendly_list_event_types | Read | Read event types owned by the chosen authenticated user URI. |
| calendly_create_single_use_link | Explicit approval required | Create a scheduling link limited to one event; plan/access requirements apply. |

## Concrete workflow

Identify the authenticated scheduler, inspect event types and explicitly create a one-use scheduling link.

1. calendly_get_current_user
2. calendly_list_event_types
3. calendly_create_single_use_link

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=calendly&integration=calendly-mcp&utm_source=github&utm_campaign=github-calendly-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/calendly/).

## Provenance and maintenance

- https://developer.calendly.com/openapi/calendly-api.yaml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
