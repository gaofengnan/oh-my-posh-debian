# oh-my-posh-debian

> Fork of [dariogriffo/oh-my-posh-debian](https://github.com/dariogriffo/oh-my-posh-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

Debian and Ubuntu packaging for [oh-my-posh](https://ohmyposh.dev) — a prompt
theme engine for any shell. Each package ships the `oh-my-posh` binary **and
every built-in theme** under `/usr/share/oh-my-posh/themes/`.

Packages are built automatically from official upstream releases (usually
within hours) and served from **[deb.gaofn.xyz](https://deb.gaofn.xyz)** for
Debian (bookworm, trixie, forky, sid) and Ubuntu (jammy, noble, questing,
resolute) on amd64, arm64 and armhf.

## Install

```bash
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.gpg -o /etc/apt/keyrings/deb.gaofn.xyz.gpg
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.sources -o /etc/apt/sources.list.d/deb.gaofn.xyz.sources
# Debian 12 (bookworm): fetch deb.gaofn.xyz-bookworm.sources instead
sudo apt update
sudo apt install -y oh-my-posh
```

Then initialize it in your shell, e.g. for bash:

```bash
eval "$(oh-my-posh init bash --config /usr/share/oh-my-posh/themes/jandedobbeleer.omp.json)"
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/gaofengnan/oh-my-posh-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```

## How it works

- `check-upstream.yml` polls upstream hourly; a new release dispatches `release.yml`.
- `release.yml` builds binary packages (Docker, per suite × architecture, binary +
  themes from the upstream release assets) and source packages (`.dsc`, from the
  upstream source tarball), then publishes everything as a GitHub release tagged
  `<version>+<build>`.
- The deb.gaofn.xyz mirror ingests published releases automatically.

Manual build: `./build.sh <version> <build> [arch|all]` (e.g. `./build.sh 29.28.0 1 all`).

## Links

- Upstream: https://github.com/JanDeDobbeleer/oh-my-posh
- Repository: https://deb.gaofn.xyz
