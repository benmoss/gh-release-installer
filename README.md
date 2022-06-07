# gh-release-installer

A (relatively) simple tool for downloading/installing artifacts from GitHub
releases. Kinda like a package manager, sorta.

## Usage

### Installing dependencies
```
❯ gh-release-installer install --config examples/sigstore.yml -d /tmp/sigstore
2022/06/07 11:55:14 dependencies.go:183: gitsign downloaded
2022/06/07 11:55:14 dependencies.go:194: gitsign validated
2022/06/07 11:55:17 dependencies.go:183: cosign downloaded
2022/06/07 11:55:18 dependencies.go:194: cosign validated
```

### Fix/sync checksums
This can be useful if you add a new os/arch or change a version manually, just
run `update-checksums` and let the tool do the work of filling out the
checksums.

```
❯ gh-release-installer update-checksums --config examples/sigstore.yml
2022/06/07 12:02:34 dependencies.go:409: gitsign v0.1.0 linux/amd64 checksum synced
2022/06/07 12:02:50 dependencies.go:409: gitsign v0.1.0 linux/arm64 checksum synced
2022/06/07 12:02:51 dependencies.go:409: cosign v1.8.0 darwin/amd64 checksum synced
2022/06/07 12:03:04 dependencies.go:409: cosign v1.8.0 linux/amd64 checksum synced
```

### Automatic updates
We can check for new releases and automatically update the versions and checksums!

```
❯ go run ./ update --config examples/sigstore.yml
2022/06/07 12:04:42 dependencies.go:363: gitsign is already at latest version 0.1.0
2022/06/07 12:04:42 dependencies.go:366: Updating cosign to 1.9.0
2022/06/07 12:04:49 dependencies.go:409: cosign v1.9.0 darwin/amd64 checksum synced
2022/06/07 12:04:55 dependencies.go:409: cosign v1.9.0 linux/amd64 checksum synced
```
