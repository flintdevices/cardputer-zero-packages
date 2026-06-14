# CardputerZero Packages

APT repository for CardputerZero applications.

- `.deb` files stored in git via LFS
- CI auto-generates APT index and deploys to GitHub Pages
- Optional Aliyun OSS mirror lives under `oss/` and is disabled by default
- CN AppStore registry is generated at the OSS mirror when OSS sync is enabled
- Users download via Pages CDN (100GB/month bandwidth)

## Usage on device

```bash
echo "deb [trusted=yes] https://cardputerzero.github.io/packages stable main" | sudo tee /etc/apt/sources.list.d/cardputerzero.list
sudo apt update
sudo apt install nc2000 lofibox
```

## Adding a package

1. Place the `.deb` file in `pool/main/<package-name>/`
2. Push to `main` branch
3. CI will auto-regenerate APT index and deploy to Pages

## Structure

```
pool/main/<pkg>/<pkg>_<ver>_<arch>.deb   ← LFS-tracked binaries (source of truth)
public/                                  ← built by CI, deployed to GitHub Pages
  ├── pool/...                           ← deb files served via CDN
  └── dists/stable/main/binary-arm64/    ← APT metadata
```
