# Evaboot MCP Server

Extract LinkedIn Sales Navigator leads and find or validate their professional emails, from any MCP client.

This repository holds the documentation for Evaboot's hosted MCP server. The server itself is a remote endpoint run by Evaboot; there is nothing to install.

## What it does

Evaboot turns a plain-English audience description into a LinkedIn Sales Navigator search, exports the results, and finds and verifies a professional email for each lead. Results can be pushed straight into HubSpot, Attio, Apollo, Pipedrive, Instantly, lemlist, Clay, Google Sheets, Make, Zapier, n8n or your own webhook.

## Connect it

Remote endpoint (Streamable HTTP):

```
https://mcp.evaboot.com/mcp
```

**Grok**: on grok.com, Plugins → New Connector → Custom → name it Evaboot and paste the URL → sign in to Evaboot and approve. Works on the free plan.

**Grok Bot**: connectors are shared with your Grok account, so the step above covers it. From the desktop app, send "Add a custom MCP server called evaboot at https://mcp.evaboot.com/mcp", then Authorize.

**Grok Build**: `grok mcp add --transport http evaboot https://mcp.evaboot.com/mcp --header "Authorization: Bearer YOUR_API_KEY"`, or install the plugin with `grok plugin install https://github.com/evaboot-labs/evaboot-grok-plugin.git`.

**Claude**: Settings → Connectors → Add custom connector → paste the URL → sign in to Evaboot and approve.

**ChatGPT**: Settings → Connectors → add the URL above.

**Cursor / VS Code**: add to your MCP config:

```json
{
  "mcpServers": {
    "evaboot": {
      "url": "https://mcp.evaboot.com/mcp"
    }
  }
}
```

## Authentication

OAuth 2.1 with PKCE and dynamic client registration. Most clients handle this for you: paste the URL and sign in through the browser.

```
authorize   https://mcp.evaboot.com/o/authorize/
token       https://mcp.evaboot.com/o/token/
register    https://mcp.evaboot.com/o/register/
```

Clients that can't do OAuth can send an API key instead:

```
Authorization: Bearer <your Evaboot API key>
```

Get a key from the API page of your Evaboot dashboard.

## Tools

56 tools, grouped by what they do.

### Search building

| Tool | What it does |
| --- | --- |
| `build_sn_search_from_prompt` | Turn a natural-language audience into a Sales Navigator search URL. |
| `get_search_build` | Poll a search that `build_sn_search_from_prompt` is still building. |
| `get_account_based_search_job` | Poll an account-based lead search started by `build_sn_search_from_prompt`. |
| `search_sn_leads` | Read one page of a Sales Navigator lead search. |
| `search_sn_accounts` | Read one page of a Sales Navigator account search. |
| `list_saved_searches` | List your saved Sales Navigator searches. |
| `save_search` | Save a Sales Navigator search on your seat. |
| `delete_saved_search` | Delete a saved search from your Sales Navigator account. |
| `read_alerts` | Read Sales Navigator alerts (job changes, posts, funding rounds). |

### Extraction

| Tool | What it does |
| --- | --- |
| `export_sn_search_or_list` | Export a Sales Navigator search or lead/account list. |
| `export_profile` | Export one LinkedIn profile. |
| `export_profile_list` | Export a list of profile URLs or ids (1 to 2,500). |
| `get_export` | Fetch an export's status and results. |
| `get_export_list` | List your exports, newest first. |
| `cancel_sales_nav_job` | Stop a running Sales Navigator job. |
| `get_daily_export_quota` | Get your remaining daily export quota and credit balance. |

### Email finding

| Tool | What it does |
| --- | --- |
| `find_email_single` | Find one professional email from a name and company. |
| `find_emails` | Find emails for a list of people in bulk. |
| `list_email_finder_jobs` | List your email-finder jobs. |
| `get_email_finder_job` | Fetch an email-finder job's status and results. |

### Email verification

| Tool | What it does |
| --- | --- |
| `verify_email_single` | Verify one email address. |
| `verify_email` | Verify many email addresses in bulk. |
| `list_email_verification_jobs` | List your email-verification jobs. |
| `get_email_verification_job` | Fetch a verification job's status and results. |

### List management

| Tool | What it does |
| --- | --- |
| `list_lead_lists` | List your Sales Navigator lead lists. |
| `create_lead_list` | Create a lead list. |
| `add_leads_to_list` | Add leads to a lead list. |
| `create_lead_list_from_ids` | Create lead lists from profile ids. |
| `create_lead_list_from_search` | Save every result of a lead search into a new lead list. |
| `delete_lead_list` | Delete a lead list. |
| `list_account_lists` | List your Sales Navigator account lists. |
| `create_account_list` | Create an account list. |
| `add_accounts_to_list` | Add companies to an account list. |
| `create_account_list_from_ids` | Create an account list from company ids. |
| `create_account_list_from_search` | Save every result of an account search into a new account list. |
| `delete_account_list` | Delete an account list. |
| `split_lead_search` | Split a lead search over 2,500 people into list-backed slices. |
| `split_account_search` | Split an account search over 1,000 companies into list-backed slices. |
| `get_list_from_search_status` | Poll a list being built from a search. |

### Recurring exports

| Tool | What it does |
| --- | --- |
| `create_recurring_export` | Repeat a Sales Navigator search daily, weekly or monthly. |
| `list_recurring_exports` | List your recurring exports. |
| `get_recurring_export` | Fetch one recurring export. |
| `update_recurring_export` | Change a recurring export's name, cadence or pause state. |
| `delete_recurring_export` | Stop a recurring export permanently. |
| `attach_recurring_export` | Send every future run of a recurring export to a destination. |

### Integrations

| Tool | What it does |
| --- | --- |
| `list_integrations` | List the CRM and webhook destinations you have connected. |
| `connect_integration` | Connect a CRM, outreach tool, spreadsheet or webhook. |
| `test_integration` | Send a sample payload to a webhook destination. |
| `list_integration_targets` | List where a connected provider can receive leads. |
| `push_export` | Send a finished export to a connected destination. |
| `get_push` | Check a push started by `push_export`. |
| `retry_write_back` | Re-run failed write-backs of an email job. |
| `list_lead_sources` | List where leads can be read from in a connected CRM or outreach tool. |
| `get_leads_from_integration` | Read leads from your own CRM or outreach tool. |
| `list_folders` | List the folders on your Evaboot account. |

### Account

| Tool | What it does |
| --- | --- |
| `verify_token` | Check that your Evaboot credentials are valid. |

## Requirements

- An Evaboot account
- A LinkedIn account with Sales Navigator, connected through the Evaboot Chrome extension

## Links

- Product: https://evaboot.com/mcp
- Documentation: https://docs.evaboot.com/mcp-server
- Support: support@evaboot.com

## License

The documentation in this repository is released under the [MIT License](LICENSE). The Evaboot service is proprietary.
