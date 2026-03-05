# AI Bot Auto-Build Docker Image

Automated daily builds of an Arch Linux Docker image with popular AI coding assistants pre-installed.

## Included Tools

- **openai-codex-bin** - OpenAI Codex CLI
- **gemini-cli-git** - Google Gemini CLI (built from source)
- **claude-code** - Anthropic Claude Code CLI
- **opencode-bin** - OpenCode AI assistant

## Usage

### Pull from GitHub Container Registry

```bash
docker pull ghcr.io/chmouel/agents-image:latest
```

### Run the container

```bash
docker run -it ghcr.io/chmouel/agents-image:latest
```

### Run a specific tool

```bash
# Run Codex
docker run -it ghcr.io/chmouel/agents-image:latest codex --help

# Run Gemini
docker run -it ghcr.io/chmouel/agents-image:latest gemini --help

# Run Claude
docker run -it ghcr.io/chmouel/agents-image:latest claude --help

# Run OpenCode
docker run -it ghcr.io/chmouel/agents-image:latest opencode --help
```

### Install additional AUR packages

The image includes `yay` AUR helper, so you can install additional packages:

```bash
docker run -it ghcr.io/chmouel/agents-image:latest bash
# Inside container:
yay -S <package-name>
```

## Build Locally

```bash
docker build -t agents-image .
```

For multi-architecture builds:

```bash
docker buildx build --platform linux/amd64,linux/arm64 -t agents-image .
```

## Automated Builds

This image is automatically built and pushed to GitHub Container Registry:

- **Daily**: Every day at 2 AM UTC
- **On push**: When changes are pushed to the main branch
- **On PR**: For testing (not pushed to registry)
- **Manual**: Via GitHub Actions workflow dispatch

## Architecture Support

- `linux/amd64` (x86_64)
- `linux/arm64` (ARM 64-bit)
  - **Compatible with Apple Silicon** (M1, M2, M3, M4 Macs)
  - Native ARM64 performance (not emulated)

## Image Size Optimization

The Dockerfile uses multi-stage builds to minimize the final image size while keeping essential tools like `yay` for package management.

## License

MIT
