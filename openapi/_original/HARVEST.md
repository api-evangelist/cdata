# Harvested source — CData's own OpenAPI definitions

Every file in this directory (excluding `superseded/`) was fetched **verbatim** from CData's
own documentation host on **2026-09-05**, HTTP 200 for all seven, and is byte-identical to
what CData serves. They are linked from `https://docs.cloud.cdata.com/llms.txt` under the
`## OpenAPI Specs` heading.

| Fetched from | Saved as |
|---|---|
| https://docs.cloud.cdata.com/en/API/REST-API.yaml | cdata-rest-api-openapi.yml |
| https://docs.cloud.cdata.com/en/API/Management-API.yaml | cdata-management-api-openapi.yml |
| https://docs.cloud.cdata.com/en/API/REST-API-Embedded.yaml | cdata-rest-api-embedded-openapi.yml |
| https://docs.cloud.cdata.com/en/API/MCP-API.yaml | cdata-mcp-api-openapi.yml |
| https://docs.cloud.cdata.com/en/API/MCP-API-Embedded.yaml | cdata-mcp-api-embedded-openapi.yml |
| https://docs.cloud.cdata.com/en/API/OData-API.yaml | cdata-odata-api-openapi.yml |
| https://docs.cloud.cdata.com/en/API/OpenAPI-API.yaml | cdata-openapi-api-openapi.yml |

## Ownership check (STEP 0c)

All seven belong to CData, judged by what they say about themselves and not by where they
were fetched:

- `servers[]` are `https://cloud.cdata.com/api`, `https://cloud.cdata.com/api/v1/admin`,
  `https://cloud.cdata.com/api/odata`, `https://cloud.cdata.com/api/openapi` and
  `https://mcp.cloud.cdata.com` — all CData-controlled hosts.
- `info.title` on five of the seven begins "CData Connect AI". The two MCP documents are
  titled "Example MCP Server API" (a template title CData did not customise), but their
  `servers[]` name `https://mcp.cloud.cdata.com`, the endpoint CData's own MCP
  documentation tells clients to use, and a live probe of that host returns a CData
  MCP OAuth challenge.
- The auth descriptions reference CData's own concepts by name — "Use your PAT as the
  password. You can get your PAT from Connect AI by selecting **Settings** > **Access
  Tokens**" — and the OAuth token URL is `https://cloud-login.cdata.com/oauth/token`,
  which matches https://docs.cloud.cdata.com/en/API/Authentication.

`info.contact` and `info.termsOfService` are absent from all seven; ownership rests on
`servers[]`, `info.title` and the auth descriptions above.

## superseded/

`superseded/` holds the doc-derived definitions an earlier round authored, kept as a
provenance record. See `superseded/README.md`. They are **not** harvested and must not be
registered in `apis.yml`.
