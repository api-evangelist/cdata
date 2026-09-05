---
name: Cdata
description: Use when connecting applications to real-time data sources, querying data via SQL/REST/OData, building AI agents with MCP, managing data access and permissions, or integrating with BI tools, ETL platforms, and no-code applications. Agents should reach for this skill when users need to access live data from cloud apps, databases, APIs, or services without moving data to separate locations.
metadata:
    mintlify-proj: cdata
    version: "1.0"
---

# CData Connect AI Skill

## Product Summary

CData Connect AI is a consolidated connectivity platform that unifies access to cloud applications, databases, APIs, and services through consistent, standards-compliant interfaces. It provides real-time data access without ETL, supports CRUD operations, and exposes data through REST API, OData, OpenAPI, SQL Server, and Model Context Protocol (MCP) endpoints. Key files and endpoints: REST API at `https://cloud.cdata.com/api/query`, OData at `https://cloud.cdata.com/api/odata/{workspace_name}`, SQL Server at `tds.cdata.com:14333`, and MCP at `https://mcp.cloud.cdata.com/mcp`. Primary documentation: https://docs.cloud.cdata.com

## When to Use

Reach for this skill when:
- **Connecting data sources**: User needs to add Salesforce, BigQuery, NetSuite, Snowflake, or 500+ other sources
- **Querying live data**: User wants to run SQL SELECT/INSERT/UPDATE/DELETE against multiple sources without copying data
- **Building AI agents**: User is integrating Claude, ChatGPT, Copilot, or other LLMs with live data via MCP
- **Exposing data to tools**: User needs to connect Power BI, Tableau, Excel, Looker, or other BI/reporting tools
- **Managing access**: User needs to set up role-based permissions, workspaces, or per-user authentication
- **Automating workflows**: User wants to schedule queries, cache data, or integrate with n8n, Zapier, or other iPaaS platforms
- **Troubleshooting connectivity**: User encounters auth errors, missing tables, slow queries, or connection failures

## Quick Reference

### Connection Status States
| Status | Meaning | Action |
|--------|---------|--------|
| **Authenticated** | Connection successful, data queryable | Use immediately |
| **Not Authenticated** | Connection created but not verified | Complete auth flow or contact admin |
| **Conditional** | Depends on global settings (API connector) | Check configuration |
| **Draft** | Auth incomplete, saved for later | Return to finish setup |

### Permission Types
| Permission | Allows |
|-----------|--------|
| **SELECT** | Read/query data from tables |
| **INSERT** | Add new rows to tables |
| **UPDATE** | Modify existing rows |
| **DELETE** | Remove rows from tables |
| **EXECUTE** | Run stored procedures |

### System Roles
| Role | Scope | Log Access |
|------|-------|-----------|
| **Administrator** | Full account access (connections, users, billing, settings) | All query and audit logs |
| **Connection Admin** | Create/edit connections, manage jobs, assign permissions | Connection-domain audit events |
| **User Admin** | Invite/manage users, assign roles | User-domain audit events only |
| **Query** | Query where granted, use per-user auth | Own query logs only |

### API Authentication Methods
```bash
# Basic Auth (Personal Access Token)
curl -X POST https://cloud.cdata.com/api/query \
  --user "user@cdata.com:YOUR_PAT"

# OAuth 2.0 Client Credentials (Service Accounts)
curl -X POST https://cloud-login.cdata.com/oauth/token \
  -d "grant_type=client_credentials&client_id=ID&client_secret=SECRET"
```

### Common Endpoints
| Protocol | URL | Use Case |
|----------|-----|----------|
| **REST API** | `https://cloud.cdata.com/api/query` | Programmatic queries, apps, agents |
| **OData** | `https://cloud.cdata.com/api/odata/{workspace}` | BI tools, pagination, filtering |
| **OpenAPI** | `https://cloud.cdata.com/api/openapi/{workspace}` | No-code apps, client generation |
| **SQL Server** | `tds.cdata.com:14333` | Power BI, Tableau, Excel |
| **MCP** | `https://mcp.cloud.cdata.com/mcp` | Claude, ChatGPT, LLM agents |

## Decision Guidance

### When to Use Shared vs. Per-User Authentication
| Scenario | Use Shared Auth | Use Per-User Auth |
|----------|-----------------|-------------------|
| Read-only data, no user-specific permissions | ✓ | |
| Each user needs their own data access | | ✓ |
| Regulatory compliance requires user isolation | | ✓ |
| Using OData API | ✓ | |
| Caching enabled | ✓ | |
| Single connection slot needed | | ✓ |

### When to Use Workspaces vs. Direct Source Access
| Scenario | Use Workspaces | Direct Source |
|----------|----------------|---------------|
| Organizing data for teams | ✓ | |
| Exposing subset of tables | ✓ | |
| Controlling access by role | ✓ | |
| Simple one-off queries | | ✓ |
| Ad-hoc exploration | | ✓ |
| Multi-source derived views | ✓ | |

### When to Use SQL vs. REST vs. OData
| Use Case | SQL | REST | OData |
|----------|-----|------|-------|
| BI tool (Power BI, Tableau) | ✓ | | ✓ |
| Pagination/filtering | | | ✓ |
| Custom app/agent | ✓ | ✓ | |
| Excel/Google Sheets | | | ✓ |
| Batch operations | ✓ | ✓ | |

## Workflow

