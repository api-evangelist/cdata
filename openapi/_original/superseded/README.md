# Superseded doc-derived OpenAPI definitions

These three files were **derived from CData's public documentation** by an earlier
enrichment round (their own `info.description` said so: *"This best-effort OpenAPI is
derived from the public docs at https://docs.cloud.cdata.com/SQL-API.html"*). They were
split by tag from `../cdata-openapi.yml`.

On **2026-09-05** the enrichment pipeline found CData's **own first-party OpenAPI
definitions**, published and linked from `https://docs.cloud.cdata.com/llms.txt` under
`## OpenAPI Specs`:

| Published spec | Saved as |
|---|---|
| `https://docs.cloud.cdata.com/en/API/REST-API.yaml` | `openapi/cdata-rest-api-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/Management-API.yaml` | `openapi/cdata-management-api-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/REST-API-Embedded.yaml` | `openapi/cdata-rest-api-embedded-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/MCP-API.yaml` | `openapi/cdata-mcp-api-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/MCP-API-Embedded.yaml` | `openapi/cdata-mcp-api-embedded-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/OData-API.yaml` | `openapi/cdata-odata-api-openapi.yml` |
| `https://docs.cloud.cdata.com/en/API/OpenAPI-API.yaml` | `openapi/cdata-openapi-api-openapi.yml` |

The derived files are archived rather than deleted because they are the provenance record
of what the catalog previously asserted. They must **not** be registered in `apis.yml`:
they describe metadata paths (`/catalogs/{catalog}/schemas`) that CData's real REST API
does not serve — the real surface uses flat `/schemas`, `/tables`, `/columns` with query
parameters.

Retrieved 2026-09-05, HTTP 200 for all seven.
