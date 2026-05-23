# Publishing to AUR

## Prerequisites

- An [AUR account](https://aur.archlinux.org/register)
- SSH key added to your AUR account
- `base-devel` and `go` installed locally

## Initial Setup

```sh
# Clone the (empty) AUR package repo
git clone ssh://aur@aur.archlinux.org/pinentry-dms.git
cd pinentry-dms

# Copy package files from this repo
cp /path/to/DankPinentry/aur/PKGBUILD .
```

## Build & Verify

```sh
# Test the build locally
makepkg -si

# Generate .SRCINFO (required by AUR)
makepkg --printsrcinfo > .SRCINFO
```

## Publish

```sh
git add PKGBUILD .SRCINFO
git commit -m "pinentry-dms 0.1.0"
git push
```

## Updating the Package

1. Tag a new release on GitHub (`v<new_version>`)
2. Update `pkgver` and `pkgrel` in `PKGBUILD`
3. Run `updpkgsums` to refresh `sha256sums`
4. Rebuild locally with `makepkg -si` to verify
5. Regenerate `.SRCINFO` and push

## Notes

- `sha256sums=('SKIP')` is acceptable during development; run `updpkgsums` before publishing to AUR
- The source URL expects a GitHub tag matching `v${pkgver}` — ensure the tag exists before publishing
- `provides=('pinentry')` allows this package to satisfy pinentry dependencies system-wide