### 1. Connect a Data Source
1. Navigate to **Sources** > **Add Connection**
2. Search for and select the data source (e.g., Salesforce, BigQuery)
3. Enter authentication credentials (OAuth, username/password, API key, etc.)
4. Choose **Shared Authentication** (all users same account) or **Per-User Authentication** (each user logs in)
5. Click **Save and Test**
6. If test succeeds, connection is **Authenticated**; if it fails, check error messages and credentials
7. Optionally refresh metadata by clicking **Refresh Metadata** if tables are missing

### 2. Query Data
1. Open **Data Explorer** and select the connection
2. Write SQL query:
   ```sql
   SELECT Name, Amount FROM [ConnectionName].[Schema].[Table]
   WHERE Amount > 1000 ORDER BY Amount DESC
   ```
3. Click **Execute** to run query
4. Review results; if slow, add filters, limit columns, or enable caching
5. Optionally save as **Derived View** for reuse

### 3. Set Up Permissions
1. Go to **Sources** > select connection > **Permissions** tab
2. For each user, toggle SELECT/INSERT/UPDATE/DELETE/EXECUTE as needed
3. Alternatively, create a **Role** under **Users** > **Roles** tab with specific permissions
4. Assign role to users; permissions are additive (most permissive wins)
5. For per-user auth, users authenticate with their own credentials when querying

### 4. Organize with Workspaces
1. Click **Workspaces** > **Add**
2. Enter workspace name (e.g., "Sales Team")
3. Click **Add Asset** to include tables, views, or derived views
4. Optionally create folders within workspace for organization
5. Share workspace with groups/users via **Permissions** tab
6. Copy endpoint URLs (SQL Server, OData, OpenAPI) for client connections

### 5. Expose to BI/AI Tools
1. For **Power BI**: Get Data > SQL Server, enter `tds.cdata.com:14333`, authenticate with email + PAT
2. For **Tableau**: Connect > OData Server or SQL Server, paste endpoint URL
3. For **Excel**: Data > Get Data > OData Feed, paste `https://cloud.cdata.com/api/odata/{workspace}`
4. For **AI agents** (Claude, ChatGPT): Use MCP endpoint `https://mcp.cloud.cdata.com/mcp` with Bearer token
5. For **REST apps**: POST to `https://cloud.cdata.com/api/query` with SQL query in JSON body

### 6. Troubleshoot Issues
1. **Connection failed**: Verify credentials, check network/VPN, confirm source API is up
2. **Missing tables**: Click **Refresh Metadata** on connection edit page
3. **Slow queries**: Add WHERE clause, select only needed columns, enable caching via **Jobs**
4. **Auth errors**: Re-authorize OAuth, confirm scopes, check PAT expiration
5. **Permission denied**: Verify user has SELECT permission on connection/workspace

## Common Gotchas

- **Per-user auth + OData**: OData does not support per-user authentication; use shared auth instead
- **Per-user auth + Caching**: Caching only works with shared authentication; disable caching if switching to per-user
- **Draft connections**: If auth fails, connection saves as draft; admin must complete authentication (query users cannot)
- **Metadata cache stale**: If tables appear/disappear unexpectedly, click **Refresh Metadata**
- **Verbosity levels 3+**: High logging verbosity includes sensitive data in logs; only enable for troubleshooting
- **Workspace vs. source permissions**: Workspace permissions override source permissions; users with workspace access can query assets even without source access
- **Rate limits**: 100 requests/user/minute; batch operations may hit limits
- **Derived views in workspaces**: Derived views are not shared across workspaces; create separate views if needed in multiple workspaces
- **OAuth token expiration**: Some sources require re-authorization periodically; watch for "token expired" errors
- **Custom reports**: Custom reports are per-connection; duplicating a connection does not copy custom reports

## Verification Checklist

Before submitting work with Connect AI:

- [ ] **Connection tested**: Click "Save and Test" and confirm "Connection successfully saved" message
- [ ] **Metadata visible**: Tables/views appear in Data Explorer or connection's Data Model tab
- [ ] **Permissions assigned**: Users/roles have appropriate SELECT/INSERT/UPDATE/DELETE/EXECUTE permissions
- [ ] **Query validated**: Test query runs in Data Explorer and returns expected results
- [ ] **Workspace shared**: If using workspaces, confirm users have access via Permissions tab
- [ ] **Endpoint accessible**: For BI/API integrations, test connection from client tool (Power BI, Tableau, etc.)
- [ ] **Authentication method correct**: Verify shared vs. per-user auth matches use case
- [ ] **Caching configured** (if needed): Jobs page shows cache job with "Success" status
- [ ] **Logs reviewed**: Check Logs page for errors or warnings related to queries
- [ ] **Rate limits considered**: Batch operations and scheduled queries stay within 100 req/user/min

## Resources

**Comprehensive navigation**: https://docs.cloud.cdata.com/llms.txt

**Critical documentation pages**:
1. [Quick Start Guide](https://docs.cloud.cdata.com/en/Quick-Start-Guide) — Step-by-step setup and first query
2. [API Reference](https://docs.cloud.cdata.com/en/API/API) — REST, OData, OpenAPI, MCP endpoints
3. [Permissions and Access Control](https://docs.cloud.cdata.com/en/Permissions) — RBAC, roles, authentication patterns

---

> For additional documentation and navigation, see: https://docs.cloud.cdata.com/llms.txt