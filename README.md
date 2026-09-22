# How to Connect Cursor to Social Media With MCP

Connect Cursor to social media by adding Groniz as a remote MCP server, preferably with OAuth. Keep its publishing tools subject to Cursor's normal approval prompt. Cursor supports remote MCP over Streamable HTTP and can store the server for a project in `.cursor/mcp.json` or globally in `~/.cursor/mcp.json`. The remote endpoint is `https://mcp.groniz.com/mcp`.

Set up the connection only after the source post or media package is approved. Cursor can use it to inspect integrations, upload approved media, and deliver a reviewed payload. A person still decides the facts, rights, disclosures, destination, wording, and timing. Before the first send, verify the live integration requirements and show that person the exact write. Submit it once, then capture the returned post ID or reconcile an uncertain outcome before retrying.

## Freeze the source packet

Cursor can work beside the files that produced a release or campaign, but proximity to a repository does not make every file publishable. Create a small, approved source packet before exposing a social write tool to the task.

```markdown
Canonical source file or URL:
Approved version or commit:
Facts and links checked by:
Rights and consent checked by:
Disclosure decision:
Approved text or adaptation brief:
Approved media:
Permitted destination:
Permitted timing window:
```

Keep secrets, embargoed details, internal issue commentary, and unrelated repository context outside that packet. Creation, research, editing, approval, and rights or disclosure checks for the source stay outside Groniz. Cursor may prepare an adaptation, but the person responsible for the account must still review the final destination-specific payload.

