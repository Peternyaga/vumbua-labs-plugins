# Vumbua Labs plugins

The shared Git-backed **Vumbua Labs** marketplace for Codex. This repository holds the marketplace catalog and installable plugin packages; each product has its own source repository and service.

| Plugin | Plugin ID | Service | Guide |
| --- | --- | --- | --- |
| Timeline Curator | `timeline-curator` | https://curator.vumbualabs.com | [Tester guide](docs/external-testing.md) |
| Fieldwork Reach | `sales-workspace-hosted` | https://reach.vumbualabs.com | [Tester guide](docs/fieldwork-reach-testing.md) |

## Add the shared marketplace

```powershell
codex plugin marketplace add Peternyaga/vumbua-labs-plugins --ref main
```

Then install the product you want:

```powershell
codex plugin add sales-workspace-hosted@vumbua-labs
# Or, for Timeline Curator:
codex plugin add timeline-curator@vumbua-labs
```

Restart Codex desktop and open a new chat. Each plugin requires its own product account and OAuth approval; marketplace installation does not grant access to another person's data. Background workers require their separate setup permissions.

## Update

```powershell
codex plugin marketplace upgrade vumbua-labs
codex plugin add sales-workspace-hosted@vumbua-labs
# For an installed Timeline plugin:
codex plugin add timeline-curator@vumbua-labs
```

## Existing installations

If you added Vumbua Labs using a product repository previously, replace its source registration first:

```powershell
codex plugin marketplace remove vumbua-labs
codex plugin marketplace add Peternyaga/vumbua-labs-plugins --ref main
```

This removes the old marketplace source registration; do not use `codex plugin remove`. The shared catalog retains the same `vumbua-labs` marketplace identity. Plugin identifiers, server names, scopes and service endpoints are retained. Refresh your installed plugin with `codex plugin add`, restart desktop and verify an authenticated read. Keep existing OAuth connections and poller credentials; reauthenticate only if the connection is missing or permissions require it. See the Fieldwork package README for preserving an existing Windows poller.

## Maintaining this catalog

The catalog is `.agents/plugins/marketplace.json`. Its name stays `vumbua-labs`; package paths are relative to this repository root. Update a package's version when changing bundled metadata, skills or scripts. Keep product server implementation in the product repository and exclude credentials, customer records, poller state and generated archives from this repository.
