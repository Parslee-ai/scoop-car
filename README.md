# Install CAR on Windows

The **Common Agent Runtime** (CAR) — a deterministic execution layer for AI
agents. This repo is the official [Scoop](https://scoop.sh) bucket that installs
the CAR CLI and server on Windows.

## Install — 30 seconds

Open **PowerShell** (Windows PowerShell 5.1 or [PowerShell 7+](https://aka.ms/powershell) — both work; **not** cmd.exe, **not** WSL) and run:

```powershell
# 1. Install Scoop itself, if you don't have it (skip if `scoop` already works)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

# 2. Add this bucket and install CAR
scoop bucket add car https://github.com/Parslee-ai/scoop-car
scoop install car
```

That's it. Verify:

```powershell
car --version
car info          # what CAR detects about this machine
```

## What's Scoop, and why?

[Scoop](https://scoop.sh) is a command-line installer for Windows — think
`apt`/`brew`, but for Windows. We use it because it:

- **needs no admin rights** — installs into your user profile
- **runs in any PowerShell** — no GUI, no UAC prompts
- **uninstalls cleanly** — one command, no leftovers
- **auto-updates** — `scoop update car` pulls each new CAR release

It's the lightest way to get a CLI tool onto Windows and keep it current.

> **Which shell?** Run every `scoop` and `car` command in **PowerShell**. The
> Scoop install script is PowerShell-only — it won't run in `cmd.exe`. And don't
> use WSL: that's a Linux environment with its own package managers; on Windows,
> Scoop is the path.

## Getting started — your first 60 seconds

After install, the binaries (`car`, `car-server`, `car-memgine-eval`) are on your
`PATH`. Start here:

```powershell
car info                 # show what CAR can do on this machine
car init                 # scaffold a .car\ project directory in the current folder
car --help               # full command list
```

**To actually run inference**, CAR needs a model. Two paths:

```powershell
# Option A — hosted Parslee models (requires a Parslee account)
car auth login parslee
car infer "Say hello in three words."

# Option B — a local CPU model (no account; downloads ~1 GB once)
car models pull qwen/qwen3-1.7b:q8_0
car infer "Say hello in three words."
```

> ⚠️ Running `car infer` on a **fresh install with no model and no auth** will
> fail — the default model chain has nothing to fall back to on Windows yet
> ([tracking issue](https://github.com/Parslee-ai/car/issues/231)). Run Option A
> or B first.

Cookbook examples (Python, Node, web app) live in the
[releases repo](https://github.com/Parslee-ai/car-releases).

## What got installed

```
car.exe               # the CLI
car-server.exe        # WebSocket/JSON-RPC server exposing the runtime
car-memgine-eval.exe  # StateBench evaluation bridge
```

Supported: **Windows x64**.

## Upgrade & uninstall

```powershell
scoop update car        # upgrade to the latest release (autoupdate is on)
scoop uninstall car     # remove the binaries
scoop bucket rm car     # remove the bucket
```

## Other languages

This bucket ships the CLI + server only. For language bindings:

- **Node.js**: `npm install car-runtime`
- **Python**: `pip install car-runtime`

Full docs: [Parslee-ai/car-releases](https://github.com/Parslee-ai/car-releases).

## License

Binaries are free for use and unmodified redistribution; modification forbidden.
This bucket (the `.json` manifest) is Apache-2.0. See the
[releases repo](https://github.com/Parslee-ai/car-releases/blob/main/LICENSE) for
the binary license.
