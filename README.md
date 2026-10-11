# Ollama with VS Code

This workspace documents how to run Ollama with VS Code on Windows, macOS, or
Linux. Install Ollama as a normal application/service and keep downloaded model
files outside this Git repository.

## VS Code setup (all platforms)

1. Install VS Code 1.127 or newer and install Ollama for your operating system
   using the steps below.
2. Open this folder in VS Code. The workspace recommends the
   [Ollama extension](https://marketplace.visualstudio.com/items?itemName=Ollama.ollama);
   accept the recommendation, or install the extension from the Marketplace.
   Ollama 0.17.6 or newer is recommended.
3. Pull a model in a terminal, replacing the example with a model you want:

   ```text
   ollama pull <model-name>
   ollama list
   ```

   Cloud models additionally require `ollama signin`.
4. Open VS Code Chat, use the model picker, and select a model in the **Ollama**
   section. The extension discovers models from the local Ollama server at
   `http://127.0.0.1:11434` by default.

If models do not appear, confirm Ollama is running and `ollama list` shows the
model, then run **Ollama: Refresh Models** or **Ollama: Diagnose Models** from
the VS Code Command Palette.

## Windows

Install Ollama from [ollama.com/download](https://ollama.com/download). The
native app runs in the background and makes the `ollama` command available in
PowerShell and other terminals.

Default locations:

| Data | Default location |
| --- | --- |
| Application | `%LOCALAPPDATA%\Programs\Ollama` |
| Downloaded models and configuration | `%USERPROFILE%\.ollama` |
| Logs and update data | `%LOCALAPPDATA%\Ollama` |

To store models somewhere else, set the user environment variable
`OLLAMA_MODELS` to a directory outside this repository, then quit and relaunch
Ollama.

## macOS

Ollama requires macOS Sonoma (14) or newer. Apple silicon supports CPU and GPU
use; Intel Macs are CPU-only. Download and open the
[Ollama macOS app](https://ollama.com/download), then move it to Applications.
On first launch, allow it to add the `ollama` command to your PATH if prompted.

Models and configuration are under `~/.ollama` by default; logs are in
`~/.ollama/logs`. To change the model location, configure `OLLAMA_MODELS` for
the account running Ollama and restart the app.

## Linux

Install using the official script:

```sh
curl -fsSL https://ollama.com/install.sh | sh
```

The script installs Ollama and configures a systemd service on supported
systems. Start and check it with:

```sh
sudo systemctl start ollama
sudo systemctl status ollama
ollama pull <model-name>
ollama list
```

For a manual install, ARM64, AMD ROCm, driver requirements, or service
customization, see the official Linux guide. For a system service, model files
are associated with the service account (commonly `/usr/share/ollama/.ollama`
for the documented service setup); an interactive/user-run installation uses
that user's home directory, usually `~/.ollama`. Set `OLLAMA_MODELS` in the
service environment or user environment to relocate model files, then restart
the service or app.

## Keep machine data out of Git

Ollama itself, its configuration, model files, and VS Code user settings are
managed outside this workspace. Model weights can require tens or hundreds of
gigabytes. Keep model storage outside this repository; `.gitignore` also
excludes common local model folders, `.gguf` files, and environment files.
Do not commit credentials or machine-specific paths.

## References

- [Ollama: VS Code integration](https://docs.ollama.com/integrations/vscode)
- [Ollama for Windows](https://docs.ollama.com/windows)
- [Ollama for macOS](https://docs.ollama.com/macos)
- [Ollama for Linux](https://docs.ollama.com/linux)
- [VS Code Marketplace: Ollama extension](https://marketplace.visualstudio.com/items?itemName=Ollama.ollama)
