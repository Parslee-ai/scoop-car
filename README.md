# Install CAR on Windows

**Common Agent Runtime (CAR)** — a deterministic execution layer for AI agents.
This is the official [Scoop](https://scoop.sh) bucket for installing the CAR
CLI and server on Windows.

## 30-second install

Open **PowerShell** (Windows PowerShell 5.1 or PowerShell 7+ — *not* `cmd.exe`,
and *not* a WSL/Linux shell) and paste:

```powershell
# 1. Install Scoop itself (skip if you already have it)
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression

# 2. Add the CAR bucket and install
scoop bucket add car https://github.com/Parslee-ai/scoop-car
scoop install car
```

That's it. `car` is now on your `PATH`. Confirm:

```powershell
car --version
```

> **Heads-up:** the binaries are not yet code-signed, so on first run Windows
> SmartScreen may warn ("Windows protected your PC"). Choose **More info →
> Run anyway**. Signing is in progress —
> see [Parslee-ai/car#248](https://github.com/Parslee-ai/car/issues/248).

## What's next

```powershell
car info        # what CAR detected on this machine (hardware, models)
car init        # scaffold a .car/ project directory in the current folder
car --help      # full command list
```

For the getting-started flow, cookbook examples (Python / Node / web), and the
full docs, see **[Parslee-ai/car-releases](https://github.com/Parslee-ai/car-releases)**.

---

## What is Scoop?

[Scoop](https://scoop.sh) is a command-line installer for Windows — think
`apt` or `brew`, but for Windows. It installs apps into your user profile, so
it **needs no administrator rights**, doesn't touch the registry, and
uninstalls cleanly. It runs in PowerShell. If you've never used it, the
two-step install above sets it up for you.

A *bucket* is just a collection of app manifests Scoop can install from. This
repo is the bucket for CAR.

## What gets installed

`scoop install car` puts three binaries on your `PATH`:

| Binary | Purpose |
|--------|---------|
| `car.exe` | The CLI |
| `car-server.exe` | WebSocket server exposing the runtime over JSON-RPC |
| `car-memgine-eval.exe` | StateBench evaluation bridge |

Supported platform: **Windows x64**.

## Language bindings (Node.js / Python)

This bucket ships only the CLI + server. For the language bindings, use the
native package managers instead:

- **Node.js:** `npm install car-runtime`
- **Python:** `pip install car-runtime`

## Upgrade

```powershell
scoop update car
```

`autoupdate` is configured, so the bucket picks up new CAR releases
automatically.

## Uninstall

```powershell
scoop uninstall car
scoop bucket rm car
```

## License

This bucket (the `bucket/car.json` manifest and the contents of this repo) is
licensed under **Apache-2.0** — see [`LICENSE`](./LICENSE).

The CAR **binaries** it installs are under a separate license: free for use
and unmodified redistribution, modification forbidden. See the
[releases repo](https://github.com/Parslee-ai/car-releases/blob/main/LICENSE)
for the binary license terms.
