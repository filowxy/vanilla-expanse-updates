# vanilla-expanse-updates

Update check metadata for the **Vanilla Expense** Minecraft modpack (NeoForge 1.21.1).

Consumed by [modpack-update-checker](https://modrinth.com/mod/modpack-update-checker) when Minecraft starts.

## Layout

- `meta.json` — version index (array of released versions, newest at end of array is treated as latest by some clients; this mod picks the **last** entry)
- `versions/<id>/changelog.txt` — human-readable changelog shown in-game for that version
- `id` in `meta.json` must match a folder name under `versions/`

## Adding a new version

1. Append a new object to the `versions` array in `meta.json`:
   ```json
   {
     "id": "1.0.0",
     "releasedAt": 1782200000000,
     "promotions": {
       "downloads": {
         "modrinth": "https://modrinth.com/modpack/vanilla-expanse/version/1.0.0",
         "curseforge": null,
         "generic": null
       }
     },
     "updateType": "minor"
   }
   ```
   `updateType` can be `minor`, `minor_breaking`, `major`, or `incompatible`.

2. Create `versions/1.0.0/changelog.txt` with the changelog body.

3. In the modpack's `config/modpack-update-checker/config.json`, bump `currentVersion` to `1.0.0`.

## Timestamp

`releasedAt` is **milliseconds since 1970-01-01 00:00:00 UTC** (Unix epoch in ms). One quick way to get it:

```python
import time
int(time.time() * 1000)
```

Or in PowerShell:

```powershell
[DateTimeOffset]::UtcNow.ToUnixTimeMilliseconds()
```
