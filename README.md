# Debian CI/CD Container Images

[![Build and Push](https://github.com/a2b-technology-corporation/debian-ci-containers/actions/workflows/build-and-push.yml/badge.svg)](https://github.com/a2b-technology-corporation/debian-ci-containers/actions/workflows/build-and-push.yml)
[![Debian 12](https://img.shields.io/badge/Debian%2012-Bookworm-red?logo=debian)](https://ghcr.io/a2b-technology-corporation/debian-ci)
[![Debian 13](https://img.shields.io/badge/Debian%2013-Trixie-green?logo=debian)](https://ghcr.io/a2b-technology-corporation/debian-ci)
[![Container Registry](https://img.shields.io/badge/ghcr.io-Container%20Registry-blue?logo=github)](https://github.com/a2b-technology-corporation/debian-ci-containers/pkgs/container/debian-ci)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains Debian-based Docker images optimized for GitHub Actions CI/CD workflows.

## Available Images

| Image Tag | Debian Version | Codename | Support Status |
|-----------|---------------|----------|----------------|
| `ghcr.io/a2b-technology-corporation/debian-ci:12` | Debian 12 | Bookworm | Old Stable |
| `ghcr.io/a2b-technology-corporation/debian-ci:13` | Debian 13 | Trixie | Stable |
| `ghcr.io/a2b-technology-corporation/debian-ci:latest` | Debian 13 | Trixie | Stable |

## Pre-installed Tools

All images include:

### Core Tools
- **Git** - Version control
- **curl/wget** - HTTP clients
- **OpenSSH client** - SSH connectivity
- **ca-certificates** - SSL/TLS certificates

### Development Tools
- **Python 3** - With pip and venv
- **Node.js & npm** - JavaScript runtime
- **GCC/G++** - C/C++ compilers
- **Make** - Build automation

### CI/CD Tools
- **Ansible** - Infrastructure automation
- **ansible-lint** - Ansible playbook linting
- **[GitHub CLI (gh)](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)** - GitHub operations
- **jq** - JSON processor
- **yq** - YAML processor

### Utilities
- **zip/unzip** - Archive management
- **tar/gzip/bzip2/xz** - Compression tools
- **sed/awk/grep** - Text processing
- **vim-tiny** - Text editor

## Usage in GitHub Actions

### Basic Usage

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/a2b-technology-corporation/debian-ci:13
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: |
          # All tools are pre-installed!
          python3 --version
          ansible --version
          node --version
```

### Using Specific Debian Version

```yaml
container:
  image: ghcr.io/a2b-technology-corporation/debian-ci:12  # Use Debian 12 (old stable)
```

## Building Locally

```bash
# Build Debian 12 image
docker build -t debian-ci:12 debian-12/

# Build Debian 13 image
docker build -t debian-ci:13 debian-13/

# Test the image
docker run --rm -it debian-ci:13 bash
```

## Automated Builds

Images are automatically built and pushed to GitHub Container Registry:
- On push to `main` branch (when Dockerfiles change)
- Weekly (Sunday 2 AM UTC) for security updates
- On manual workflow dispatch

## Architecture Support

Images are built for multiple architectures:
- `linux/amd64` (x86_64)
- `linux/arm64` (ARM64/Apple Silicon)

## Security

- Base images use `-slim` variants for smaller attack surface
- Images are rebuilt weekly for security updates
- Git safe directory is pre-configured for GitHub Actions
- Non-root user `runner` is available (though GitHub Actions typically overrides this)

## Documentation & Resources

- [Debian Releases](https://wiki.debian.org/DebianReleases) - Information about Debian versions
- [GitHub Actions Containers](https://docs.github.com/en/actions/using-jobs/running-jobs-in-a-container) - Using containers in workflows
- [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) - GHCR documentation
- [GitHub CLI in Actions](https://cli.github.com/manual/gh_help_environment) - Using gh in GitHub Actions

## Contributing

1. Fork the repository
2. Make changes to the appropriate `debian-*/Dockerfile`
3. Test locally with `docker build`
4. Submit a pull request

## License

MIT License - See LICENSE file for details

## Support

For issues or questions, please open an issue in this repository or contact A2B Technology Corporation.
