# Fieldwork Reach for Codex — 0.4.6

Connect to https://reach.vumbualabs.com/mcp using OAuth. Manage accessible leads and internal tasks, correct eleven profile fields with provenance and retained history, and process queued work with guarded reversal. Version 0.4.5 adds optional, individually authorized lead email through each user's connected SMTP mailbox. No calls or external calendar events are made. This version is local source until you publish it; the installed marketplace version remains unchanged.

## Install

Add the existing Vumbua Labs marketplace and install the hosted plugin:

```powershell
codex plugin marketplace add Peternyaga/vumbua-labs-plugins --ref main
codex plugin add sales-workspace-hosted@vumbua-labs
```

Restart Codex desktop, open a new chat and connect Fieldwork Reach to your own Fieldwork account. If linking was not offered, run `codex mcp login fieldwork`. Approve only the scopes you need: `leads:read`, `leads:write`, `tasks:write`, and, if you want explicitly authorized agent email, `email:send`. Each person must connect an SMTP mailbox in Fieldwork separately. Ask the plugin to read your current follow-ups to verify the connection. A Fieldwork owner must provision your account; installing the plugin does not create an account or grant access to other workspaces.

## Update

```powershell
codex plugin marketplace upgrade vumbua-labs
codex plugin add sales-workspace-hosted@vumbua-labs
```

Restart Codex desktop and test in a new chat. Reapprove OAuth only if the existing connection is missing or lacks the requested scopes. Server tool changes are discovered from the hosted MCP endpoint; bundled skill/script changes require refreshing the plugin package.

## Release 0.4.6

The Windows poller now resolves the current Codex executable each time it runs. This prevents a desktop-app update from leaving the poller pointed at a removed versioned `codex.exe` path. Re-running `scripts/install-poller.ps1 -Accept -WorkspaceRoot <your existing workspace>` copies the repaired script while preserving the existing pairing and schedule.

## Release 0.4.5

The poller treats authenticated notes as requests for safe internal work, investigates research requests before reporting a blocker, uses the workspace timezone and open internal slots for broad follow-up windows, and avoids recursively queueing agent-authored notes. The new `list_agent_reports` tool helps it inspect prior outcomes. Email sending needs both `email:send` OAuth permission and the lead-specific task checkbox; ordinary notes never authorize outbound email. Publish the server upgrade before refreshing this plugin; the older server does not expose these tools or permission.

## Migrate from fieldwork-local

Install the marketplace package first. Disable `sales-workspace-hosted@fieldwork-local` after the marketplace copy is enabled to avoid duplicate tools. Both packages use the same `fieldwork` server name, HTTPS endpoint and scopes; preserve the existing connection and verify a read before reauthenticating. Do not log out or revoke the existing grant just to change package source.

The optional Windows poller is separate from OAuth. Keep the `.fieldwork-reach` directory and the existing `Fieldwork Reach Poller` scheduled task. Run the new package's `scripts/install-poller.ps1 -Accept -WorkspaceRoot <your existing workspace>` to update its script; when that task and credential exist, the installer preserves pairing. For first-time installation, invoke the setup skill to review permissions and approve pairing in Reach. The poller runs only while the configured Windows user is signed in and the machine is online; work remains queued while offline.

## Release 0.4.2

The optional Windows poller now launches without a visible console. Running the installer again updates an existing scheduled task while preserving its pairing, account, and schedule.

## Release 0.4.1

Moves distribution to the dedicated Vumbua Labs catalog while retaining the same plugin identity and OAuth endpoint. Includes the dedicated lead-profile skill, updated queue correction/recovery guidance and a poller prompt that invokes that workflow. Profile fields: phone, email, website, Facebook, Instagram, LinkedIn, name, organisation, contact role, location and source. Each tool requires current version and factual provenance. Historical values are retained. Ambiguous evidence needs review.

Source: [Fieldwork sales workspace](https://github.com/Peternyaga/fieldwork-sales-workspace/tree/main/sales-workspace-hosted). Distribution: [Vumbua Labs](https://github.com/Peternyaga/vumbua-labs-plugins/tree/main/plugins/sales-workspace-hosted).