If you need a complete preflight artifact, use the [agent-to-channel publishing checklist](https://groniz.com/blog/agent-to-channel-publishing-checklist). For the server’s role in the architecture, see [what a social media MCP server does](https://groniz.com/blog/social-media-mcp-servers). The [client-by-client setup guide](https://groniz.com/blog/ai-agent-social-media-publishing-setup) shows how Cursor’s scope and approval model differ from the other confirmed paths.

## Choose project or global configuration deliberately

Cursor’s [official MCP documentation](https://cursor.com/docs/mcp) documents two configuration locations:

- `.cursor/mcp.json` for a project
- `~/.cursor/mcp.json` for the user’s global Cursor environment

Project scope makes sense when the server and its intended use are part of a reviewed repository workflow. It is also a source-control boundary. Keep bearer tokens and key-bearing URLs out of committed files. Review the proposed configuration before sharing the project, and document which team members should connect with their own credentials.

Global scope fits an operator who uses the same publishing connection across several projects. It keeps the definition out of individual repositories, though the server may then appear in contexts where nobody expected to publish. Record that the global server exists and keep tool enablement narrow.

Whichever scope you choose, write down four facts:

| Decision | Record |
| --- | --- |
| Scope | Project or global |
| Owner | Person allowed to change the server definition |
| Authentication | OAuth or the protected fallback used by this environment |
| Write policy | Which operations require approval and who may approve them |

The scope determines where Cursor discovers the server. It does not grant permission for every post in that project.

## Add Groniz as a remote MCP server

The remote MCP endpoint is:

```text
https://mcp.groniz.com/mcp
```

Cursor supports remote MCP, including Streamable HTTP and OAuth. Follow the current form in the official Cursor documentation, select its documented remote HTTP transport, and prefer OAuth when offered. That keeps a reusable credential out of the repository and prompt.

Groniz MCP can also authenticate with an `Authorization: Bearer YOUR_API_KEY` header or with a key embedded in the endpoint URL. If OAuth cannot be used in the intended Cursor environment, choose one of those supported methods only through Cursor’s current protected credential mechanism. The issuance location for fallback keys is [Groniz Connectors API keys](https://groniz.com/console/connectors/api-keys). Never copy a real value into `.cursor/mcp.json`, a chat message, a screenshot, or a log. Treat a key-bearing URL as a credential too.

After connecting, confirm that Cursor shows the intended Groniz endpoint. Successful authentication proves that the client and server can communicate. It says nothing yet about which social account is connected or whether a post is approved.

## Keep the publishing tools reviewable

Cursor lets users enable and disable MCP tools. Its agent asks for approval by default before running them. Preserve that boundary for publishing writes.

Keep auto-run off by default for tools that can create or schedule a public post. A read tool that lists integrations has a different consequence from a write that publishes immediately. Limit the agent's available tools to the work at hand, and disable publishing tools when the task does not need them.

Use this Cursor configuration and trust checklist as the original setup asset:

```markdown
### Cursor configuration and trust checklist

- [ ] The source packet has a stable approved version.
- [ ] The MCP server is in the intended project or global scope.
- [ ] The server URL is exactly `https://mcp.groniz.com/mcp`.
- [ ] OAuth is used when available.
- [ ] No real key appears in repository files, prompts, screenshots, or logs.
- [ ] The operator reviewed the server identity before enabling tools.
- [ ] Only the tools needed for this run are enabled.
- [ ] Publishing and scheduling writes retain an approval prompt.
- [ ] Auto-run is not the default for social write tools.
- [ ] The exact destination and final payload require separate human approval.
```

Connection trust, tool enablement, and post approval are separate decisions. This prevents a one-time infrastructure choice from becoming standing permission for future content. The [human-approval policy guide](https://groniz.com/blog/human-approval-ai-social-posts) shows how to bind approval to risk and content version.

## Inspect the live destination before building the write

Ask Cursor to start with the connected server’s read capabilities. The sequence is:

```text
discover available tools
→ list connected integrations
→ select the exact account or page
→ inspect its current required settings
→ prepare a destination-specific payload
```

Do not ask for "the company social account" if several profiles or Pages are connected. Put a human-readable account label beside the integration reference and have the reviewer confirm both.

The live settings are authoritative. Groniz handles provider OAuth, per-platform formatting, and delivery to 32+ networks, but it does not expose identical fields, media, analytics, or scheduling for every provider. Avoid copying provider-specific fields from a blog example into the tool call. Let Cursor inspect what the selected connection currently requires.

If the approved packet includes media, upload it before the post is created or scheduled. Confirm the upload completed and associate the returned reference with the correct destination. Keep media order and any supported destination settings in the final review.

## Present one exact approval view

Before Cursor invokes the write tool, have it present the complete proposal without credentials:

```markdown
Source version:
Network and connected account:
Final text and links:
Disclosure:
Uploaded media references and order:
Live destination settings:
Publish now or schedule:
Local time and named timezone:
Exact timestamp with offset:
Requested write operation:
```

The reviewer confirms facts, rights, disclosure, destination, payload, media, and time together. If Cursor edits any of them after approval, stop and obtain a new approval. A general instruction such as "you can publish launch updates" is not approval for this exact send.

Cursor can assemble and check the packet. Groniz can format and deliver it through the selected integration. The account owner still decides whether to publish.

## Verify the first delivery without duplicating it

Invoke the approved write once. Record the submission time, integration, payload version, response state, and returned post or scheduled-record ID. If the request is scheduled, compare the stored time with the approved local time, timezone, and offset. If it is immediate, check the supported delivery state and public destination when a public result is available.

A response timeout is not proof of failure. Cursor may lose the result after the server or provider accepted the request. In that case, inspect the available post records and the intended account before doing anything else. Classify the run as unknown while reconciliation is in progress. Retry only when non-delivery is established; if the payload or timing changes during correction, approve it again.

Keep the verification note compact:

```markdown
Submitted once at:
Post or scheduled-record ID:
Accepted state:
Destination evidence:
Verified at:
Unknown-outcome reconciliation, if any:
```

Keep this record with the approved source packet. It shows that the team used a reviewed operational path, but reach, engagement, leads, sales, and revenue remain outside that evidence.

Once the approved source packet and Cursor trust checklist are complete, [connect the reviewed workflow through Groniz Connectors](https://groniz.com/console/connectors).
