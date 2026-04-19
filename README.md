# Scoop bucket for Common Agent Runtime

Official [Scoop](https://scoop.sh) bucket for the CAR CLI on Windows.

## Install

```powershell
scoop bucket add car https://github.com/Parslee-ai/scoop-car
scoop install car
```

Installs three binaries into your `$PATH`:

- `car.exe` — the CLI
- `car-server.exe` — WebSocket server exposing the runtime over JSON-RPC
- `car-memgine-eval.exe` — StateBench evaluation bridge

Supported: Windows x64.

## Upgrade

```powershell
scoop update car
```

`autoupdate` is configured, so `scoop bucket update` picks up new releases
automatically.

## Uninstall

```powershell
scoop uninstall car
scoop bucket rm car
```

## Node.js / Python bindings

This bucket only ships the CLI + server. For language bindings:

- **Node.js**: `npm install car-runtime`
- **Python**: `pip install car-runtime`

See https://github.com/Parslee-ai/car-releases for full docs.

## License

Binaries are free for use and unmodified redistribution; modification
forbidden. This bucket (the `.json` manifest) is Apache-2.0. See the
[releases repo](https://github.com/Parslee-ai/car-releases/blob/main/LICENSE)
for the binary license.
