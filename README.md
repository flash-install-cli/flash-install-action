<p align="center">
  <img src="https://raw.githubusercontent.com/flash-install-cli/flash-install/main/assets/logo.png" alt="flash-install logo" width="200" height="200">
</p>

<h1 align="center">⚡ Flash Install GitHub Action</h1>
<p align="center">Speed up your CI/CD pipeline with Flash Install, a fast npm alternative with deterministic caching</p>

<p align="center">
  <a href="https://github.com/marketplace/actions/flash-install"><img src="https://img.shields.io/badge/GitHub%20Actions-Flash%20Install-yellow" alt="GitHub Actions"></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
  <a href="https://nodejs.org/"><img src="https://img.shields.io/badge/node-%3E%3D%2016.0.0-brightgreen.svg" alt="Node.js Version"></a>
  <a href="https://www.npmjs.com/package/@flash-install/cli"><img src="https://img.shields.io/npm/v/@flash-install/cli" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@flash-install/cli"><img src="https://img.shields.io/npm/dm/@flash-install/cli" alt="npm downloads"></a>
  <a href="https://github.com/flash-install-cli/flash-install/graphs/commit-activity"><img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" alt="Maintenance"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Speed-Up%20to%2050%%20Faster-orange" alt="Speed: Up to 50% Faster">
  <img src="https://img.shields.io/badge/Cache-Deterministic-blue" alt="Cache: Deterministic">
  <img src="https://img.shields.io/badge/Cloud-Team%20Sharing-lightblue" alt="Cloud: Team Sharing">
  <img src="https://img.shields.io/badge/CI/CD-Optimized-green" alt="CI/CD: Optimized">
</p>

<p align="center">
  <b>Compatible with:</b><br>
  <img src="https://img.shields.io/badge/npm-Compatible-red" alt="npm Compatible">
  <img src="https://img.shields.io/badge/yarn-Compatible-blue" alt="yarn Compatible">
  <img src="https://img.shields.io/badge/pnpm-Compatible-orange" alt="pnpm Compatible">
  <img src="https://img.shields.io/badge/bun-Compatible-purple" alt="bun Compatible">
  <img src="https://img.shields.io/badge/Monorepos-Supported-green" alt="Monorepos Supported">
</p>

## Features

- ⚡ **30-50% faster** than standard npm install
- 🔄 **Deterministic caching** for consistent builds
- ☁️ **Cloud caching** support for team sharing
- 🔌 **Multiple package managers** support (npm, yarn, pnpm, bun)
- 🛠️ **Optimized for CI/CD** environments
- 📦 **GitHub Actions caching** integration
- 🏗️ **Monorepo support** with workspace detection
- 🔍 **Fallback to npm** if Flash Install encounters an error

## Usage

Add Flash Install to your GitHub Actions workflow:

```yaml
steps:
  - uses: actions/checkout@v3
  
  - name: Install dependencies with Flash Install
    uses: flash-install-cli/flash-install-action@v1
    with:
      # Optional parameters (shown with defaults)
      command: 'install'           # Command to run (install, restore, snapshot, clean)
      directory: '.'               # Directory to run the command in
      cache-enabled: 'true'        # Enable GitHub Actions caching
      cloud-cache: 'false'         # Enable cloud caching
      cloud-provider: 's3'         # Cloud provider (s3, azure, gcp)
      cloud-bucket: ''             # Cloud bucket name
      cloud-region: ''             # Cloud region
      cloud-prefix: 'flash-install-cache' # Cloud prefix
      package-manager: 'npm'       # Package manager to use (npm, yarn, pnpm, bun)
      concurrency: '4'             # Number of concurrent downloads
```

## Examples

### Basic Usage

```yaml
- name: Install dependencies
  uses: flash-install-cli/flash-install-action@v1
```

### With Cloud Caching (AWS S3)

```yaml
- name: Install dependencies with S3 caching
  uses: flash-install-cli/flash-install-action@v1
  with:
    cloud-cache: 'true'
    cloud-provider: 's3'
    cloud-bucket: 'my-ci-cache-bucket'
    cloud-region: 'us-east-1'
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Using Yarn

```yaml
- name: Install dependencies with Yarn
  uses: flash-install-cli/flash-install-action@v1
  with:
    package-manager: 'yarn'
```

### Using PNPM

```yaml
- name: Install dependencies with PNPM
  uses: flash-install-cli/flash-install-action@v1
  with:
    package-manager: 'pnpm'
```

### Using Bun

```yaml
- name: Install dependencies with Bun
  uses: flash-install-cli/flash-install-action@v1
  with:
    package-manager: 'bun'
```

## Complete Workflow Example

Here's a complete workflow example using Flash Install:

```yaml
name: Build and Test

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
    
    - name: Install dependencies with Flash Install
      uses: flash-install-cli/flash-install-action@v1
    
    - name: Run tests
      run: npm test
    
    - name: Build
      run: npm run build
```

## Input Parameters

| Parameter | Description | Required | Default |
|-----------|-------------|----------|---------|
| `command` | Command to run (install, restore, snapshot, clean) | No | `install` |
| `directory` | Directory to run the command in | No | `.` |
| `cache-enabled` | Enable GitHub Actions caching | No | `true` |
| `cloud-cache` | Enable cloud caching | No | `false` |
| `cloud-provider` | Cloud provider (s3, azure, gcp) | No | `s3` |
| `cloud-bucket` | Cloud bucket name | No | `''` |
| `cloud-region` | Cloud region | No | `''` |
| `cloud-prefix` | Cloud prefix | No | `flash-install-cache` |
| `package-manager` | Package manager to use (npm, yarn, pnpm, bun) | No | `npm` |
| `concurrency` | Number of concurrent downloads | No | `4` |

## How It Works

1. **Setup Node.js**: The action sets up Node.js v16
2. **Install Flash Install**: Installs the Flash Install CLI globally
3. **Setup Cache Directory**: Creates a cache directory for Flash Install
4. **Cache Dependencies**: Uses GitHub Actions caching to store and retrieve the Flash Install cache
5. **Run Flash Install**: Executes the Flash Install command with the specified parameters
6. **Fallback to npm**: If Flash Install fails, falls back to npm for reliability

## Benchmarks

| Project Type | npm install | flash-install | Improvement |
|--------------|------------|---------------|-------------|
| Small App    | 45s        | 28s           | 38% faster  |
| Medium App   | 1m 32s     | 52s           | 44% faster  |
| Large Monorepo | 4m 15s   | 2m 10s        | 49% faster  |

*Benchmarks run on GitHub-hosted runners with cold cache

## Benefits

- **Faster CI/CD**: Reduce your GitHub Actions workflow time
- **Cost Savings**: Shorter workflow runs mean lower GitHub Actions minutes usage
- **Better Developer Experience**: Faster feedback loops for your team
- **Reliable Builds**: Deterministic caching ensures consistent builds
- **Team Sharing**: Share caches across your team with cloud caching
- **Monorepo Support**: Optimized for monorepo projects
- **Fallback Mechanism**: Automatically falls back to npm if any issues occur

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository at https://github.com/flash-install-cli/flash-install-action
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Related Projects

- [Flash Install CLI](https://github.com/flash-install-cli/flash-install) - The main Flash Install CLI project
- [Flash Install Documentation](https://github.com/flash-install-cli/docs) - Comprehensive documentation for Flash Install

## License

MIT

## Acknowledgements

- Thanks to all the open-source projects that made this possible
- Special thanks to all our [sponsors](https://github.com/flash-install-cli/flash-install/blob/main/SPONSORS.md) who make this project sustainable
