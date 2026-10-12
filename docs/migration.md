# Shared catalog migration

Vumbua Labs now has a product-independent GitHub address: `Peternyaga/vumbua-labs-plugins`. The marketplace name remains `vumbua-labs`, and existing plugin IDs and OAuth endpoints are unchanged.

```powershell
codex plugin marketplace remove vumbua-labs
codex plugin marketplace add Peternyaga/vumbua-labs-plugins --ref main
codex plugin marketplace upgrade vumbua-labs
codex plugin add sales-workspace-hosted@vumbua-labs
# If Timeline Curator is installed:
codex plugin add timeline-curator@vumbua-labs
```

Restart desktop and open a new chat. Do not remove the installed plugin, revoke OAuth or delete poller state just to change catalog source. Existing users must update their marketplace source once; the old catalog location is retired. New users use only this shared catalog address.
