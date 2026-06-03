# CAR on Windows

This is the official [Scoop](https://scoop.sh) bucket for the **Common
Agent Runtime (CAR)** — a deterministic execution layer for AI agents.
It installs the `car` CLI and the `car-server` daemon on Windows.

## Install

Open **PowerShell** (Windows 10/11 ships with it — search "PowerShell"
in the Start menu; **not** Command Prompt, **not** WSL) and paste:

```powershell
scoop bucket add car https://github.com/Parslee-ai/scoop-car
scoop install car
```

That's it — `car`, `car-server`, and `car-memgine-eval` are now on your
PATH.

> **First time with Scoop?** If `scoop` isn't recognized, install it
> first (one line, no admin rights needed):
>
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
> ```
>
> Scoop is a command-line installer for Windows. It installs apps into
> your user profile (no admin), keeps them on your PATH, and uninstalls
> them cleanly. [scoop.sh](https://scoop.sh)

> **SmartScreen warning?** The CAR binaries are not yet code-signed, so
> Windows may warn ("Windows protected your PC") the first time you run
> `car-server.exe`. Click **More info → Run anyway**. Code-signing is
> on the roadmap.

## First 60 seconds

```powershell
car info                          # what CAR detects on this machine
car-server --port 9100            # start the daemon (leave this running)
```

Then, in a **second** PowerShell window:

```powershell
car ui                            # opens the browser dashboard
```

The dashboard (served by the daemon at `http://127.0.0.1:9101/`) shows
your agents, pending approvals, available models, and memory. `car info`
also prints this URL.

To run a model, either pull a local one or sign in to Parslee's hosted
inference:

```powershell
car auth login parslee            # use Parslee's hosted models
# or browse and pull a local model:
car models list
```

Full getting-started docs and examples (Node, Python, web app) live at
[Parslee-ai/car-releases](https://github.com/Parslee-ai/car-releases).

## Start the daemon automatically on login (optional)

If you want `car-server` running every time you sign in, register a
login task. This is **opt-in** — paste it only if you want a
background daemon. It creates a shortcut in your Startup folder:

```powershell
$startup = [Environment]::GetFolderPath('Startup')
$carServer = (Get-Command car-server).Source
$wsh = New-Object -ComObject WScript.Shell
$lnk = $wsh.CreateShortcut("$startup\car-server.lnk")
$lnk.TargetPath = $carServer
$lnk.Arguments = "--port 9100"
$lnk.Save()
Write-Host "car-server will start on next login. Remove $startup\car-server.lnk to undo."
```

To stop it starting on login, delete the shortcut:

```powershell
Remove-Item "$([Environment]::GetFolderPath('Startup'))\car-server.lnk"
```

## Language bindings

This bucket ships the CLI + server only. For embedding CAR in code:

- **Node.js**: `npm install car-runtime`
- **Python**: `pip install car-runtime`

Both bundle the `car-server` binary too.

## Maintenance & troubleshooting

**Upgrade** (the bucket has `autoupdate`, so this picks up new releases):

```powershell
scoop update car
```

**Uninstall:**

```powershell
scoop uninstall car
scoop bucket rm car
```

**What's installed:**

- `car.exe` — the CLI (`car ui`, `car info`, `car infer`, `car models`, …)
- `car-server.exe` — the daemon: WebSocket JSON-RPC + the browser dashboard
- `car-memgine-eval.exe` — StateBench evaluation bridge

Supported: Windows x64.

## License

Binaries are free for use and unmodified redistribution; modification
forbidden. This bucket (the `.json` manifest) is Apache-2.0. See the
[releases repo](https://github.com/Parslee-ai/car-releases/blob/main/LICENSE)
for the binary license.
