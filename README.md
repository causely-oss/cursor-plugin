# Causely for Cursor

Use Causely directly in Cursor through a preconfigured MCP server. Query service health, root causes, SLOs, metrics, and topology through natural conversation — grounded in system ontology and live causal intelligence.

## Prerequisites

- A [Causely](https://causely.ai) account. Contact support@causely.ai if you need access.
- Cursor with MCP support.

## Installation

Install via **Cursor Settings → Plugins**, search for **Causely**, and click **Install**. Cursor will prompt you to sign in to Causely and grant access.

## Authentication

### OAuth (recommended)

Cursor initiates the OAuth flow automatically on install. Sign in to Causely once — Cursor manages token refresh from that point on.

### API credentials

For non-interactive or CI environments, generate API credentials at [auth.causely.app/oauth/portal/api-tokens](https://auth.causely.app/oauth/portal/api-tokens) and configure the server manually:

```json
{
  "mcpServers": {
    "causely": {
      "url": "https://api.causely.app/mcp",
      "transport": "Streamable HTTP",
      "headers": {
        "X-Causely-Client-Basic": "Basic <base64(client_id:client_secret)>"
      }
    }
  }
}
```

## What you can ask

- "What's the root cause of the checkout service degradation?"
- "Which services are burning their error budget?"
- "What changed before this incident started?"
- "Show me the blast radius of the database slowdown."
- "Are there correlated failures across namespaces?"
- "Write a post-mortem for the incident that resolved an hour ago."
- "What are the top slow queries on the orders database?"
- "Give me a morning health report for the production namespace."

## Packaged skills

This plugin includes six skills that activate automatically for the right type of question:

| Skill | Activates for |
|---|---|
| `causely-alert-triage` | Incoming alerts — PagerDuty, Datadog, Prometheus, OpsGenie |
| `causely-change-impact` | Post-deploy regression checks and rollout validation |
| `causely-correlated-incidents` | Multi-service failures and blast radius analysis |
| `causely-health-reporting` | Health summaries, SLO status, morning briefings |
| `causely-k8s-investigation` | Kubernetes infrastructure — pods, nodes, namespaces |
| `causely-postmortem` | Post-mortems, incident reports, and ticket drafts |

## Available tools

All tools are read-only. Causely does not execute changes through this connection.

| Tool | Description |
|---|---|
| `get_environment_health` | Global health overview: active root causes, symptoms, status |
| `get_root_causes` | Root causes with remediation, blast radius, and supporting symptoms |
| `get_symptoms` | Raw observable signals feeding into root cause detection |
| `triage` | Deep investigation of a single service |
| `get_service_summary` | Comprehensive health summary for a service |
| `get_entity_health` | Health for databases, pods, queues, and other entity types |
| `team_health` | Health summary for all services owned by a team |
| `get_metrics` | Time-series or snapshot metrics for any entity |
| `get_logs` | Logs for an entity or evidence logs for a root cause |
| `get_alerts` | Alert history with mapping state |
| `get_events` | Lifecycle events: restarts, deployments, scaling, config changes |
| `get_topology` | Dependency graph: upstream, downstream, or end-to-end dataflow |
| `get_slo` | Error budget, burn rate, at-risk and violated SLOs |
| `get_slow_queries` | Slow SQL queries ranked by total execution time |
| `get_entities` | Resolve service and infrastructure entity names to IDs |
| `get_scopes` | Discover available clusters, namespaces, customers, and products |
| `get_label_values` | Enumerate distinct values for a label key (e.g. team, product) |
| `list_namespaces` | List all Kubernetes namespace names |
| `list_clusters` | List all cluster names |
| `get_integration_status` | Scraper and integration status per cluster |
| `get_config` | Raw configuration files for an entity |
| `reliability_delta` | Post-deploy regression check for a single service |
| `fleet_reliability_delta` | Post-deploy regression check across a team or namespace |
| `postmortem` | Structured post-mortem draft from a resolved incident |
| `generate_ticket` | Ticket draft for Jira, GitHub, or Linear from an incident |
| `ask_causely` | Natural-language question answering (markdown response) |

## Support

Email: support@causely.ai
Website: https://causely.ai
Docs: https://docs.causely.ai/agent-integration/mcp-server
