# nvsw (Neovim Version Switcher)

**Neovim Version Switcher** – Easily install, switch, and manage multiple versions of Neovim like a boss 🚀

[![GitHub release](https://img.shields.io/github/release/y3owk1n/nvsw.svg)](https://github.com/y3owk1n/nvsw/releases) [![License](https://img.shields.io/github/license/y3owk1n/nvsw.svg)](LICENSE)

## 👀 Overview

**nvsw** (Neovim Version Switcher) is a lightweight cross-platform (maybe, only tested on mac) CLI tool written in Go 🏗️ that makes it super easy to install, switch between, and manage multiple versions of Neovim on your machine. Whether you’re testing a cutting‑edge nightly build 🌙 or sticking with the stable release 🔒, nvsw has got your back!

> [!note]
> I only have a mac and it's working perfectly fine for my use case. If it's not working for other OS, feel free to help fixing that or share it as an issue. I'll try to look into it.

## 🌟 Features

- **Easy Installation:**
  Download and install Neovim versions directly from GitHub with a single command.
- **Version Switching:**
  Switch between installed versions in a snap. nvsw updates a global symlink so your preferred version is always just a command away.
- **Remote Version Listing:**
  List all available remote releases (stable, nightly, etc.) with cached results to avoid GitHub rate limits ⚡. Need fresh data? Just add the `force` flag.
- **Uninstallation & Reset:**
  Remove individual versions or reset your entire configuration with ease. (Full cleanup? See the caveats! ⚠️)
- **Cross-Platform (Maybe):**
  Works on macOS (Intel & Apple Silicon), Linux, and Windows. (Maybe, not exactly tested yet, as i only have a mac)
- **Global Symlink Management:**
  Automatically creates a consistent global binary in `~/.nvsw/bin` for a seamless experience.

---

## 🚀 Installation

### From Source

Make sure you have [Go](https://golang.org/dl/) (v1.23 or later) installed. Then run:

```bash
git clone https://github.com/y3owk1n/nvsw.git
cd nvsw
mkdir -p build
# Build for darwin-arm64.
env GOOS=darwin GOARCH=arm64 go build -ldflags "-X main.Version=local-build" -o ./build/nvsw-darwin-arm64 ./main.go
# Build for darwin-amd64.
env GOOS=darwin GOARCH=amd64 go build -ldflags "-X main.Version=local-build" -o ./build/nvsw-darwin-amd64 ./main.go
# Build for linux-amd64.
env GOOS=linux GOARCH=amd64 go build -ldflags "-X main.Version=local-build" -o ./build/nvsw-linux-amd64 ./main.go
# Build for windows-amd64.
env GOOS=windows GOARCH=amd64 go build -ldflags "-X main.Version=local-build" -o ./build/nvsw-windows-amd64.exe ./main.go
````

Move the binary to your PATH or run it directly.

### Homebrew

Install nvsw via Homebrew! Simply add our tap:

```bash
brew tap y3owk1n/tap
```

Then install with:

```bash
brew install y3owk1n/tap/nvsw
```

## 💻 Usage

**nvsw** uses a clean subcommand interface. Run nvsw --help for full details.

> [!note]
> Remember to add `nvws` to your path. See next section about how.

### Commands

#### install

Install a specific Neovim version.

```bash
nvsw install stable    # Install the latest stable release 🔒
nvsw install nightly   # Install the latest nightly release 🌙
nvsw install v0.10.3   # Install a specific version
```

#### use

Switch to a particular version. This updates a global symlink in ~/.nvsw/bin so that you can simply run nvim.

```bash
nvsw use stable
nvsw use nightly
nvsw use v0.10.3
```

#### list

List installed versions.

```bash
nvsw list
```

#### list-remote

List available remote releases (cached for 5 minutes to avoid rate limiting). Use the force flag to refresh the cache.

```bash
nvsw list-remote
nvsw list-remote force
```

#### current

Display the currently active Neovim version.

```bash
nvsw current
```

#### uninstall

Uninstall an installed version.

```bash
nvsw uninstall stable
nvsw uninstall nightly
nvsw uninstall v0.10.3
```

#### reset

Reset to factory state.

> [!warning]
> This command deletes the entire nvsw configuration (removes ~/.nvsw, including downloaded versions, symlinks, and cache). Use with caution.

```bash
nvsw reset
```

## 🔗 Adding nvsw to Your PATH

To easily run the Neovim binary provided by nvsw, you need to add the global bin directory (`~/.nvms/bin`) to your PATH. Below are instructions for common shells:

### Bash

Add the following line to your `~/.bashrc` (or `~/.bash_profile` on macOS):

```bash
export PATH="$HOME/.nvms/bin:$PATH"
```

Then, reload your configuration:

```bash
source ~/.bashrc   # or source ~/.bash_profile
```

### Zsh

Add the following line to your `~/.zshrc`:

```bash
export PATH="$HOME/.nvms/bin:$PATH"
```

Then, reload your configuration:

```bash
source ~/.zshrc
```

### Fish

Add the following line to your `~/.config/fish/config.fish`:

```bash
set -gx PATH $HOME/.nvms/bin $PATH
```

Then, reload your configuration:

```bash
source ~/.config/fish/config.fish
```

## Shell Completions 🧩

nvsw supports generating shell completions using Cobra’s built‐in functionality. You can easily enable command completions for your favorite shell by following the instructions below.

### Bash

To enable Bash completions, add the following line to your `~/.bashrc` (or `~/.bash_profile` on macOS):

```bash
source <(nvsw completion bash)
```

Then, reload your configuration:

```bash
source ~/.bashrc   # or source ~/.bash_profile
```

### Zsh

For Zsh users, first ensure that completion is enabled by adding the following to your ~/.zshrc (if not already present):

```bash
autoload -U compinit && compinit
```

Then add the following line to generate and load nvsw completions:

```bash
source <(nvsw completion zsh)
```

Then, reload your configuration:

```bash
source ~/.zshrc
```

### Fish

Fish shell users can generate completions with:

```bash
nvsw completion fish | source
```

To make the completions permanent, save them to your completions directory:

```bash
nvsw completion fish > ~/.config/fish/completions/nvsw.fish
```

Then, reload your configuration:

```bash
source ~/.config/fish/config.fish
```

## Configuration & Data 📂

**nvsw** stores its configuration, downloaded versions, and cache in the ~/.nvsw directory.

> [!note]
> Remember: Homebrew will not delete this directory upon uninstallation, you must delete it manually if you want a full cleanup.

## 🤝C ontributing

Contributions are always welcome! Here's how you can help:

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to your branch
5. Open a pull request

## 📄 License

This project is licensed under the MIT License. Feel free to use, modify, and distribute it as you see fit.

Enjoy using nvsw, and may your Neovim sessions be ever lit! ✨
