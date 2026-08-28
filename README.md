# updates.meshrunner.dev

The static tree deployed relays fetch their updates from — signed
manifests only, never binaries. The binaries live in release assets;
each channel's `manifest.json` names them by URL and sha256, and the
`.minisig` beside it is what a relay actually trusts.

```
CNAME                          the Pages domain
lotor/channels.json            which channels are published
lotor/<channel>/manifest.json  one channel's current statement
lotor/<channel>/…minisig       its signature(s)
```

Nothing here is edited by hand: the lotor repository's workflows push
manifests through a deploy key, and sweep the stale try channels on a
schedule. Verification happens on the relays, against keys pinned per
release train — this repository only hosts.

Leaving GitHub one day is an rsync of this tree to any static host,
and fresh manifests pointing at new artifact URLs. No deployed relay
changes.
