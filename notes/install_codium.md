# Install Codium

```bash
sudo dnf install libXScrnSaver
```

```bash
curl -sLO https://github.com/VSCodium/vscodium/releases/download/1.42.1/VSCodium-linux-arm64-1.42.1.tar.gz
```

```bash
mkdir -p /usr/local/codium
```

```bash
sudo tar -C /usr/local/codium -xzvf VSCodium-linux-arm64-1.42.1.tar.gz
```

```bash
cd /usr/local/bin
sudo ln -sf ../codium/bin/codium .
```
