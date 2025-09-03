# Bitwarden CLI Backup

```sh
bw login --apikey
BW_SESSION=$(bw unlock "$BW_PASSWORD" --raw)
bw sync --session "$BW_SESSION"
bw export --session "$BW_SESSION" --format encrypted_json \
  --password "$EXPORT_PASSWORD" \
  --output "/data/bitwarden-backup-$(date +%F).json"
bw lock --session "$BW_SESSION"
```

Will output filename:

```javascript
const timestamp = new Date().toISOString().slice(0, 10);
const filename = `/data/bitwarden-backup-${timestamp}.json`;
return [
  {
    json: {
      filePath: filename,
    },
  },
];
```
